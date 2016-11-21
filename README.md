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
    listen          80;
    server_name     mywebsite.com;
    root            /var/www/html/project/folder/;
    include templates/default.conf;
    include templates/gzip.conf;
    include templates/php.conf;
    include templates/static-cache.conf;
}

```
