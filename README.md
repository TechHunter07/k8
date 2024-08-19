<div style="background-color: #FF0000; padding: 10px; border-radius: 5px;">
  <h2>Kubernetes</h2>
</div>
<<p align="center">
  <img src="https://github.com/user-attachments/assets/0a1f25f7-9472-4855-be7b-f8e1f105af24" alt="docker" width="100" hspace="20">
  <img src="https://github.com/user-attachments/assets/d52a430b-d8a2-4ebf-9e9d-f35dccb1e4c8" alt="docker" width="100" hspace="20">
  <img src="https://github.com/user-attachments/assets/20573d70-0d83-4256-8625-c9ea8547ee96" alt="docker" width="100" hspace="20">
</p>

```plaintext
+-------------------------------------------------------------------+
|                         Kubernetes Cluster                        |
|                                                                   |
|  +------------------+          +------------------+               |
|  |                  |          |                  |               |
|  |   Master Node    |          |    Worker Node   |               |
|  |                  |          |                  |               |
|  |  +------------+  |          |  +------------+  |               |
|  |  |            |  |          |  |            |  |               |
|  |  | etcd       |  |          |  | Kubelet    |  |               |
|  |  +------------+  |          |  +------------+  |               |
|  |                  |          |                  |               |
|  |  +------------+  |          |  +------------+  |               |
|  |  |            |  |          |  |            |  |               |
|  |  | API Server |  |          |  | Kube-proxy |  |               |
|  |  +------------+  |          |  +------------+  |               |
|  |                  |          |                  |               |
|  |  +------------+  |          |  +------------+  |               |
|  |  |            |  |          |  |   Pod       |  |               |
|  |  | Controller |  |          |  |            |  |               |
|  |  +------------+  |          |  |  +--------+|  |               |
|  |                  |          |  |  |Container||  |               |
|  |  +------------+  |          |  |  +--------+|  |               |
|  |  |            |  |          |  |            |  |               |
|  |  | Scheduler  |  |          |  +------------+  |               |
|  |  +------------+  |          |                  |               |
|  |                  |          |                  |               |
|  +------------------+          +------------------+               |
|                                                                   |
+-------------------------------------------------------------------+

Explanation of Kubernetes Components
    **Master Node:**
        **etcd:**
            A distributed key-value store that Kubernetes uses to store all cluster data. It is the source of truth for the cluster's state.
        **API Server:**
            The front end for the Kubernetes control plane. It exposes the Kubernetes API and is the entry point for all REST commands used to control the cluster.
        **Controller Manager:**
            Runs controller processes that handle routine tasks in the cluster, such as managing node operations, endpoints, and replicas.
        **Scheduler:**
            Assigns workloads to specific nodes in the cluster based on resource availability and other constraints.

  **Worker Node:**
        **Kubelet:**
            An agent that runs on each node in the cluster. It ensures that containers are running in a Pod as expected.
        **Kube-proxy:**
            A network proxy that maintains network rules on each node. It enables communication between Pods within the cluster and external services.
        **Pods:**
            The smallest and simplest Kubernetes object. A Pod represents a single instance of a running process in the cluster and can contain one or more containers.

  **Containers:**
        **Container (within Pod):**
            Encapsulated environments where applications and their dependencies run. Each container in a Pod shares the same network namespace and storage.

**Diagram Explanation**
  **>>The Kubernetes cluster consists of one or more Master Nodes and multiple Worker Nodes.
    >>The Master Node is responsible for managing the cluster and making global decisions about its operation (e.g., scheduling).
    >>Each Worker Node hosts Pods, which run the actual application workloads.
    >>The API Server acts as the primary point of interaction with the cluster, enabling users and system components to communicate and manage the cluster's state.
    >>The Scheduler and Controller Manager are integral to ensuring that the desired state of the cluster matches the actual state.
    >>etcd stores the entire configuration and state of the cluster.
    >>Kubelet and Kube-proxy run on every Worker Node, ensuring that Pods are running and facilitating network communication.
    >>Containers within Pods are the units of execution, encapsulating the application and its dependencies.**



**Hierarchical Structure:
    Cluster
       >> Contains multiple Nodes
          >>  Each Node contains multiple Pods
              >>  Each Pod contains one or more Docker Containers
                  >>  Each Docker Container is instantiated from a Docker Image
                      >>  Each Docker Image is built from a Docker File**
 **Cluster
  ├── Node
  │    ├── Pod
  │    │    ├── Docker Container
  │    │    │    ├── Docker Image
  │    │    │    │    └── Docker File**


************************** **Basic Flow Chart to  in  K8** ***************************
Create Kubernetes Namespace
    |
    v
Command: kubectl create namespace <namespace-name>
    |
    v
Create ConfigMaps & Secrets (if needed)
    |
    v
Command: kubectl create configmap <configmap-name> --from-literal=<key>=<value> -n <namespace-name>
Command: kubectl create secret generic <secret-name> --from-literal=<key>=<value> -n <namespace-name>
    |
    v
Create Persistent Volumes & Claims (if needed)
    |
    v
Command: kubectl apply -f <persistent-volume-file>.yaml
Command: kubectl apply -f <persistent-volume-claim-file>.yaml
    |
    v
Create Kubernetes Deployment
    |
    v
Command: kubectl apply -f <deployment-file>.yaml
    |
    v
Create Kubernetes Service
    |
    v
Command: kubectl apply -f <service-file>.yaml
    |
    v
Verify Deployment
    |
    v
Command: kubectl get deployments -n <namespace-name>
Command: kubectl get pods -n <namespace-name>
Command: kubectl get svc -n <namespace-name>
    |
    v
Monitor & Scale (if needed)
    |
    v
Command: kubectl top pods -n <namespace-name>
Command: kubectl scale deployment <deployment-name> --replicas=<number> -n <namespace-name>
    |
    v
Update & Rollback (if needed)
    |
    v
Command: kubectl set image deployment/<deployment-name> <container-name>=<new-image> -n <namespace-name>
Command: kubectl rollout undo deployment/<deployment-name> -n <namespace-name>

************************** Basic Flow Chart to run an application [NGNIX] in  K8 ***************************
1. Create Dockerfile
       |
       v
   1.1. Add base image (NGINX)
   1.2. (Optional) Add custom configuration
   1.3. Set up port exposure and commands
       |
       v
2. Build Docker Image
       |
       v
   2.1. Use `docker build` command
   2.2. Tag the image appropriately
       |
       v
3. Test Docker Container (Optional)
       |
       v
   3.1. Use `docker run` to test locally
   3.2. Map ports for testing
       |
       v
4. Push Docker Image to Registry
       |
       v
   4.1. Tag the image for the registry
   4.2. Use `docker push` to upload
       |
       v
5. Create Kubernetes Namespace
       |
       v
   5.1. Use `kubectl create namespace`
       |
       v
6. Create Kubernetes Deployment
       |
       v
   6.1. Define YAML for deployment
   6.2. Set replicas and container spec
       |
       v
7. Deploy NGINX to Kubernetes
       |
       v
   7.1. Apply the deployment file using `kubectl apply`
       |
       v
8. Create Kubernetes Service
       |
       v
   8.1. Define YAML for service
   8.2. Set service type (ClusterIP, NodePort, LoadBalancer)
       |
       v
9. Deploy Service
       |
       v
   9.1. Apply the service file using `kubectl apply`
       |
       v
10. Verify Deployment
       |
       v
   10.1. Use `kubectl get deployments`, `kubectl get pods`, and `kubectl get svc`
   10.2. Check pod logs if needed using `kubectl logs`
       |
       v
11. Access NGINX
       |
       v
   11.1. Use `minikube service` (if using Minikube) or access via external IP for LoadBalancer
   11.2. Confirm NGINX is serving traffic

