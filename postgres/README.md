# PostgreSQL

Shared PostgreSQL infrastructure for the home server.

This stack provides:

* PostgreSQL — shared database server
* pgAdmin — PostgreSQL administration UI

PostgreSQL databases are persisted in a Docker volume so recreating the containers does not remove database data.

## Directory

```text
PostgreSQL/
├── docker-compose.yaml
├── .env.example
├── .env.local
└── README.md
```

## First-time setup

Copy the example environment file:

```bash
cp .env.example .env.local
```

Edit the local environment file:

```bash
nano .env.local
```

Set the required passwords and configuration values.

## Start the stack

```bash
docker compose --env-file .env.local up -d
```

Check the containers:

```bash
docker compose ps
```

Follow PostgreSQL logs:

```bash
docker compose logs -f postgres
```

Follow pgAdmin logs:

```bash
docker compose logs -f pgadmin
```

## Access pgAdmin

From another device on the home network:

```text
http://<SERVER_IP>:5050
```

Log in using the pgAdmin credentials configured in `.env.local`.

### Connect pgAdmin to PostgreSQL

When creating the PostgreSQL server connection in pgAdmin:

```text
Host: postgres
Port: 5432
Username: postgres
Password: <POSTGRES_PASSWORD>
```

`postgres` is the Docker Compose service name. Do not use `localhost` when connecting from the pgAdmin container.

## PostgreSQL access from other containers

Applications running on the same Docker network can connect to PostgreSQL using:

```text
postgres:5432
```

Applications outside the Docker network should use the server's LAN address and exposed PostgreSQL port, if one is configured.

## Stop the stack

```bash
docker compose --env-file .env.local down
```

This removes the containers but **does not remove the PostgreSQL data volume**.

## Restart the stack

```bash
docker compose --env-file .env.local up -d
```

## Update images

Pull newer images:

```bash
docker compose --env-file .env.local pull
```

Recreate the containers:

```bash
docker compose --env-file .env.local up -d
```

Check the result:

```bash
docker compose ps
```

## Persistent data

PostgreSQL data is stored in a Docker named volume.

Do **not** run:

```bash
docker compose down -v
```

unless you intentionally want to remove the persistent volumes and delete the database data.

## Useful commands

View running containers:

```bash
docker compose ps
```

View all logs:

```bash
docker compose logs
```

Follow all logs:

```bash
docker compose logs -f
```

Restart the stack:

```bash
docker compose --env-file .env.local restart
```

Stop containers:

```bash
docker compose --env-file .env.local down
```
