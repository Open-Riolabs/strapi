# Strapi docker 

## Build development doker image

```sh
docker build --build-arg NODE_ENV=development -t strapi:latest -f Dockerfile-dev .
```

## Run with docker compose
```sh
docker compose up -d strapi
```

## Docker compose example

```yaml
services:
  strapi:
    container_name: strapi
    build: .env
    image: strapi:latest
    restart: unless-stopped
    env_file: .env
    environment:
      DATABASE_CLIENT: postgres
      DATABASE_HOST: <ip>
      DATABASE_PORT: <port>
      DATABASE_NAME: <db-name>
      DATABASE_USERNAME: <db-user>
      DATABASE_PASSWORD: <db-password>
      DATABASE_SSL: false
      JWT_SECRET: 
      ADMIN_JWT_SECRET: 
      APP_KEYS: 
      API_TOKEN_SALT: 
      NODE_ENV: development
      VITE_ALLOWED_HOSTS: <hostname>
    volumes:
      - /mnt/data/strapi/config:/opt/app/config                     
      - /mnt/data/strapi/src:/opt/app/src                           #Used to save change to db schema
      - /mnt/data/strapi/upload:/uploads:/opt/app/public/uploads
      - /mnt/data/strapi/migration:/opt/app/database/migrations/
    ports:
      - "1337:1337"
```