## Ensure Containers Run with High-Availability
You can filter the list of currently running containers using:
> docker ps -a -f naeme=image_name

You can restart the container whenever it exits to ensure it is always running. Use the following command:
> docker run --restart always

You can also achieve this using `docker-compose` with a `docker-compose.yml` file.

```yml
version: '3',
services:
  helloworld:
    image: helloworld
    restart: always
```

Now to scale the app by running multiple instances of an image:
> docker-compose up --scale helloworld=3

Three instances of `helloworld` are now running, each of which always restarts on exit!