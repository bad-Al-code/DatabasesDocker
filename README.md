# Docker Compose for Databases

This repository contains Docker Compose configurations for running various databases and their web interfaces using Docker.

## Overview

The following services are inclued:

- MySQL
- Adminer (Database management tool)
- PostgreSQL
- MongoDB
- Mongo Express (Web-based MongoDB admin interface)
- Redis
- Redis Commander (Redis management tool)

## Usage

#### Prerequisites

- Docker

#### Running services

```bash
docker compose up -d
```

**To run individual services, navigate to their respective directories and run `docker compose up -d.`**

#### Accessing Web Interfaces

- Adminer: http://localhost:8080
- Mongo Express: http://localhost:8081
- Redis Commander: http://localhost:8082

#### Stopping Services

To stop all services:

```bash
docker compose down
```

## Connections

#### PostgreSQL

- `psql` command-line tool

```bash
psql -h localhost -p 5432 -U postgres -d postgres
```

Enter Password: `postgres`

- For Adminer, you can access it via a web browser by navigating to `http://localhost:8081`

#### MYSQL

```bash
mysql -h 127.0.0.1 -P 3306 -u root -p
```

Enter the root password when prompted (the password specified for MYSQL_ROOT_PASSWORD in your Docker Compose file, which is root in your case). Then, you can create databases and perform administrative tasks.

## Configuration

Each service has its own `docker-compose.yml` file in its respective directory. You can customize settings such as volumes, ports, environment variables, etc., as needed.
