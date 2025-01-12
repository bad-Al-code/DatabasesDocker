# Redis And Redis Commander

This repository contains a Docker Compose configuration for setting up a Redis container along with a Redis Commander container for database management. The setup includes:

- **Redis**: A Redis instance with persistence enabled using the append-only file (AOF) method.
- **Redis Commander**: A web-based interface for managing Redis.

### Requirements

- [Docker](https://docs.docker.com/engine/install/)

### Setup and Usage

1. **Customize Environment Variables (Optional)**
   You can modify the default environment variable for Redis Commander in the `docker-compose.yml` file:

```bash
environment:
  - REDIS_HOSTS=local:redis:6379  # Change this if you want to connect to a different Redis instance
```

2. **Start the Containers**
   In the project directory where your `docker-compose.yml` is located, run the following command to start the containers:

```bash
docker-compose up -d
```

This will:

- Download the necessary Docker images (`redis:alpine3.20` and `rediscommander/redis-commander:latest`) if not already present.
- Start the Redis container with persistence enabled.
- Start the Redis Commander container for web-based management.

3. **Access the Service**
   The Redis service will be running on port 6379 of your host machine. You can connect to it using any Redis client (e.g., `redis-cli`, a library in your application, or your preferred Redis GUI tool) using the following connection details:

- Host: `localhost`
- Port: `6379`

**Redis Commander**
To access the Redis Commander web interface, open your browser and go to:

```bash
http://localhost:8081
```

You can now use the Redis Commander interface to manage your Redis instance. It will be pre-configured to connect to the Redis container via the `redis` hostname.

4. **Running Redis Commands Inside the Redis Container**
   To run Redis commands inside the Redis container, you can use the following Docker command to access the `redis-cli`:

```bash
docker-compose exec redis redis-cli
```

This will open the redis-cli command-line interface connected to the Redis container. From here, you can run any Redis commands (e.g., SET, GET, DEL, etc.).

To exit the `redis-cli`, simply type:

```bash
exit
```

5. **Healthecheck and Logs**

- The Redis container includes a health check that ensures the Redis service is ready. You can check the status of the health check with:

```bash
docker compose ps
```

This will display the status of all containers. The Redis container should show `healthy` if everything is running fine.

````bash
docker-compose logs redis
docker-compose logs redis-commander`

6. **Stopping the container**
   To stop the container

```bash
docker compose down
````

This command stops and removes the containers but preserves your data in the `./data/redis` directory on your local machine.

7. **Persistent Data**
   The Redis service uses a volume to store its data persistently. Data is saved in the ./data/redis directory on your host machine. This ensures your Redis data persists even if the containers are stopped or removed.

8. **Restarting the container**
   If you need to restart the containers, use the following command:

```bash
docker compose restart
```

### Troubleshooting

- If you face any issues with the containers, you can check the logs using `docker-compose logs <service-name>`.
- Ensure that port 6379 is not being used by another Redis instance on your local machine.

Enjoy Redis inside a docker container.
