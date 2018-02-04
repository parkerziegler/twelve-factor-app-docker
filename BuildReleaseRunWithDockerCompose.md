## Build, Release, and Run Containers with `docker compose`
The `docker build` command will pull in your app dependencies and compile binaries and assets into a process that can be run as a tagged release.

```sh
docker build -t vendor-name/app-name:1.0 .
```

You can customize the build using a `docker-compose.yml` file. For example:

```yml
# Note that the image property below should reference the 
# tagged release just created in by running docker build
version: '3'
services:
  app:
    image: my-vendor/my-app:1.0
      env_file:
        - .env
      ports:
        - 8080:8080
```

Once you've saved this file, use version control to keep the file maintained. Make sure you have a `.dockerignore` when you commit as well that ignores both `.env` and `node_modules`. Then, after commit, tag using `git tag`.

To run the release, check out the tag `git checkout v1.0.0`. To push the release to production `docker-compose up -d app`. This will pull down any images not local to the machine, apply the compose config, and start the containers in daemon mode. Confirm the containers are running with `docker ps`.