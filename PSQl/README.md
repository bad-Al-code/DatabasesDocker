# PostgreSQL and Adminer

This repository contains a Docker Compose configuration for setting up a PostgreSQL container along with an Adminer container for database management. The setup includes:

- PostgreSQL: A PostgreSQL database instance.
- Adminer: A lightweight database management tool for managing the PostgreSQL database through a web interface.

### Requirements

- [Docker](https://docs.docker.com/engine/install/)

### Setup and Usage

1. **Customize Environment Variables (Optional)**
   You can modify the default environment varibales for PostgreSQL (database name, username and password) in the `docker-compose.yml` file:

```yml
environment:
  - POSTGRES_DB=your_database_name # Change this to your preferred DB name
  - POSTGRES_USER=your_user_name # Change this to your preferred username
  - POSTGRES_PASSWORD=your_password # Change this to your preferred password
```

2. **Start the Containers**
   In the project directory where your `docker-compose.yml` is located, run the following command to start the container:

```bash
docker compose up -d
```

This will:

- Download the necessary Docker images (`postgres:16` and `adminer:4.8.0`) if not already present.
- Start the PostgreSQL container with the configured databases, user and password.
- Start the Adminer container for web-based database management.

3. **Access the Services**

**PostgreSQL**
The PostgreSQL service will be running on port 5432 of your host machine. You can connect to it using any PostgreSQL client (e.g., psql, pgAdmin, or your application) using the following connection details:

- Host: `localhost`
- Port: `5432`
- Database: `postgres` (or the custom database name you specified)
- Username:`postgres` (or the custom username you specified)
- Password: `postgres` (or the custom password you specified)

**Adminer**
To access the Adminer web interface, open your browser and go to:

```bash
http://localhost:8080
```

Log in using the following details:

- System: `PostgreSQL`
- Server: `postgresql` (container name defined in the `docker-compose.yml`)
- Username: `postgres`(or the custom username you specified)
- Password: `postgres` (or the custom password you specified)
- Database: `postgres` (or the custom database name you specified)

4. **Running the `psql` Commands Inside the PostgreSQL Container**
   To run `psql` commands inside the PostgreSQL container, you can use the following Docker command to access the `psql` shell:

```bash
docker-compose exec postgresql psql -U postgres
```

This command will open the `psql` command-line interface connected to the PostgreSQL database. You can replace `postgres` with your custom database username if needed.

Once you're inside the `psql` shell, you can execute any PostgreSQL commands (e.g., `SELECT`, `INSERT`, `CREATE`, etc.).

To exit the `psql` shell, simply type:

```bash
\q
```

5. **Healthecheck and Logs**

- The PostgreSQL container includes a health check that esures the database is ready. You can check the status of the health check with:

```bash
docker compose ps
```

This will display the status of all containers. The PostgreSQL container should show `healthy` if everything is running fine - To view logs for both services, you can run:

```bash
docker compose logs postgresql
docker compose logs adminer
```

6. **Stopping the container**
   To stop the container

```bash
docker compose down
```

This command stops and removes the containers but preserves your data in the `./data/postgresql` directory on your local machine.

7. **Persistent Data**
   The postgresql service uses a volume to store its data persistently. Data is saved in the `./data/postgresql` directory on your host machine. This ensures your database persists even if the containers are stopped or removed.

8. **Restarting the container**
   If you need to restart the containers, use the following command:

```bash
docker compose restart
```

### Troubleshooting

- If you face any issues with the containers, you can check the logs using `docker-compose logs <service-name>`.
- Ensure that port `5432` is not being used by another PostgreSQL instance on your local machine.

Enjoy PostgreSQL inside a docker container.
