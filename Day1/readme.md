### Kubernetes Architecture and core concepts - Day 1

For day 1, we will focus more on the core concepts that are really crucial. 

**What is Kubernetes?**

Kubernetes (K8s) is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It follows a master-worker architecture, ensuring high availability, scalability, and fault tolerance.

A Kubernetes cluster consists of two main components:

Control Plane (Master Node) → Manages the cluster
Worker Nodes → Run containerized applications
Each component plays a critical role in orchestrating containers across multiple machines.

A cluster can have 100s of nodes. Nodes can have multiple pods or applications running. 

Let's see what these nodes are on a high level,

**What is a Node?**
A worker machine in Kubernetes and may be either a virtual or a physical machine, depending on the cluster. Each Node is managed by the control plane. A Node can have multiple pods, and the Kubernetes control plane automatically handles scheduling the pods across the Nodes in the cluster.

A node must have 3 processes installed on it:
1. A Container Run Time (CRT), for example Docker, rkt
2. Kubelet Service (Think of it as the captain of the worker nodes)
3. KubeProxy Service (responsible for communication across worker nodes)

As i mentioned there can be 100s of nodes in a cluster, then how do we manage or interact with these clusters? For that we have the controle plane which consists of one or more Master Nodes,

**Master Node**
A master node must have 4 process installed,
1. Api Server: a cluster gateway, which acknowledges the client requests, acting as an entry point into the cluster. API server validates the incoming requests and pass it on to the scheduler.
2. Kube-Scheduler: it is responsible for **DECIDING** which request is assigned to which pod in our cluster, this decision is made based on metrics such as for example, CPU, GPU, storage requirement. **(JUST decides!)**
3. Controller Manager: detects the pod health, if any pod crashed controller manager notifies the scheduler to spin that pod back up. There are many control managers, some of them are node manager, replication manager, we can also customize these managers based on our requirements.
4. ETCD: this is the cluster brain, a highly-available key-value store that is used to back-up all the cluster data in K8s.

Now, let's dive deeper, 

The **Kubernetes API Server** (`kube-apiserver`) is a critical component of the Kubernetes control plane. It serves as the front-end for Kubernetes and is responsible for handling all API requests from users, command-line tools (`kubectl`), and internal system components.

### **Kubernetes API Server**
1. **Authentication & Authorization**  
   - Verifies the identity of users and services using authentication methods like tokens, certificates, or OpenID Connect.
   - Determines access control using Role-Based Access Control (RBAC) or Attribute-Based Access Control (ABAC).

2. **Validation & Admission Control**  
   - Ensures that API requests follow Kubernetes schema and required fields.
   - Runs **admission controllers** to enforce policies before objects are stored in etcd.

3. **Data Persistence (etcd)**  
   - Acts as an interface between clients and **etcd**, the distributed key-value store used for maintaining cluster state.

4. **Serving the API Endpoints**  
   - Exposes the Kubernetes API endpoints (e.g., `/api`, `/apis`, `/healthz`).
   - Used by `kubectl`, the Kubernetes dashboard, and other system components.

5. **Handling Cluster Workloads**  
   - Schedules workloads by interacting with the **scheduler** and **controllers**.
   - Facilitates communication between controllers, services, and nodes.


**Kube API Server Configuration**
- Configured via the `kube-apiserver` binary.
- Common flags:
  ```bash
  kube-apiserver \
    --etcd-servers=http://127.0.0.1:2379 \
    --authorization-mode=RBAC \
    --enable-admission-plugins=NamespaceLifecycle,LimitRanger \
    --service-cluster-ip-range=10.96.0.0/12
  ```
- **High Availability**: Can be deployed as a set of replicas behind a load balancer.

**Useful API Endpoints**
- Get all available API resources:
  ```bash
  kubectl api-resources
  ```
- View API versions:
  ```bash
  kubectl api-versions
  ```
- Describe an API resource:
  ```bash
  kubectl explain pods
  ```







