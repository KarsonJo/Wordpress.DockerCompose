# Overview

One-click WordPress deployment in production environment, saving time for small applications.

For a more detailed explanation [please refer to my blog](https://www.karsonjo.com/build-a-wordpress-site-with-one-click) (in Chinese).

# Features

1. No torture, painless configuration
   1. No need to install database in advance
   1. No need to install PHP in advance
1. Deployment scripts are simple to the extreme
1. Ready for file upload
1. Ready for installing plugins and themes
1. No permissions problems
   - No weird "why can't I change the site language" problem.
1. Nginx reverse proxy
   - Support HTTPS
   - Support HTTP redirection

# Instructions

## Requirements

1. [Docker](https://www.docker.com/)

## Configuration

### Environment variables

Copy `.env.template` to `.env` and fill in the environment variables:

```bash
# Databse name for wordpress
DB_NAME=wordpress
# Database user name
DB_USER=wordpress
# Database user password
DB_PASSWORD=wordpress

# Your domain name
NGINX_HOST=wp.lndo.site
```

### SSL Certificate

Replace the contents of the following files with your site's SSL certificate:

- PRIVATE KEY: `./ssl/wp.key`
- CERTIFICATE: `./ssl/wp.pem`

### Modify file upload limits (optional)

By default, files up to 128MB are allowed to be uploaded. Modify `./php/php.ini` if you want to change the limit:

```bash
file_uploads = On
memory_limit = 512M
upload_max_filesize = 128M
post_max_size = 128M
max_execution_time = 600
client_max_body_size =  128M
```

Modify 128M to a greater value. And increase the memory limit and transfer time appropriately.

If you need to support uploading files exceeding 1G, open `./nginx/wp.conf.template` and modify the `client_max_body_size`:

```bash
client_max_body_size 1G;
```

### Deploy

```bash
docker compose up
```

Open your site in the browser and complete the setup. (Defaults to [https://wp.lndo.site](https://wp.lndo.site))
