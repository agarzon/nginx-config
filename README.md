# Nginx Template

Easy to understand and extend Nginx configuration template

## Features
 * GZIP compression support
 * PHP handling support
 * Cache for static files
 * It never replaces any built-in configuration. Upgrading your Nginx will be always safe.

## Installation
Just put the code in your **/etc/nginx**

Add this line at end of you **/etc/nginx/nginx.conf**:
```nginx
    include /etc/nginx/sites-enabled/*.conf;
```

## Usage

To create a site, add a file with extension **.conf** in **sites-enabled/** folder. Example:

**/etc/nginx/sites-enabled/example.conf**

```nginx
server
{
    listen 80;
    server_name mywebsite.com;
    root /var/www/html/project/folder/;
    include templates/default.conf;
    include templates/gzip.conf;
    include templates/php.conf;
    include templates/static-cache.conf;
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

Include in your nginx configuration file:
```nginx
include templates/ssl.conf;
```
