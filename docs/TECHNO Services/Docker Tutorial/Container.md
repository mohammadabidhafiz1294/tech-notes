-------------
A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

--------------------

- Checking that the docker binary works
    ```
    $ sudo docker info 
    ```
	
	output arrives:
	
	Containers: 33 
    Running: 0 Paused: 0 Stopped: 33 
    Images: 217 
    Server Version: 1.12.0 
    Storage Driver: aufs 
    Root Dir: /var/lib/docker/aufs 
    Backing Filesystem: extfs 
    Dirs: 284 Dirperm1 
    Supported: false 
    Logging Driver: json-file 
    Cgroup Driver: cgroupfs . . . 
    Username: jamtur01 
    Registry: https://index.docker.io/v1/ 
    WARNING: No swap limit support Insecure Registries: 127.0.0.0/8  ```
  
- Creating and naming a container ahead:
 ```
 $ sudo docker run --name bob_the_container -i -t ubuntu /bin/bash 

```
	this command is open the terminal inside the container bash:
```
root@aa3f365f0f4e:/# exit  
```

- We can also attach the existing created container inside the container bash:
```
$ sudo docker attach bob_the_container
```

- Creating daemonized containers:
```
$ sudo docker run --name daemon_dave -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done" 
```
	this is the output :
```
1333bb1a66af402138485fe44a335b382c09a887aa9f95cb9725e309ce5b7db3
```
- Automatic container restarts  :
   If your container has stopped because of a failure you can configure Docker to restartitusingthe--restartflag.
 ```
 $ sudo docker run --restart=always --name daemon_alice -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
```

- Container Inspect : 
	```
	sudo docker inspect [docker_container_name] 	 
	```
	The docker inspect command will interrogate our container and return its configuration information, including names, commands, networking configuration, and awide variety of other useful data.

- 