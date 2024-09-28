### NODE IMAGES FOR PODS ![4 Pods inside a Node and Each Pod Has Couple of Database Volume and containers.](https://miro.medium.com/v2/resize:fit:700/1*YlHaa7bw7AvVxHWypIm7oA.png)

4 Pods inside a Node and each Pod has a couple of database volumes and containers.

# Node and Pod:

- **Node** is a simple server in a physical or virtual machine.
- Inside a Node we can have multiple **Pods**, also the Pod is the smallest unit in Kubernetes.
- The Pod is an abstraction over a **container**. The Pod provides a running environment on top of the container, for _example, a docker container runs inside a Pod._
- Each Pod has an internal IP address through which they can communicate with each other, For e_xample, one Pod can have an application and the other one can have a database and they can communicate with each other._
- We can run multiple **applications** inside a Pod, in the image above there is a Pod with `IP: 10.10.10.4` contains a couple of **Database** volumes running and a few containerized apps running.
- **Pod components in Kubernetes can die** easily maybe because Pod crash, application crash, or the Node process ran out of resources the Pod will die, and when the Pod dies a new one will get created in its place with a new IP address.

> Now, the problem comes in a case when a database running in a Pod dies and when new one gets created it assigned with a new IP address and your application which was pointing to an old IP address will loose a connection. And every time we need to adjust IP address and that is why another component used called **Service and Ingress**.

# Service and Ingress

**Service** is basically a static IP address or permanent IP address that can be attached to each Pod. Example: Pod with an application have its own service and Pod with a database has its own service. So even if a Pod dies the service with an IP address will stay. So we don’t have to change the IP address pointing to the database in an application when Pod dies.

Now, we want our application to be accessible from a browser, and for this, we need to create an external service, so an **external service is a service that opens a communication from external sources**.

Also, we want our database to be open for public requests, for that we create an **internal service**. Here is an example of service:  
`HTTP protocol` `://` `Node IP address` `:` `Port number of the Service`

- The URL for the application, external service is  
    `http://app-service-ip:port` (`http://10.10.10.1:8080`)
- The URL for the database, internal service is  
    `http://db-service-ip:port` (`http://10.10.10.1:8081`)

But for public access, we want our URL with a secure protocol (`https`) and `domain name` like `**https://my-app-domain.com**` and for that, we use another component in Kubernetes called **Ingress.**

> So, when we call a domain first **request goes to Ingress** **and it forward then to the Service.**

> **All together in a single diagram**:
> 
> In left most — Pod communication is being done by IP, then in center — we used services and at last — we used Ingress.

![[Pasted image 20230618205830.png|850]]

# ConfigMap and Secret:

To allow Pods communication between application and database we need to configure URLs or endpoint IP.

Now, where do we configure these?  
- In application properties file or  
- External environmental variable but usually it’s inside of the built image of the application.

Next, when we change these URL configurations we need to `**re-build our application**` `**push it to the repository** then **we need to pull that new image in Pod**` and `**restart the whole server**`. And for this purpose Kubernetes has a component called **ConfigMap**.

## **ConfigMap**

**ConfigMap allows external configuration of our application.** This configMap file contains the URLs of the application & database and we just need to connect this configMap to Pod and Pod will read the configuration.

ConfigMap file looks like this:  
`DB_URL = some-mongo-db-service-url`  
`DB_USERNAME = username`  
`DB_PASSWORD = password`  
`APP_URL = some-application-service-url`

> We just need to update ConfigMap file whenever we need a change in any URL, this way we don’t need to create new image and update the Pod.

But, putting `Username` and `Password` in ConfigMap is insecure. And for this purpose Kubernetes has another component called **Secret.**

## **Secret**

**The secret is used to store secret data not in plain text but in base 64 encoded format.** So secret component in Kubernetes is used to maintain things like Credentials. Just like ConfigMap, we need to connect Secret to Pod and Pod will read the configuration.

## Data Storage in Kubernetes

To keep the data persist for a long time we use another component called **Volumes.** It attaches Physical storage or hard drive to Pod.

> This hard drive could be in the same local machine where the Pod is running or it could be on a remote storage, outside of the Kubernetes cluster.

This way when the Pod or container is restarted all the data will be safe there. Kubernetes does not manage data persistence. That is why we keep the outside of the Kubernetes cluster.

Now, what happens when Pod dies because of an application crash, or I have to build a new container image because of this the application will be down and to avoid relying on just one Pod for the app and one pod for the database we need to replicate everything on multiple servers. So we would need another Node that uses the same service because the service has a static or permanent IP address with a DNS name. Services also work as Load balancers, they forward the request to another Pod when it's busy.

## Deployment and StatefulSet

### Development

**The deployment** component in Kubernetes *creates a blueprint for Pods to create a number of replicas of Pods we want to run*. We don’t create or replicate Pods we create a deployment and there we specify how many replicas we want where we can scale up and scale down a number of replicas of Pods.

> **Pod is a layer of abstraction over containers and Deployment is another layer of abstraction over Pods.**

![](https://miro.medium.com/v2/resize:fit:700/1*ydga8thF-Blaqh1H7PdGzw.png)

> We need a mechanism to manage which Pods is writing to a storage or which Pods are reading from the storage in order to avoid data inconsistencies and that mechanism is offered by another Kubernetes component called **StatefulSet**.

### StatefulSet

**StatefulSet** component is specially meant for applications like databases MySQL, MongoDB, elastic search or any other stateful applications or databases should be created using StatefulSet.

> ★ **Deployment** is used for StateLess Apps.  
> ★ **StatefulSet** is used for StateFul Apps or Databases.
> 
> Just like Deployment component a **StatefulSet component take care of replicating the Pods and scaling them up and down.** StatefulSet also **making sure that the reads and writes are synchronized to avoid database inconsistencies.**

Database applications are often hosted outside of the Kubernetes cluster because managing StatefulSet in Kubernetes is difficult. So most often Databases are kept outside and communicate with applications Pod.

![](https://miro.medium.com/v2/resize:fit:700/1*yZV4Bw34PAUzBtMrxy2UJg.png)



