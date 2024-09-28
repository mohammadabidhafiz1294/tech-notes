### ***Main Components of K8s***

Kubernetes (K8s) consists of several key components that work together to manage and orchestrate containerized applications. Here are the main components of a Kubernetes cluster:

1. Master Components:
    
    - API Server: Acts as the front-end for the Kubernetes control plane. It exposes the Kubernetes API, which clients use to interact with the cluster.
    - etcd: Distributed key-value store that stores the cluster's configuration data, state, and metadata. It provides reliable and consistent storage for Kubernetes.
    - Scheduler: Assigns pods (groups of containers) to nodes based on resource requirements, constraints, and other policies.
    - Controller Manager: Manages various controllers that handle different aspects of the cluster, such as replication, endpoints, service accounts, and more.
    
2. Node Components:
    
    - kubelet: Runs on each node and communicates with the master components. It manages the containers, starts and stops them, and reports their status to the master.
    - kube-proxy: Manages network connectivity between services within the cluster by setting up and maintaining network rules and forwarding traffic.
    - Container Runtime: The underlying software responsible for running containers, such as Docker, containerd, or CRI-O. It pulls container images and starts containers.
    
3. Add-Ons and Supporting Components:
    
    - DNS Service: Provides DNS-based service discovery and enables communication between services using their names.
    - Ingress Controller: Manages inbound network traffic to services within the cluster, typically by acting as a reverse proxy and applying routing rules.
    - Dashboard: A web-based graphical user interface (GUI) for managing and monitoring the Kubernetes cluster.
    - Metrics Server: Collects resource utilization data from nodes and pods and exposes it as metrics in the Kubernetes API.
    - Persistent Volumes: Abstraction layer that allows pods to request and use durable storage. It decouples storage from the lifecycle of pods.
    - Service Mesh (e.g., Istio): Provides advanced networking and observability capabilities, including traffic management, load balancing, and monitoring.
	

> These components work together to provide the core functionalities of Kubernetes, including container orchestration, scaling, automated deployment, service discovery, and load balancing. Each component has a specific role in managing the lifecycle of containers and ensuring the desired state of the cluster.

