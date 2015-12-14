# Dokku
Literally the greatest thing ever.

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
