# Locel Reverse Proxy

This repository contains a simple reverse proxy (NGINX) with automatic SSL certificate renewal (Certbot). The default configuration provides support for a single domain on both HTTP (redirects all traffic to HTTPS) and HTTPS.

## Setup and Run

- Obtain the initial certificates;
  - You can run `docker compose run -it certbot sh` to create a temporary container and follow the documentation to generate certificates for your domain;
- Configure environment variables in `common.env` and `sensitive.env`;
  - `common.env` requires `HTTP_PORT` (target HTTP port for NGINX), `HTTPS_PORT` (target HTTPS por for NGINX), `ACME_CHALLENGE` (path to ACME well-known);
  - `sensitive.env` requires `SERVER_NAME`, `CERT_PEM` (path), `CERT_KEY` (path), `PROXY_HOST` (actual server that provides the webserver functionality), `PROXY_PORT`;
- Additionally add filtering rules for the HTTPS server in `data/nginx/conf.d/filters/` (you can add as many `.conf` files as desirable);
- Update firewall rules on the host to ensure the web server can be accessible;
- Run `docker compose up -d`;
