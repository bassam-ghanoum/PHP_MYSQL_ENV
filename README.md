# EDI Docker Environment

This repository contains a Docker-based development environment for the EDI system.

## Services

- `EDI_System`: Symfony application runtime on PHP 8.5 with PHP-FPM
- `EDI_Nginx`: Nginx web server for the Symfony `public/` directory
- `EDI_MySQL`: MySQL 8.4 database server
- `EDI_phpMyAdmin`: phpMyAdmin UI for database administration

## Start the environment

```bash
docker compose up --build -d
```

## Access points

- Application: `http://localhost:8080`
- phpMyAdmin: `http://localhost:8081`
- MySQL from host tools: `127.0.0.1:3307`

## Prepare Symfony 8

The Docker environment provides PHP-FPM, Nginx, MySQL, and phpMyAdmin. Install Symfony explicitly inside the PHP container after the stack is up:

```bash
docker compose exec edi_system composer create-project symfony/skeleton:^8.0 .
docker compose exec edi_system composer require webapp
```

If `app/` already contains a Symfony project, use:

```bash
docker compose exec edi_system composer install
```

If port `3306` is already used on your machine, the project maps MySQL to host port `3307` by default via `.env`.

If Composer reports that Symfony 8 is not yet available in your package index, use the latest Symfony 7 release temporarily and upgrade later.
