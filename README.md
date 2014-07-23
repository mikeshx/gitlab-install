# GitLab Automated Installation

This repository holds scripts that will perform automated installation of [GitLab](http://gitlab.org) on your server.

## Supported Systems

These are currently the tested and supported systems.

* Ubuntu Server 12.04 64-Bit
* Ubuntu Server 13.04 64-Bit

## Usage

### Ubuntu

For __Ubuntu Server 12.04 or 13.04 64-Bit__, issue the following commands. Ensure that you use the `-d` or `--domain-var` flags to specify your domain name, and `--mysql` or `--postgresql` to choose your database. PostgreSQL is the default, and is recommended.

```bash
# Download the script and make it executable
wget -O ~/ubuntu.sh https://raw.github.com/mikeshx/gitlab-install/master/ubuntu-server-12.04.sh
chmod u+x ~/ubuntu.sh

# Display the help menu
~/ubuntu.sh (-h OR --help)

# Run the script
sudo ~/ubuntu.sh -d gitlab.example.com (--mysql OR --postgresql)
```

## Troubleshooting

If you run into problems, the first thing to check is to make sure that each file got it's proper configuration added. Everything listed below should happen automatedly, but there is always a chance for error. You can also check out the [GitLab Troubleshooting Guide](https://github.com/gitlabhq/gitlab-public-wiki/wiki/Trouble-Shooting-Guide) for further help. The following are the files to check and what should be set:

#### /home/git/gitlab-shell/config.yml

This file should have the gitlab_url set to the URL of your GitLab instance (with a trailing slash).

```bash
  gitlab_url: "http://gitlab.example.com/"
```

#### /home/git/gitlab/config/gitlab.yml

This file should have the hostname set under the web server settings.

```bash
gitlab:
  ## Web server settings
  host: gitlab.example.com
  port: 80
```

#### /home/git/gitlab/config/database.yml

This file should have the gitlab user and password for the database configuration.

```bash
production:
  username: gitlab
  password: kenvo2i3j0239urlks
```

#### /etc/nginx/sites-available/gitlab

This file should have the server name in the virtual host set to your domain.

```bash
server {
  listen *:80;
  server_name gitlab.example.com;
  server_token off;
  root /home/git/gitlab/public;
}
```
