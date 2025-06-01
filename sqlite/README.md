# Sqlite

This setup run Sqlite in a Docker container.

## Service

1. `sqlite-db`: uses `keinos/sqlite3`. Container runs idle (`tail -f /dev/null`) to allow interaction via cli.
   Data is stored in `/data`

## Volumes

1. `sqlite_data`: Persistes `.sqlite` files.

## Example: Create a DB

````bash

```bash
docker exec -it sqlite-db sqlite3 /data/mydb.sqlite
```

Then use SQL commands or `.exit` to quit.


````
