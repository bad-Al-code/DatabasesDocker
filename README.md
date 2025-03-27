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
- ChromaDB (Vector database)
- Pinecone Indexes (Dense & Sparse Indexing)

# Features

- ✅ Daily automatic backups for MySQL, PostgreSQL, and MongoDB
- ✅ Auto-cleanup of backups older than 14 days
- ✅ Optimized resource allocation for better performance
- ✅ Health checks for all database services
- ✅ Web-based database management

## Usage

#### Prerequisites

- Docker
- Create a `.env` file in the project root and configure it as shown below.

### Environment Variables

Copy the following into your .env file and update values as needed:

```bash
# MySQL Configuration
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=my_database
MYSQL_USER=my_user
MYSQL_PASSWORD=my_password

# PostgreSQL Configuration
POSTGRES_DB=my_database
POSTGRES_USER=my_user
POSTGRES_PASSWORD=my_password

# MongoDB Configuration
MONGO_INITDB_ROOT_USERNAME=mongo_user
MONGO_INITDB_ROOT_PASSWORD=mongo_password

# Redis Configuration
REDIS_HOSTS=redis

# ChromaDB Configuration
IS_PERSISTENT=true
CHROMA_DB_DIR=/chroma/.chroma

```

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

## Database Connections

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

## Backup System

Backups are stored in the ./backups/ directory and cleaned up automatically every 14 days.

- MySQL: ./backups/mysql/
- PostgreSQL: ./backups/postgresql/
- MongoDB: ./backups/mongodb/

## Configuration

Each service has its own `docker-compose.yml` file in its respective directory. You can customize settings such as volumes, ports, environment variables, etc., as needed.
