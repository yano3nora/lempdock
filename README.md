LEMP Docker.
===============

> posted: 2019.05.10  
> author: hyano@ampware.jp

## OVERVIEW
Docker boilerpalte for LEMP environment.

### Composition.
- php 7.2
  - php-fpm
- nginx 1.15.6
- mysql 5.7

### DEPLOYMENT
```sh
# Set .env file.
$ cp .env.development .env

# Build containers.
$ docker-compose build
$ docker-compose up -d

# Login to app container.
$ docker-compose exec app bash

# e.g. Install PHP framework that like the Laravel ...
app> composer create-project --prefer-dist laravel/laravel laravel
app> php artisan key:generate
app> exit
$ vi .docker/web/default.conf
  > server {
  >   # root  /var/www/html;
  >   root /var/www/laravel/public;
$ vi laravel/.env
  > DB_CONNECTION=mysql
  > DB_HOST=db
  > DB_PORT=3306
  > DB_DATABASE="${DB_DATABASE}"
  > DB_USERNAME="${DB_USERNAME}"
  > DB_PASSWORD="${DB_PASSWORD}"
$ docker-compose restart
```
