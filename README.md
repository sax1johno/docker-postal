## Docker container for [atech/postal](https://github.com/atech/postal)

### Docker Hub Daily Builds
Builds are done every 6 hours by [Codeship](http://codeship.com/)

| tag           | Status                                                                                                                                   | Docker Hub                                                    |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| latest        | ![Daily Build](https://app.codeship.com/projects/aef32ad0-1807-0135-b213-7e299b644564/status?branch=master)                              | [alinuxninja/postal:latest](https://hub.docker.com/r/alinuxninja/postal/) |

By default, docker-compose.yml uses Docker Hub for the image and does not do building, though it can be set to build from the included Dockerfile if needed.

### Instructions
Change configuration in docker-compose.yml to update passwords for MySQL/RabbitMQ. Note that both passwords in the `postal` service, `mysql` service and `rabbitmq` service have to be changed.

Then, begin by following the directions at https://github.com/atech/postal/wiki/Installation#initialize-database--assets.
Postal can be accessed by checking the section below. Note that `postal intialize-config` is already run for you, as the database parameters need to be configured to match the environment variables before the postal tool can be used.

After configuration is done, run the following to bring the container up.
```
docker-compose up -d
```
### Using the `postal` tool.
To use the `postal` tool, simply run
```
docker-compose run postal <parameter>
```
For example, the following command runs `postal initialize` inside the container.
```
docker-compose run postal initialize
```

### Migrations
See https://github.com/atech/postal/wiki/Upgrading. Note that building a new container (or pulling a new version from Docker Hub) will update the files in postal, so all you have to run is `postal upgrade` after building or retrieving the new container. Updating postal using its auto-update feature is highly not reccomended and likely does not work properly.

### Ports
Port mappings may change (as they have in the past). If SMTP/HTTP(s) is not working, verify that the mapped ports are correct.

### Anti-Spam / Antivirus
The initial design for the container was to be simple, minimal, and customizable, so Spamassassin and ClamAV are not included by default. Feel free to fork and add to the Dockerfile (though you must set docker-compose.yml to build from Dockerfile and not pull an image), or add them by linking additional containers.
