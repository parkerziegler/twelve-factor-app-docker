## Run Consistent Dev, Stage & Prod Docker
Docker makes it pretty simple to run consistent dev, stage, and prod environments. Our `docker-compose.yml` file defines all the app services (and versions of those services) we want to use across environments, guaranteeing parity. For example, we could use the following `docker-compose.yml` in all three environments.

```yml
version: '3'
services:
  app:
    build: .
    image: helloworld
    env_file:
      .env
```

Third party backing services are typically set using `env` variables. This allows the same `docker-compose.yml` file to point at different services depending on local `env` variables alone.