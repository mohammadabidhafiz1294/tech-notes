### INTRODUCTION

A Docker volume is a persistent data storage mechanism that can be used to store and manage data outside of a Docker container. Volumes can be used to share data between containers or between a container and the host system.

When a Docker container is created, it can be configured to use a volume, which will be mounted inside the container as a directory. The data stored in the volume will persist even if the container is deleted, allowing for persistent data storage that is decoupled from the container.

Docker volumes can be used to store a variety of data, including application data, configuration files, and logs. Volumes can also be managed and inspected using the Docker CLI, making it easy to manage and monitor data storage across multiple containers.

- Volumes can be created using the command, 
```
docker volume create 
```
which creates a new named volume that can be referenced by other Docker containers.
- Volumes can also be created using the ```
```
docker run 
```

command with the ***-v*** option, which creates a new anonymous volume that is deleted when the container is deleted.

### Docker Volume List CMD
- To list the Docker volumes on your system, you can use the ***docker volume ls*** command. This command will display a list of all the volumes that are currently available on your Docker host.

  Output list like:

```
DRIVER              VOLUME NAME
local               myapp_data
local               postgres_data
```

### Docker Volume Inspect
You can also use the `docker volume inspect` command to get more detailed information about a specific volume, such as its mount point and other configuration options:

```
docker volume inspect myapp_data

```
This will output the JSON-formatted configuration information for the ***myapp_data*** volume.

