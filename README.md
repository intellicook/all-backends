# IntelliCook All Backends

This repository contains the docker compose file for all the backends of IntelliCook.

## Services

[🎛️ App Controller](https://github.com/intellicook/app-controller)

[🔐 Auth](https://github.com/intellicook/auth)

[🔎 Recipe Search](https://github.com/intellicook/recipe-search)

## Quick Start

To start all the services locally:

1. Make sure you have [Docker](https://www.docker.com) and [Docker Compose](https://docs.docker.com/compose) installed.

2. Clone all the repositories of the services from the [Services](#services) section.

3. Copy the `.env.example` file in each repository to `.env`.

4. You may also need to make `entrypoint.sh` in the `recipe-search` repository executable by running the following command in the repository:

    ```bash
    chmod +x entrypoint.sh
    ```

5. Fill in the variables in the `.env` file in this repository, which are the most essential variables and they override the `.env` files in the respective services.
    
    - Other variables not in the `.env` file in this repository can be filled in the `.env` files in the respective services' repositories.

6. Run docker compose:
    ```bash
    docker compose up
    ```

    - For ARM-based systems, because [MSSQL does not support ARM](https://github.com/microsoft/mssql-docker/issues/802), we have a separate docker compose file as a temporary solution:
        ```bash
        docker compose -f docker-compose-arm.yml up
        ```

7. The services should be running now, you can reach them at the following URLs:

    - App Controller [OpenAPI](https://www.openapis.org/) specification: http://localhost:2501/swagger/index.html/

    - Auth [OpenAPI](https://www.openapis.org/) specification: http://localhost:2503/swagger/index.html/

    - Recipe Search [gRPC](https://grpc.io/) (support server reflection): grpc://localhost:2505/

## Service Names

All IntelliCook services are in the format `[service name]-api`, while all the third-party services are in the format `[service name]-[service type]`.

The following service types are used:

- `se`: Search Engine

- `db`: Database

## Ports

All the ports are in 4-digit numbers.

First 2 digits represents whether it is an IntelliCook service or a third-party service. `25` is for IntelliCook services and `26` is for third-party services.

Last 2 digits are randomly assigned.

Ports are assigned based on the following table, where rows are the first 2 digits and columns are the last 2 digits:

```
      | ##00   | ##01               | ##02   | ##03     | ##04   | ##05              | ##06         | ##07
------+--------+--------------------+--------+----------+--------+-------------------+--------------+---------------------------
 25## |        | app-controller-api |        | auth-api |        | recipe-search-api |              | ingredient-recognition-api
------+--------+--------------------+--------+----------+--------+-------------------+--------------+---------------------------
 26## |        |                    |        | mssql-db |        | postgres-db       | typesense-se |
```

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
docker compose up
```

## Kubernetes

We use [Kubernetes](https://kubernetes.io) to manage the environment in production.

All the Kubernetes configuration files are in the `k8s` directory.

**Important**: Kubernetes configuration files are outdated and need to be updated.

**Note**: Our AWS EC2 instance do not run Kubernetes at the moment due to resource constraints.