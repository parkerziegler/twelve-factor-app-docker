## Scale Docker Horizontally with Nginx Load Balancing
Nginx can help us to load balance requests to our Node.js processes. The following `nginx.conf` file tells Nginx to listen at the root path to our server and then pass all requests through a proxy named app. Configuring the `upstream` property allows you to denote the servers you want to proxy requests to.

```conf
# this helps to tell nginx which server to proxy requests to
# nginx uses a round robin balancing method to balance requests
upstream app {
  server chicken:8000;
  server steak:8000;
}

# this helps tell nginx to listen to the root path
# and pass all requests to a proxy called app
server {
  location / {
    proxy_pass http://app;
  }
}
```

In your Dockerfile, you can configure a copy of your `nginx.conf` to make sure it's available when the container is built and run.

```
FROM nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf
```

Then start up the Docker container.

```sh
docker build -t app-nginx .
# Use --link to make servers accessible to container
docker run -d -p 8080:80 --link chicken --link steak app-nginx
```