### **Kube Scheduler - High-Level Overview**

The **Kubernetes Scheduler (`kube-scheduler`)** is a critical component of the **Kubernetes control plane** responsible for assigning **Pods to Nodes** based on resource availability and constraints. It ensures that workloads are distributed efficiently across the cluster.

---

### **How the Kube Scheduler Works**
The scheduling process follows these key steps:

1. **Watch for Unscheduled Pods**  
   - The scheduler continuously watches the API server for Pods **without a Node assignment**.

2. **Filter Nodes (Node Filtering / Predicate Checks)**  
   - The scheduler first eliminates **unsuitable nodes** based on:
     - **Resource Requirements** (CPU, Memory, Disk)
     - **Taints & Tolerations** (e.g., avoid scheduling workloads on specialized nodes)
     - **Affinity & Anti-Affinity Rules** (ensuring certain pods are placed together or apart)
     - **Node Selectors & Labels** (e.g., selecting nodes with specific characteristics)
     - **Node Readiness** (ensures the node is healthy and running)

3. **Score Nodes (Scoring & Prioritization)**  
   - The scheduler **ranks** the remaining nodes using a scoring algorithm, considering:
     - **Least loaded node** (balancing CPU, Memory)
     - **Topology Awareness** (spread across regions/zones)
     - **Custom Scheduling Policies** (e.g., preferring GPUs for ML workloads)

4. **Assign a Node & Bind the Pod**  
   - The highest-scoring node is **selected**.
   - The scheduler **binds the Pod to the chosen Node** by updating the API server.

5. **Kubelet Pulls & Runs the Pod**  
   - The **Kubelet on the assigned Node** then pulls the container image and runs the Pod.

---

### **Kube Scheduler Features**
- **Default Scheduling** → Uses built-in algorithms for scheduling.
- **Custom Schedulers** → Users can define their own scheduler.
- **Pod Affinity/Anti-Affinity** → Ensures Pods are co-located or spread across Nodes.
- **Taints & Tolerations** → Controls which workloads can be scheduled on specific nodes.
- **Priority & Preemption** → Ensures higher-priority workloads get resources first.

---

### **Key Use Cases**
- **Load Balancing** → Ensures even workload distribution.
- **High Availability** → Distributes workloads across zones/regions.
- **Optimized Resource Utilization** → Assigns Pods to nodes with sufficient resources.
- **Multi-Tenancy Support** → Enables workload isolation based on labels/affinity rules.

---


hard and soft constraints - https://www.youtube.com/watch?v=rDCWxkvPlAw
working of scheduler - https://www.youtube.com/watch?v=E3ExWruji7g