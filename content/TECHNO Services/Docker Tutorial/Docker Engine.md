### INTRODUCTION
Docker Engine is the core component of the Docker platform. It is a lightweight and powerful containerization technology that allows developers to easily create, deploy, and run applications in containers.

Here are some of the key features of Docker Engine:

1.  Containerization: Docker Engine enables containerization, which allows you to package an application with all of its dependencies into a single, portable unit that can run consistently across different environments. 

2.  Image management: Docker Engine provides tools for creating and managing Docker images, which are used to build containers. Docker images can be versioned, tagged, and stored in registries for easy sharing and distribution.
  
3.  Resource isolation: Docker Engine uses Linux kernel features such as namespaces and cgroups to provide resource isolation for containers. This means that each container has its own isolated environment for running applications, with its own filesystem, network interfaces, and processes.

4.  Networking: Docker Engine provides a flexible networking model that allows containers to communicate with each other and with the host system. Docker supports a range of networking options, including bridge networks, overlay networks, and host networks.  

5.  Orchestration: Docker Engine can be used with container orchestration tools like   Docker Swarm or Kubernetes to manage the deployment, scaling, and lifecycle of containerized applications across a cluster of machines.
  
6.  Extensibility: Docker Engine can be extended with plugins and third-party tools to add new functionality or integrate with other systems.
  
Overall, Docker Engine provides a powerful and flexible platform for containerization that enables developers to easily create and manage applications in containers.


### [[Docker Engine]] Components

The Docker Engine consists of three major components: the Docker daemon, the Docker CLI, and the Docker API.

1.  Docker daemon: The Docker daemon (also known as the Docker engine) is the core component of the Docker platform. It is responsible for managing Docker objects such as containers, images, volumes, and networks. It listens to the Docker API requests and performs actions based on those requests.  

2.  Docker CLI: The Docker CLI (Command Line Interface) is a command-line tool that allows users to interact with the Docker daemon and manage Docker objects. It is used to build, run, and manage Docker containers and images. 

3.  Docker API: The Docker API is a REST API that provides programmatic access to the Docker daemon. It can be used to automate Docker tasks, integrate Docker with other tools and platforms, and create custom Docker-based applications.
   
When you run a Docker container, the Docker client (which includes the Docker CLI) sends a request to the Docker daemon to start a new container. The daemon then creates a new container based on the specified image and runs it in an isolated environment. The Docker daemon manages the container's resources, such as its filesystem, networking, and processes.

The Docker CLI can be used to interact with the Docker daemon to manage containers, images, volumes, and networks. For example, you can use the `` docker run `` command to start a new container, the `` docker build `` command to build a new image, and the `docker stop` command to stop a running container.

### Docker API ( Called )

The Docker API provides programmatic access to the Docker daemon, allowing you to automate Docker tasks and integrate Docker with other tools and platforms. Here's a brief tutorial on how to use the Docker API:

1.  Enable the Docker API: By default, the Docker daemon does not expose its API over a network. You can enable the Docker API by configuring the daemon to listen on a network socket and setting appropriate authentication and authorization options. See the Docker documentation for details on how to do this.

2.  Choose a client library: There are many client libraries available for working with the Docker API in various programming languages, including Python, Java, Ruby, and Go. Choose a client library that works with your preferred language and programming environment.

3.  Authenticate with the Docker daemon: Before you can make API calls to the Docker daemon, you need to authenticate with it. This typically involves providing a username and password or a token. The exact authentication method depends on how you have configured the Docker daemon.

4.  Send API requests: You can use your chosen client library to send API requests to the Docker daemon. For example, you might use the `containers.create()` method to create a new container, the `containers.start()` method to start a container, or the `images.pull()` method to pull a Docker image from a registry.
 
 5.  Handle API responses: When you send an API request to the Docker daemon, it will respond with a JSON-formatted response. Your client library will typically handle parsing the response and providing a convenient object-oriented interface for working with the response data.  

Here's a simple example of using the Python `` docker `` client library to list all running containers:
```
import docker

client = docker.from_env()
containers = client.containers.list()
for container in containers:
    print(container.name)
```
	This code creates a Docker client object, retrieves a list of all running containers, 
	 and prints the name of each container.

Overall, the Docker API provides a powerful and flexible way to interact with the Docker daemon and automate Docker tasks.