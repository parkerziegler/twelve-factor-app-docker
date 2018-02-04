## Export Services with Docker Port Binding
By default, Docker locks down all ports (similar to a firewall). This means that if we attempt to run a simple server as an image (with `docker run -d <image>`) and then hit that server, we will get a `Connection refused` error. To fix this, we need to open specific ports on the container that we want to access. To do this:

```sh
# map host port to a container port and point at the
# image we want to use
docker run -d -p 8000:8000 my-image
```

We can also do this with good ol' `docker-compose.yml`:

```yml
version: '3'
services:
  app:
    build: .
    ports:
      - 8010:8000
```