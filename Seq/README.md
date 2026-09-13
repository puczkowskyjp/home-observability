## Project Startup

```bash
docker compose --env-file .env.local up -d
```


# See what's running

```bash
docker compose ps
```

# View logs
```bash
docker compose logs -f seq
```

## Stop Project

```bash
docker compose --env-file .env.local down
```

### Or if you want to delete volumes
```bash
docker compose --env-file .env.local down -v
```