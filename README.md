# Week1

## Docker + Postgres

**Note:** The following can be executed using GitHub Codespaces. The commands assume that GitHub Codespaces is used and accessed from your local VS Code.

### Running Postgres and pgAdmin together

Create a network

```bash
docker network create pg-network
```

Then

```bash
docker volume create --name dtc_postgres_volume_local -d local
```

Run Postgres 

```bash
docker run -it \
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v dtc_postgres_volume_local:/var/lib/postgresql/data \
  -p 5432:5432 \
  --network=pg-network \
  --name pg-database \
  postgres:13
```

Run pgAdmin

```bash
docker run -it \
  -e PGADMIN_DEFAULT_EMAIL="admin@admin.com" \
  -e PGADMIN_DEFAULT_PASSWORD="root" \
  -p 8080:80 \
  --network=pg-network \
  --name pgadmin \
  dpage/pgadmin4
```
