# Docker Environment

This repository contains a Docker-based development environment for the PHP MySql system development.

## Services

- `system_environment`: Symfony application runtime on PHP 8.5 with PHP-FPM
- `nginx_environment`: Nginx web server for the Symfony `public/` directory
- `mysql_environment`: MySQL 8.4 database server
- `phpmyadmin_environment`: phpMyAdmin UI for database administration

## Start the environment

Create a local root `.env` from `.env.example` and set your own database passwords before starting the stack.

```bash
docker compose up --build -d
```

## Access points

- Application: `http://localhost:8080`
- phpMyAdmin: `http://localhost:8081`
- MySQL from host tools: `127.0.0.1:3307`

All published ports bind to `127.0.0.1` and are intended for local development. The Symfony runtime defaults to `APP_ENV=dev` with `APP_DEBUG=0`; set `APP_ENV=prod` and keep `APP_DEBUG=0` for production-mode application behavior. This Compose setup is not a complete production deployment; do not expose the database or phpMyAdmin publicly.

## Prepare Symfony 8

The Docker environment provides PHP-FPM, Nginx, MySQL, and phpMyAdmin. Install Symfony explicitly inside the PHP container after the stack is up:

```bash
docker exec system_environment composer create-project symfony/skeleton:^8.0 .
docker exec system_environment composer require webapp
```

If `app/` already contains a Symfony project, use:

```bash
docker exec system_environment composer install
```

If port `3306` is already used on your machine, the project maps MySQL to host port `3307` by default via `.env`.

If Composer reports that Symfony 8 is not yet available in your package index, use the latest Symfony 7 release temporarily and upgrade later.
