# Nginx Configuration Template

Easy to understand and extend Nginx configuration template

## Features
 * GZIP compression support
 * PHP handling support
 * Cache for static files
 * SSL support with http2
 * Stronger cypher. SSL rating A+.
 * It never will replace any built-in configuration. Upgrading your Nginx will be always safe.

## Installation
Just put the code in your **/etc/nginx**

## Usage
To create a site, add a file with extension **.conf** in **sites-enabled/** folder. Example:

**/etc/nginx/sites-enabled/example.conf**

```nginx
# Force HTTPS
{
    server_name     mywebsite.com;
    return          301 https://$server_name$request_uri;
}

server
{
    server_name     mywebsite.com;
    root            /var/www/$server_name/;

    listen          443 ssl http2;
    ssl_certificate /etc/nginx/ssl/nginx.crt;
    ssl_certificate_key /etc/nginx/ssl/nginx.key;

    access_log /var/log/nginx/mywebsite.com.log combined buffer=10k flush=1m;
    error_log /var/log/nginx/mywebsite.com.error.log error;

    include templates/default.conf;
    #include templates/php.conf;
    include templates/no-php.conf;
    include templates/gzip.conf;
    include templates/static-cache.conf;
    include templates/ssl.conf;
}

```

## Create the Self-Signed SSL Certificate
```
sudo openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt
```

And complete the prompt:
```
Country Name (2 letter code) [XX]:CA
State or Province Name (full name):Quebec
Locality Name (eg, city) [Default City]:Montreal
Organization Name (eg, company) [Default Company Ltd]:ACME
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:*.domain.com
Email Address []:
```

## Generate a dhparam key for stronger security
```
openssl dhparam -out /etc/nginx/ssl/dhparams.pem 2048
```
