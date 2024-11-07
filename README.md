# IntelliCook All Backends

This repository contains the docker compose file for all the backends of IntelliCook.

## Services

[🎛️ App Controller](https://github.com/intellicook/app-controller)

[🔐 Auth](https://github.com/intellicook/auth)

[🔎 Recipe Search](https://github.com/intellicook/recipe-search)

## Docker Compose

We use [Docker](https://www.docker.com) and [Docker Compose](https://docs.docker.com/compose) to manage the environment in both development and production.

Before starting anything, you have to define the environment variables in the `.env` file.

The `docker-compose.yml` uses the `.env` files in the respective services, then override those with the `.env.example` file in this repository. The most essential environment variables are already in the current `.env.example` file.

You can copy the `.env.example` file and fill in the values.
```bash
cp .env.example .env
```

With Docker Compose, you can run the services in the `docker-compose.yml` file:
```bash
docker-compose up
```

## Kubernetes

We use [Kubernetes](https://kubernetes.io) to manage the environment in production.

All the Kubernetes configuration files are in the `k8s` directory.

**Note**: Our AWS EC2 instance do not run Kubernetes at the moment due to resource constraints.