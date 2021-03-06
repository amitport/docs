- [Deploying on Heroku](#heroku)
- [Deploying on Zeit Now](#zeit-now)
- [Deploying on Nginx (recommended)](#nginx-recommended)

## Heroku

You can deploy the [colyseus-examples](https://github.com/gamestdio/colyseus-examples) project on Heroku by hitting this button:

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/gamestdio/colyseus-examples)

## Zeit Now

You can deploy the [colyseus-examples](https://github.com/gamestdio/colyseus-examples) project on Zeit Now by hitting this button:

[![Deploy to now](https://deploy.now.sh/static/button.svg)](https://deploy.now.sh/?repo=https://github.com/gamestdio/colyseus-examples)

## Nginx (recommended)

It's recommended to use `forever` and `nginx` in your production environment.

### PM2

Install `pm2` in your environment.

```
npm install -g pm2
```

Then start your game server using it:

```
pm2 start your-server.js -i 0
```

### Nginx configuration

```
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_read_timeout 86400s;
        proxy_send_timeout 86400s;
    }
}
```

### Nginx configuration with SSL

It's recommended to acquire your certificate from [LetsEncrypt](https://letsencrypt.org).

```
server {
    listen 80;
    listen 443 ssl;
    server_name yourdomain.com;

    ssl_certificate /path/to/your/cert.crt;
    ssl_certificate_key /path/to/your/cert.key;

    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_read_timeout 86400s;
        proxy_send_timeout 86400s;
    }
}
```
