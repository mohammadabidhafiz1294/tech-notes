### SUMMARY

MicroK8s is a lightweight Kubernetes distribution provided by Canonical, the company behind Ubuntu. It is designed for easy installation and management of a single-node Kubernetes cluster on your local machine or development environment. Here are some key features of MicroK8s:

1. Lightweight and Fast:
    
    - MicroK8s has a small footprint and requires minimal system resources, making it suitable for running Kubernetes on low-resource machines.
    - It provides a fast and efficient way to set up a local Kubernetes environment.
2. Single-Node Kubernetes Cluster:
    
    - MicroK8s sets up a single-node Kubernetes cluster on your local machine, allowing you to test and develop applications in a Kubernetes environment.
    - It provides the core Kubernetes components, including the API server, scheduler, controller manager, etcd, and container runtime.
3. Fast Start-up and Updates:
    
    - MicroK8s offers rapid cluster startup and quick updates, enabling you to get up and running with Kubernetes in no time.
    - It leverages Snap package technology for easy installation, automatic updates, and rollback capabilities.
4. Multiple Add-Ons:
    
    - MicroK8s includes a range of pre-configured add-ons and extensions that can be easily enabled or disabled based on your needs.
    - Add-ons such as DNS, dashboard, storage, ingress, and metrics can be activated with a single command, providing additional functionality to your cluster.
5. Easy Integration with Other Tools:
    
    - MicroK8s integrates well with other tools and frameworks commonly used in the Kubernetes ecosystem.
    - It supports containerd as the default container runtime and can be easily integrated with popular tools like Helm, Istio, and Prometheus.
6. Multi-Node Clustering (Experimental):
    
    - MicroK8s also includes an experimental feature that allows you to create a multi-node cluster by joining multiple MicroK8s instances together.
    - This enables you to simulate a distributed Kubernetes environment on your local machine for testing and development purposes.

> 	MicroK8s provides a lightweight and convenient way to run a single-node Kubernetes cluster on your local machine. It is well-suited for local development, testing, learning Kubernetes concepts, and building applications that target Kubernetes environments. With its simplicity and ease of use, MicroK8s can be a valuable tool for developers and operators working with Kubernetes.



### Installation

1. **Install MicroK8s**
    
    MicroK8s will install a minimal, lightweight Kubernetes you can run and use on practically any machine. It can be installed with a snap:
    
   ```
   sudo snap install microk8s --classic --channel=1.27
   ```
    
    [More about setting the channel](https://microk8s.io/docs/setting-snap-channel)
    
2. **Join the group**
    
    MicroK8s creates a group to enable seamless usage of commands which require admin privilege. To add your current user to the group and gain access to the .kube caching directory, run the following two commands:  
      
    `sudo usermod -a -G microk8s $USER`  
    `sudo chown -f -R $USER ~/.kube`
    
    You will also need to re-enter the session for the group update to take place:
    
    `su - $USER`
    
3. **Check the status**
    
    MicroK8s has a built-in command to display its status. During installation you can use the **`--wait-ready`** flag to wait for the Kubernetes services to initialise:
    
    `microk8s status --wait-ready`
    
4. **Access Kubernetes**
    
    MicroK8s bundles its own version of **`kubectl`** for accessing Kubernetes. Use it to run commands to monitor and control your Kubernetes. For example, to view your node:  
      
    `microk8s kubectl get nodes`
    
    …or to see the running services:
    
    `microk8s kubectl get services`
    
    MicroK8s uses a namespaced kubectl command to prevent conflicts with any existing installs of kubectl. If you don’t have an existing install, it is easier to add an alias (append to **`~/.bash_aliases`**) like this:
    
    `alias kubectl='microk8s kubectl'`
    
5. **Deploy an app**
    
    Of course, Kubernetes is meant for deploying apps and services. You can use the **`kubectl`** command to do that as with any Kuberenetes. Try installing a demo app:  
    
    `microk8s kubectl create deployment nginx --image=nginx`
    
    It may take a minute or two to install, but you can check the status:
    
    `microk8s kubectl get pods`
    
6. **Use add-ons**
    
    MicroK8s uses the minimum of components for a pure, lightweight Kubernetes. However, plenty of extra features are available with a few keystrokes using “add-ons” - pre-packaged components that will provide extra capabilities for your Kubernetes, from simple DNS management to machine learning with Kubeflow!
    
    To start it is recommended to add DNS management to facilitate communication between services. For applications which need storage, the ‘hostpath-storage’ add-on provides directory space on the host. These are easy to set up:
    
    ```
    microk8s enable dns
    microk8s enable hostpath-storage
    ```
    
    [See the full list of addons](https://microk8s.io/docs/addons#heading--list)
    
7. **Starting and Stopping MicroK8s**
    
    MicroK8s will continue running until you decide to stop it. You can stop and start MicroK8s with these simple commands:
    
    `microk8s stop`
    
    … will stop MicroK8s and its services. You can start again any time by running:
    
    `microk8s start`
    
    Note that if you leave MicroK8s running, it will automatically restart after a reboot. If you don’t want this to happen, simply remember to run `microk8s stop` before you power down.