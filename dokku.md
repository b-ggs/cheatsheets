# Dokku
Literally the greatest thing ever.

## Setting up Dokku on DigitalOcean
Updated info will probably be [here](http://dokku.viewdocs.io/dokku/installation/).

Set up a fresh $10 Ubuntu 14.04 droplet from DigitalOcean

Install
```
wget https://raw.githubusercontent.com/dokku/dokku/v0.4.6/bootstrap.sh
sudo DOKKU_TAG=v0.4.6 bash bootstrap.sh
```

## Deploying on Dokku
This is a tl;dr. More info [here](http://dokku.viewdocs.io/dokku/application-deployment/).

Create the app on the Dokku host
```
dokku apps:create #{app_name}
```

Create backing services ([full list of services](http://dokku.viewdocs.io/dokku/plugins/#official-plugins-beta))
```
sudo dokku plugin:install https://github.com/dokku/dokku-postgres.git
dokku postgres:create #{app_name}-database
```

Link backing services to applications
```
dokku postgres:link #{app_name}-database #{app_name}
```

Deploy the app
```
git remote add dokku dokku@#{host}:#{app_name}
git push dokku master
```

## Only use subdomains for apps
Taken from [this DO question](https://www.digitalocean.com/community/questions/how-do-i-reconfigure-top-level-routing-on-the-digitalocean-dokku0-2-3-14-04-one-click-application).

Edit `/etc/nginx/conf.d/dokku.conf`.

Add the following lines:
```
server {
  listen 80;
  server_name boggs.xyz; # Root domain

  return 301 http://soon.boggs.xyz;  #New URL
}
```

Restart nginx with `/etc/init.d/nginx restart`.
