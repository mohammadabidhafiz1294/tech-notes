## Introduction




## Config File Setup and Meaning





## If Traefik Setup Local Routing with Proxmox Service

If you want to use Traefik to route traffic within your local home network without the need for external access, you can configure Traefik to work in a "docker" provider mode and use Docker labels to define routers and services. Here's an example of a Traefik YAML configuration file for this scenario:

```yaml
# traefik.yaml  
global:
	checkNewVersion: true   
	sendAnonymousUsage: true 
providers: 
	docker:     
		endpoint: "unix:///var/run/docker.sock"  
		exposedByDefault: false 
entryPoints: 
	http: 
		address: ":80" 
http: 
	routers:  
		proxmox:    
			rule: "Host(`proxmox.local`)"     
			service: proxmox  
services:  
	proxmox:   
		loadBalancer:    
			servers:      
				- url: "http://proxmox:8006"``
```

In this configuration:

- The `providers` section specifies the Docker provider and sets the endpoint to the Docker socket (`unix:///var/run/docker.sock`). This allows Traefik to monitor and discover containers and services running in Docker.
- The `exposedByDefault` option is set to `false` to prevent Traefik from automatically exposing all services. We will rely on Docker labels to explicitly define the routers and services.
- The `entryPoints` section defines an entry point named "http" listening on port 80. This is the entry point through which Traefik will receive HTTP traffic.
- The `http` section includes a single router named `proxmox` for the `proxmox` service.
- The `proxmox` router is configured to match requests with the `proxmox.local` hostname.
- The `proxmox` service is configured to use the load balancer and points to the `proxmox` container using its Docker service name (`proxmox`). The container should be running on the same Docker network as Traefik.

To use this configuration, you would deploy your services as Docker containers on the same Docker network as Traefik and add appropriate Docker labels to the containers to define the routers and services. For example, for the `proxmox` service, you can add the following labels to the container:

``
```yaml
labels:  
- "traefik.enable=true"  
- "traefik.http.routers.proxmox.rule=Host(`proxmox.local`)" 
- "traefik.http.services.proxmox.loadbalancer.server.port=8006" 
```

Make sure to adjust the hostname, container names, and ports to match your specific setup.

Remember, this configuration is suitable for local network routing only and does not include external access from the internet.