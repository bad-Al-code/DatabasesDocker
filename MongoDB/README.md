# Redis And Redis Commander

This repository contains a Docker Compose configuration for setting up a MongoDB container along with a Mongo Express container for database management. The setup includes:

- **MongoDB**: A MongoDB database instance with authentication enabled.
- **Mongo Express**: A web-based interface for managing MongoDB.

### Requirements

- [Docker](https://docs.docker.com/engine/install/)

### Setup and Usage

1. **Customize Environment Variables (Optional)**
   You can modify the default environment variable for MongoDB and Mongo Express in the `docker-compose.yml` file:

```bash
environment:
  - MONGO_INITDB_ROOT_USERNAME=rootuser  # Change to your desired MongoDB root username
  - MONGO_INITDB_ROOT_PASSWORD=rootpass  # Change to your desired MongoDB root password

mongo-express:
  - ME_CONFIG_MONGODB_ADMINUSERNAME=rootuser  # Ensure this matches MongoDB root username
  - ME_CONFIG_MONGODB_ADMINPASSWORD=rootpass  # Ensure this matches MongoDB root password
```

2. **Start the Containers**
   In the project directory where your `docker-compose.yml` is located, run the following command to start the containers:

```bash
docker-compose up -d
```

This will:

- Download the necessary Docker images (`redis:alpine3.20` and `rediscommander/redis-commander:latest`) if not already present.
- Start the MongoDB container with persistence enabled.
- Start the MongoDB Express container for web-based management.

3. **Access the Service**

**MongoDB**
The MongoDB service will be running on port 27017 of your host machine. You can connect to it using any MongoDB client (e.g., `mongo`, a library in your application, or MongoDB Compass) using the following connection details:

- Host: `localhost`
- Port: `27017`

**Mongo Express**
To access the Mongo Express web interface, open your browser and go to:

```bash
http://localhost:8081
```

You can now use the Mongo Express interface to manage your MongoDB instance. It will be pre-configured to connect to the MongoDB container via the `mongodb` hostname.

4. **Running MongoDB Commands Inside the MongoDB Container**

To run MongoDB commands inside the MongoDB container, you can use the following Docker command to access the Mongo shell:

```bash
docker-compose exec mongodb mongo -u rootuser -p rootpass
```

This will open the `mongo` shell connected to the MongoDB container with authentication. From here, you can run any MongoDB commands (e.g., db.stats(), show collections, etc.).

To exit the `redis-cli`, simply type:

```bash
exit
```

5. **Healthecheck and Logs**

- The MongoDB container includes a health check that ensures the MongoDB service is ready. You can check the status of the health check with:

```bash
docker compose ps
```

This will display the status of all containers. The MongoDB container should show `healthy` if everything is running fine.

````bash
docker-compose logs redis
docker-compose logs redis-commander`

6. **Stopping the container**
   To stop the container

```bash
docker compose down
````

This command stops and removes the containers but preserves your data in the `./data/mongodb/` directory on your local machine.

7. **Persistent Data**
   The MongoDB service uses a volume to store its data persistently. Data is saved in the `./data/mongodb` directory on your host machine. This ensures your MongoDB data persists even if the containers are stopped or removed.

8. **Restarting the container**
   If you need to restart the containers, use the following command:

```bash
docker compose restart
```

### Troubleshooting

- If you face any issues with the containers, you can check the logs using `docker-compose logs <service-name>`.
- Ensure that port 6379 is not being used by another MongoDB instance on your local machine.

Enjoy MongoDB inside a docker container.
