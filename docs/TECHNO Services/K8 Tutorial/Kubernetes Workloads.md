
## Introduction

Kubernetes is all about managing your container infrastructure. After learning the basics of what Kubernetes can do, it’s important to know all the building blocks that will help you run your containers in the best manner possible. So let’s discuss “workloads” and some of the Kubernetes components that surround this concept.

So what exactly is a workload? In Kubernetes, there is no object, component, and any kind of construct called a “workload”. However, the term is often used as a general category for tasks and services you want running on your cluster. It might be synonymous with microservices, applications, containers, or processes. Workloads are often long-lived processes, but can also be short-lived on demand or batch jobs.

## Workload Building Blocks

Now that we have basic definition of a workload, let’s explore what Kubernetes offers to manage and configure your workloads. We’ll start with Pods and work our way to components that encapsulate Pods, such as ReplicaSets, Deployments, DaemonSets, and StatefulSets. We’ll then talk about peripheral components like Services, EndPoints, and Ingress.

### Pods

Pods are the most basic building block in Kubernetes when it comes to workloads. A Pod consists of one or more containers. The containers within a pod share networking and host storage, but are isolated in terms of [cgroups](https://documentation.suse.com/sles/html/SLES-all/cha-tuning-cgroups.html) and [kernel namespaces](https://www.suse.com/c/demystifying-containers-part-i-kernel-space/) ( not to confuse with [Kubernetes namespaces](https://www.suse.com/c/rancher_blog/introduction-to-kubernetes-namespaces/) ).

How many containers should you have in your Pod? There is no limit or restriction, but it’s generally a good practice to only have a single container in your pod when you are first getting started. As you’ll see later on, many Kubernetes constructs allow you to scale Pods, so the fewer containers you put in your Pods, the more granular control you have over scaling your infrastructure. As you advance your Kubernetes expertise, you can experiment with init and sidecar containers, but this is beyond the scope of this guide. In short, these containers assist the primary container without altering the main purpose of the Pod.

### ReplicaSets

ReplicaSets are the wrappers around Pods that simply let you manage the number of Pods you want running at a given time. Kubernetes claims high availability and fault tolerance, and having multiple pods running helps achieve this. The job of the ReplicaSet is to ensure Kubernetes is running the configured number of Pods.

It’s good to know that ReplicaSets exist and what they do, but you will rarely need to create or manage ReplicaSets directly. Deployments will manage ReplicaSets for you. You normally only need to deal with ReplicaSets when troubleshooting unexpected problems.

### Deployments

Deployments are one of the most frequently used and managed components in Kubernetes. The Deployment manages your ReplicaSet, which in turn manages the number of Pods that should be running in your desired state. However, it also manages a few more things for you such as updates, rollbacks, and scaling.

After you have deployed your Pod for the first time, there’s a good chance you are going to want to update it when you have a code fix or enhancement. Deployments can help manage this update and can even do a gradual rollout so that all of your Pods are not down at the same time. It will keep track of each update which will allow you to perform rollbacks. This can be very useful if something goes wrong with an update and you need to revert quickly.

You can also use Deployments to scale up or scale down the number of Pods you want to have running. Kubernetes also has a Horizontal Pod Autoscaler that can even do this automatically based on various criteria.

### DaemonSets

DaemonSets ensure that one Pod of a set is running on each node in your cluster. Generally you want Kubernetes Deployments to manage where and how many of your Pods run in your cluster, but there are some good use cases for DaemonSets. Some of these common use cases include monitoring, logging, virus scanning, and intrusion detection.

For example, you may have a Pod that collects system logs and ships them off to an aggregator. This is a great candidate for a DaemonSet if you want to collect the logs from all of the nodes in your cluster.

### StatefulSets

StatefulSets look quite a bit like Deployments, but are specialized for Pods that require persistent storage. They provide a more predictable naming convention for your Pods to help with service discovery and ultimately allow you to do clustering or replication between your Pods in a single StatefulSet. If you are running MySQL, PostgreSQL, MongoDB, Cassandra, or Etcd in your cluster, StatefulSets may be a good solution for managing these workloads.

### Services and EndPoints

With your Pods are running and being managed by Deployments, you’ll need a way for your Pods to talk with each other. You may have an e-commerce catalog that needs to talk to a shopping cart, order, and billing APIs. That’s were Services come to the rescue.

A Service allows you to have a listening port open on your cluster or nodes that will send traffic to your Pod. This also supports high availability and fault tolerance by distributing the traffic to your healthy Pods. Note, the word “healthy”. If your Pod is down and deemed as unhealthy, the Service will automatically stop sending it traffic.

Services manage another Kubernetes component called EndPoints to achieve this. As Pods are created, scaled up, scaled down, crash, and recover, the Service will add and remove EndPoints to these Pods. EndPoints are another component you don’t generally manipulate directly, but may have to inspect to troubleshoot a problem.

### Ingress

Ingress can be thought of as the glue between the outside world and your Services. It requires an ingress controller such as [Nginx](https://nginx.org/) or [Traefik](https://traefik.io/) to be deployed in your cluster. Ingress can provide you HTTP layer 7 traffic control, including load balancing and fan out, as well as SSL termination/offloading.

In terms of traffic control, you can fan out your requests based on host name or path. For example, requests coming to “/v1/catalog/” can go to your catalog Service, which ultimate routes to your catalog Pods and requests for “/v1/orders/” can be sent to your orders Service. While you don’t need Ingress for Pods to talk to each other, it’s key for allowing other users or services on the Internet to reach your Pods.

### Jobs and CronJobs

While the majority of workloads are long-lived microservices that you always want running, there is a significant use case for short-lived workloads. Kubernetes has a Job component that allows you to run a Pod with the expectation that it will terminate normally and gracefully in the near future. In the long-lived use case, Kubernetes will automatically restart a Pod that has terminated for any reason. Job-managed Pods may also get retried if they terminate abnormally, but will be marked as completed when they terminate normally.

CronJobs manage Jobs on a scheduled basis, following the same model as a Linux `crontab`. Using CronJobs, you can schedule a job to run once a day, a week, or a month. More advanced scheduling is possible and very similar to Linux `crontab`. Running database and file backups as well as other off-hours system maintenance are common uses cases for CronJobs.

## Conclusion

You should now have a much better understanding of the various Kubernetes components that allow you to create and manage workloads. Pods, Deployments, and Services are the most popular and are good candidates for a deeper dive. It will also be important to learn more about how networking and storage work in Kubernetes as well as general day-to-day operations of your cluster.