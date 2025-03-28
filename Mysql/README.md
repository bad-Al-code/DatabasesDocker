# MySQL

This guide explains how to set up and use the provided Docker Compose file to run a MySQL database and Adminer for database management.

### Prerequisites

- [Docker](https://docs.docker.com/engine/install/)

### Setup And Usage

1. **Start the Container**

```bash
docker compose up -d
```

- `-d` runs container in detached mode (in the background)

2. **Access the Adminer Interfac**

Once the container are running, you can access Adminer in your web browser:

- URL: `http:localhost:8000`
- Use the following credentials to log in:
  - System: MySQL
  - Server: `mysql` (or `localhost` if running directly on the host machine)
  - Username: `mysql`
  - Password: `mysql`
  - Database: `mysql` (change database accordingly)

3. **Interact with MySQL Database in CLI**

To execute commands directly on the MySQL database:

- List the runnign containers to find MySQL container ID:

```bash
docker ps
```

Look for the container with the `mysql:8.0-bookworm` image

- Access the MySQL container:

```bash
docker exec -it <container_id_or_name> mysql -u root -p
```

Replace `<container_id_or_name>` with the actual container Id or name from the `docker ps` output.

- Enter the root password (`root`) when prompted to log in.

4. **Stop the container**

To stop the container, run:

```bash
docker compose down
```

This will stop and remove the containers whi;e preserving the data stored in the `./data/mysql/` directory.

5. **Resetting the container**

If you want to clear all the data and start fresh, delete the `./data/mysql/` directory

```bash
rm -rf ./data/mysql/
```

If ask for sudo previlleges, run `sudo rm -rf ./data/mysql/`

Then restart the containers:

```bash
docker compose up -d
```

## Environment Variables

Copy the following into a `.env.sample` and rename to `.env` file in the project root and update values as needed:

```bash
# MySQL Configuration
MYSQL_ROOT_PASSWORD=root
MYSQL_DATABASE=my_database
MYSQL_USER=my_user
MYSQL_PASSWORD=my_password
```

## Backup System

Backups are automatically created and stored in the ./backups/mysql/ directory.
Older backups are deleted after 14 days to save space.

## HealthCheck

The MySQL container has a built-in health check to ensure it's running correclty. It checks
MySQL availability every 30 seconds.

## Resource Allocation

To ensure **better performance**, MySQL has the following resource limits:

- Max CPU: `2 vCPUs`
- Max Memory: `2GB`
- Reserved CPU: `1 vCPUs`
- Reserved Memory: `1GB`

### Troubleshooting

- **MySQL Connection Issues**: Ensure the `db-network` is correctly set up and both containers are running.

- **Ports Already in Use**: If ports 3306 or 8080 are already in use, modify the ports section in the `docker-compose.yml` file to use different host ports, e.g., `3307:3306` or `8081:8080`.

Enjoy your MySQL and Adminer Setup inside a docker container!
