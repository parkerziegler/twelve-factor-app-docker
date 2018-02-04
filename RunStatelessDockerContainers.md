## Run Stateless Docker Containers
Docker containers should be designed to be stateless – this means they can survive system reboots and container termination without the loss of data. Recall that a `Dockerfile` is used as our basic setup for Docker:

```
FROM parkerziegler/Documents/repos/docker-example
WORKDIR srv/
COPY . .
RUN mkdir uploads
RUN yarn
EXPOSE 8080
CMD node index.js
```

and that we use `docker-compose` to run our containers:

```yml
version: '3'
services:
  app:
      build: .
      ports:
        - 8080:8080
```

One issue with this setup is that Docker's local data storage system is ephemeral – if a container terminates, the data may be lost. This can be problematic if we need to restart our container or redeploy our app.

The easiest way to fix this problem is to set up a **persistent volume**. Persistent volumes map a host directory into a container directory, so even when the host dies the container directory will not. The directory will map back to a new host directory when the container restarts. To set this up, we can again use `docker-compose`.

```yml
version: '3'
services:
  app:
      build: .
      ports:
        - 8080:8080
  # map a local file directory to a container directory
  volumes:
    - appdata: /srv/uploads
# specify container directories here
volumes:
  appdata:
```

Other useful commands introduced in this lesson:

**To start containers with `docker-compose`**
```sh
docker-compose up
```

**To remove containers with `docker-compose`**:
```sh
docker-compose rm -f
```