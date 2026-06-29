# Magento 2.4.9 Docker Environment

Generic Docker setup for running **Magento Open Source / Adobe Commerce 2.4.9** locally.

This project provides a development-friendly stack using:

* PHP 8.5 FPM
* Nginx
* MariaDB 12.3
* OpenSearch 3
* Composer 2.10+
* Valkey
* Mailpit

The goal of this repository is to provide a quick local environment for Magento development, testing, and study.

## Requirements

Before starting, make sure you have:

* Docker
* Docker Compose
* Adobe Commerce Marketplace credentials for `repo.magento.com`

Magento itself is not included in this repository. You need to install it with Composer after the containers are built.

## Getting Started

Build and start the containers:

```bash
docker compose up -d --build
```

After the containers are running, check the additional setup instructions in:

```txt
php/README.me
```

That file contains the commands needed after the container is built, including Magento installation and local configuration steps.

## Services

Default local services:

```txt
Magento Storefront: http://localhost:8080
Magento Admin:      http://localhost:8080/admin
Mailpit:            http://localhost:8025
OpenSearch:         http://localhost:9200
MariaDB:            localhost:3307
```

## Notes

This setup is intended for local development only.

It does not include production services such as Varnish, RabbitMQ, or S3 by default. Those can be added later depending on the project needs.

## License

This project is available under the MIT License.
