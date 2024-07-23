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

