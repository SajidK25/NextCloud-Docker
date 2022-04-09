## Nextcloud with Postgres database
This example defines one of the base setups for Nextcloud.

Project structure:
```
.
├── docker-compose.yaml
└── README.md
```

[_docker-compose.yaml_](docker-compose.yaml)
```
services:
  app:
    image: nextcloud:apache
    ports:
      - 80:80
    ...
  db:
    image: postgres:alpine
    ...
  redis:
    image: redis:alpine
    ...
```

When deploying this setup, docker-compose maps the nextcloud container port 8088 to
port 80 of the host as specified in the compose file.

## Deploy with docker-compose

```
$ docker$ compose up -d
```


## Expected result

Check containers are running and the port mapping:
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
9884a9cc0144        postgres:alpine     "docker-entrypoint.s…"   12 minutes ago      Up 12 minutes       5432/tcp             nextcloud-postgres_db_1
bae385bee48b        nextcloud:apache    "/entrypoint.sh apac…"   12 minutes ago      Up 12 minutes       0.0.0.0:8088->80/tcp   nextcloud-postgres_nc_1
bae385bee48b        redis:apache       "/entrypoint.sh apac…"   12 minutes ago      Up 12 minutes       0.0.0.0:8088->80/tcp   nextcloud-docker_redis_1
```

Navigate to `http://localhost:8088` in your web browser to access the installed
Nextcloud service.

![page](1_Create_admin_account.png)

Stop and remove the containers

```
$ docker-compose down
