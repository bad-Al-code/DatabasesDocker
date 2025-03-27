# MongoDB

This repository contains a Docker Compose configuration for setting up a MongoDB container along with a Mongo Express container for database management. The setup includes:

## Features

- MongoDB with authentication enabled
- Mongo Express web-based UI for managing the database
- Persistent storage for MongoDB data
- Automated daily backups with 14-day retention
- Health checks for MongoDB service
- MongoDB with authentication enabled
- Mongo Express web-based UI for managing the database
- Persistent storage for MongoDB data
- Automated daily backups with 14-day retention
- Health checks for MongoDB service
- Optimized resource allocation Optimized resource allocation

### Requirements

- [Docker](https://docs.docker.com/engine/install/)

### Setup and Usage

1. **Configure Environment Variables**
   Before running the containers, make sure you have a `.env` file in your project root .

```bash
# MongoDB Configuration
MONGODB_USER=rootuser
MONGODB_PASSWORD=rootpass
MONGODB_DATABASE=my_database
MONGODB_PORT=27017

# Mongo Express Configuration
MONGO_EXPRESS_PORT=8081

# Backup Configuration
BACKUP_RETENTION_DAYS=14
```

2. **Start the Containers**
   In the project directory where your `docker-compose.yml` is located, run the following command to start the containers:

```bash
docker-compose up -d
```

This will:

- Pull the latest MongoDB and Mongo Express images (if not already available).
- Start MongoDB with authentication and persistent storage.
- Start Mongo Express for web-based database management.
- Set up automated backups for MongoDB.

3. **Access the Service**

**MongoDB**

- Host: localhost
- Port: 27017
- Username: rootuser (or value from .env)
- Password: rootpass (or value from .env)

**Mongo Express**
To access the Mongo Express web interface, open your browser and go to:

```bash
http://localhost:8081
```

**Login Details**:

- Username: rootuser (from .env)
- Password: rootpass (from .env)

4. **Running MongoDB Commands Inside the MongoDB Container**

To open the MongoDB shell inside the container:

```bash
docker compose exec mongodb mongo -u $MONGODB_USER -p $MONGODB_PASSWORD
```

Once inside, you can run MongoDB queries such as:

```bash
show databases;
use my_database;
db.stats();
```

To exit the shell, type:

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

- MongoDB data is persistently stored in the ./data/mongodb/ directory.
- Automated daily backups are stored in ./backups/mongodb/ and deleted after 14 days.

If you need to manually trigger a backup, run:

```bash
docker compose exec mongodb-backup sh -c "mongodump --host mongodb --username $MONGODB_USER --password $MONGODB_PASSWORD --out /backups/mongodb-manual-$(date +%F)"
```

### Troubleshooting

- If you face any issues with the containers, you can check the logs using `docker-compose logs <service-name>`.
- Ensure that port 6379 is not being used by another MongoDB instance on your local machine.

Enjoy MongoDB inside a docker container.
