### Introduction

Portainer is an open-source management UI for Docker, Kubernetes, and Swarm. It allows users to manage their containerized applications and infrastructure through an easy-to-use web interface. Portainer supports multiple platforms, including Windows, Linux, and macOS, and can be installed as a standalone container or a Docker-compose stack. The platform provides users with a range of features, including container management, image management, network management, volume management, and user management. It also offers a RESTful API, which allows developers to automate and integrate their container workflows. Portainer is available in both free and paid versions, with the paid version offering additional features and support.

### Installation

To install Portainer on a Linux Docker Engine, you can use the following steps:
1. Pull the Portainer image from Docker Hub:

 ```
 docker pull portainer/portainer-ce
```
2. Create a volume to persist Portainer data: 
```
docker volume create portainer_data
```
3. Start the Portainer container using the `docker run` command:
```
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```
~ This command will start a Portainer container with the following options:
-   `-d`: Run the container in detached mode.
-  `-p 8000:8000 -p 9000:9000`: Map the container's ports 8000 and 9000 to the same ports on the host machine.
-   `--name=portainer`: Name the container "portainer".
-   `--restart=always`: Automatically restart the container if it crashes or is stopped.
-   `-v /var/run/docker.sock:/var/run/docker.sock`: Mount the Docker engine's Unix socket file into the container so that Portainer can communicate with the Docker engine.
-   `-v portainer_data:/data`: Mount the `portainer_data` volume we created earlier into the container.
	_NOTE_: Once the Portainer container is running, you can access the Portainer web interface by visiting `http://<your-server-ip>:9000` in a web browser. From there, you can create a new administrator account and start managing your Docker environment.

### Portainer-ce Vs Portainer

`portainer-ce` and `portainer` are two different Docker images for Portainer, which provide different versions of the software.

`portainer-ce` is the Community Edition of Portainer, which is an open-source and free version of the software. It provides basic container management features, including container creation, deletion, and deployment. It also includes features like container and image management, user management, and basic resource monitoring.

`portainer` is the official Portainer Docker Hub repository, which provides a range of images for different versions of Portainer, including both the Community Edition and the Enterprise Edition. This repository also includes images for different architectures, like ARM and PowerPC.

When you run `docker pull portainer/portainer-ce`, you are pulling the latest version of the Community Edition of Portainer from the official Docker Hub repository. When you run `docker pull portainer/enterprise`, you are pulling the latest version of the Enterprise Edition of Portainer from the same repository.

Both `portainer-ce` and `portainer/` can be used to deploy and manage Portainer on Docker, but they provide different feature sets and support different versions of the software. You should choose the appropriate image based on your specific needs and requirements.


## Uninstall

To uninstall Portainer from an Ubuntu server, you can follow these steps:

1. Stop the Portainer container:
    
    Use the `docker stop` command followed by the container name or ID to stop the Portainer container. For example:
    
   
    `docker stop portainer`
    
2. Remove the Portainer container:
    
    Use the `docker rm` command followed by the container name or ID to remove the Portainer container. For example:
    
	 `docker rm portainer`
    
3. Remove the Portainer image:
    
    Use the `docker rmi` command followed by the image name or ID to remove the Portainer image. For example:
    
	`docker rmi portainer/portainer-ce`
    
    If you pulled a specific version of the Portainer image, specify the version tag along with the image name, like `portainer/portainer-ce:tag`.
    
4. Remove the Portainer data volume (optional):
    
    If you created a data volume specifically for Portainer, you can remove it using the `docker volume rm` command followed by the volume name. For example:
	
	 `docker volume rm portainer_data`
    
5. Verify the removal (optional):
    
    You can use the `docker ps -a` command to list all containers and verify that the Portainer container has been removed. Similarly, you can use the `docker images` command to verify that the Portainer image has been removed.
    

By following these steps, you should be able to successfully uninstall Portainer from your Ubuntu server.