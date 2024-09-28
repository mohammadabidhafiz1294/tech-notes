### IMAGES
![[Pasted image 20230620185845.png]]

## Introduction

Kubernetes has become increasingly popular as a reliable platform for running and managing applications. Kubernetes is a distributed systems platform and follows a client-server architecture. The master nodes function as the server side of Kubernetes, while the worker nodes connect to the master and run as clients.

Because of this division, Kubernetes components can be logically split up into these two categories:

- **Master components:** These components run on the master nodes of the cluster and form the control plane.
- **Node components:** Applications and services running on the worker nodes to receive instructions and run containers.

## Master Components

The master components are responsible for coordinating each node in the cluster, assigning work through pod scheduling, providing administrative interfaces to the cluster, and managing cluster-wide health and services.

Let’s take a look at what each of these services provide.

### Kube-api-server

The Kubernetes cluster is exposed via API and made available outside the cluster through the `kube-apiserver` component. The `kube-apiserver` is the only component that all other master and worker components can directly communicate directly with. Because of this, it serves as the interface for all cluster communications. All contact with the `kube-apiserver` uses a secure port.

The `kube-apiserver` is responsible for API validation for all resource creation requests before the resources are actually generated and saved to the data store. Users can communicate with the API server via the `kubectl` command line client or through REST API calls.

### Etcd

[etcd](https://github.com/etcd-io/etcd) is a distributed, highly-available key value data store that Kubernetes uses to store cluster configuration. It holds metadata and the desired and current state for all resources. Any object or resource that is created is saved in etcd.

etcd only communicates directly with the `kube-apiserver`, which serves as a mediator and validator for any interactions with the data store. All other components that need to check the metadata or state of resources stored in etcd must contact it through the `kube-apiserver`.

### Kube-controller-manager

Kubernetes manages applications through various controllers that operate on the general model of comparing the current status against a known spec. These controllers are control loops that continuously ensure that the current state of the cluster (the status) matches the desired state (the spec). They watch the current cluster state stored in etcd through the `kube-apiserver` and create, update, and delete resources as necessary. `kube-controller-manager` is shipped with many controllers such as:

- Node Lifecycle controller
- DaemonSet controller
- Deployment controller
- Namespace controller

You can specify which controllers you want to enable by passing the “controllers” flag during your cluster configuration.

### Kube-scheduler

Since Kubernetes is an orchestration framework, it has builtin logic for managing the scheduling of pods. The `kube-scheduler` component is responsible for this. Scheduling decision depends on a number of factors such as:

- Resource requirements of the app
- Resource availability across nodes
- Whether the pod spec has affinity labels requesting scheduling on particular nodes
- Whether the nodes have certain taints/tolerations preventing them from being included in the scheduling process

The `kube-scheduler` takes all of these considerations into account when scheduling new workloads.

### Cloud-controller-manager

The `cloud-controller-manager` is responsible for managing the controllers associated with builtin cloud providers. These controllers are dedicated to abstracting resources offered by individual cloud providers and mapping them to Kubernetes objects.

Cloud controllers are the main way that Kubernetes is able to offer a relatively standardized experience across many different cloud providers.

## Node Components

The node, or worker, machines are the primary workhorses of Kubernetes clusters. While the master components handle most of the organization and logic, the nodes are responsible for running containers, reporting health information back to the master servers, and managing access to the containers through network proxies.

### Kubelet

The `kubelet` component is an agent that runs on every worker node of the cluster. It is responsible for managing all containers running in every pod in the cluster. It does this by ensuring that the current state of containers in a pod matches the spec for that pod stored in etcd.

The `podspec` might be passed through the `kube-apiserver` to `kubelet` to run pods on that particular node, or might be passed as a file with the `kubectl` command line tool. The `kubelet` agent manages the container runtime to make sure the containers operating on the machine are in the desired state.

### Kube-proxy

The `kube-proxy` component is a network proxy that runs on each node. It is responsible for forwarding requests. The proxy is somewhat flexible and can handle simple or round robin TCP, UDP or SCTP forwarding. Each node interacts with the Kubernetes service through `kube-proxy`.

### Container Runtime

The container runtime is the component responsible for running the containers within pods. Rather than being a specific technology as with the other components, the container runtime in this instance is a descriptor for any container runtime that is capable of running containers with the appropriate features. Docker, CRI-O and containerd are some of the popular options for container runtimes.

The container runtime is the single component that actually operates containers on the host. All of the orchestration, coordination, and management features provided by the other components are meant to enhance the experience of working with the container runtime.

## Setting Up Your Cluster

Now that we’ve discussed the individual components operating on each of the machines in the cluster, we can talk about how you’d actually deploy these across a number of machines. Depending on your use case, you might want to set up your Kubernetes architecture based on any of the following topologies.

### Single Control-Plane Cluster

This is a suitable option when you are just starting to evaluate Kubernetes for your applications. In this type of cluster, only a single node in your cluster runs the master or control-plane components. This makes it easy to deploy and manage at the expense of redundancy and availability options. You can choose from the following options when it comes to your worker nodes:

#### Single Node Cluster

With this topology, all of the master and worker node components run on a single node. So a single machine will fulfill all of control-plane, etcd, and worker roles. Referring to this as a cluster is a bit of a stretch since it is only comprised of a single machine, but we’ll use that terminology to remain consistent.

This type of cluster is really only suitable for development work, running a few tests, or CI environments, and it should not be used in production. There are various products/tools such as K3s, RKE, Minikube, and Kubeadm that you can use to bring such a cluster up and running within minutes.

#### Single Master, Multiple Worker Nodes

This topology begins to spread out the roles by separating the worker node components from the master components. So all of the master components such as `kube-apiserver`, etcd, `kube-scheduler`, and the `controller-manager` will run on a single master node, as before. However, one or more dedicated nodes will be used to run the worker components.

![single node cluster](https://www.suse.com/c/rancher_blog/03-introduction-to-kubernetes-architecture/media/single_node_cluster.png)

This topology is more fault tolerant than a single node cluster, but is still not recommended for production. It can handle greater workloads, but it is still not fault tolerant when it comes to the `kube-apiserver` or etcd, without which the cluster can’t function.

### HA Cluster

Kubernetes is known for its resilience and reliability. This is possible by ensuring that the cluster does not have any single points of failure. Because of this, to have a highly available cluster, you need to have multiple master nodes. All master components such as the `kube-apiserver` and etcd can be scaled up to ensure high availability. Each of the etcd replicas copy the etcd data already stored for the cluster. This data redundancy ensures reliability and high availability. It is recommended to also have **master nodes spread across different regions or zones to handle zone failures**.

#### Etcd Quorum

Etcd stores the Kubernetes cluster configuration and state. In order to make your cluster HA, you need to have multiple nodes running etcd. Etcd needs the majority of nodes, called a quorum, to agree on cluster updates. For a cluster with `n` members, quorum is calculated as `(n/2)+1` (one greater than 50%). So to make your Kubernetes cluster tolerant to partial etcd failure, you will need etcd running on at least three nodes. In a 3 etcd node cluster, quorum will be 2, so it can still function if one of the nodes goes down. You can choose from among these topologies for an HA cluster based on how you set up etcd nodes:

#### Master Nodes with Co-Located Control-Plane and Etcd

#### Stacked Etcd Topology

In this type of cluster, a single control-plane master is scaled horizontally, so you have multiple master nodes. Each runs all of the master components including control-plane and etcd. The `kube-apiserver` on each node communicates with the local etcd member. To bring up HA cluster with this topology, you will need at least 3 master nodes and one or more dedicated worker nodes. This is also known as the **stacked etcd topology**.

##### External Etcd Cluster

In this topology, there are dedicated etcd nodes running separately from the nodes running the other control-plane components. The topology with co-located control plane and etcd components faces the risk of failed coupling. If one master node goes down, it is equivalent to losing a control-place node along with an etcd node. This can be avoided by decoupling the control-plane and etcd nodes.

In this topology, each control-plane node runs `kube-apiserver`, `kube-scheduler` and `kube-controller-manager`. Etcd members are run on separate nodes. Each etcd member can communicate with the apiserver on each of the control-plane nodes. With this design, even if a control plane node goes down, etcd nodes are not impacted and vice versa. This way the data redundancy isn’t impacted as much as it would in the first HA topology. The only downside to this architecture is that this setup requires twice the number of nodes.

## Conclusion

You should now have a decent understanding of some of the key processes running throughout a Kubernetes cluster as well as the various ways these can be arranged to achieve different levels of availability and scale. Though there are many different pieces to a full Kubernetes deployment, they all work together to provide high levels of functionality and offer a robust environment for container workloads.