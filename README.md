lempdock.
===============

> posted: 2019.05.10  
> author: hyano@ampware.jp

## OVERVIEW
The Docker boilerplate for LEMP environment.

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
app> cd laravel
app> php artisan key:generate --show
     > base64:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
app> exit

# Fix nginx setting.
$ vi .docker/web/default.conf
  > server {
  >   # root  /var/www/html;
  >   root /var/www/laravel/public;

# Fix env.
#
# ## NOTE ##
# laravel/.env is ignored,
# if there is a system environment variable of the same name.
# ##########
#
$ vi .env
  > APP_KEY=base64:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
  > DB_HOST=db

# Restart containers.
$ docker-compose down
$ docker-compose up
```
