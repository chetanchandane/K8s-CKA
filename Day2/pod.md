# Kubernetes Pod

A Kubernetes Pod is the smallest and simplest Kubernetes object. It represents a single instance of a running process in your cluster.

## Key Concepts

- **Single Container Pods**: The most common type of Pod, which runs a single container.
- **Multi-Container Pods**: Pods that run multiple containers that need to work together.

## Pod Lifecycle

1. **Pending**: The Pod has been accepted by the Kubernetes system, but one or more of the container images have not been created.
2. **Running**: The Pod has been bound to a node, and all of the containers have been created.
3. **Succeeded**: All containers in the Pod have terminated successfully.
4. **Failed**: All containers in the Pod have terminated, and at least one container has terminated in failure.
5. **Unknown**: The state of the Pod could not be obtained.

## Example Pod Definition

[Example Pod Definition](./pod.yaml)

## Commands

- **Create a Pod**: `kubectl apply -f pod.yaml`
- **Get Pods**: `kubectl get pods`
- **Describe a Pod**: `kubectl describe pod mypod`
- **Delete a Pod**: `kubectl delete pod mypod`

## References

- [Kubernetes Documentation](https://kubernetes.io/docs/concepts/workloads/pods/)

## Replication Controller

A Replication Controller ensures that a specified number of pod replicas are running at any given time. If there are too many pods, the Replication Controller will terminate the extra pods. If there are too few, it will start more pods.

### Key Concepts

- **Desired State**: The number of pod replicas that should be running.
- **Current State**: The number of pod replicas that are currently running.
- **Labels**: Used to identify the pods that are managed by the Replication Controller.

### Example Replication Controller Definition

[Example Replication Controller Definition](./rc-definition.yaml)

### Commands

- **Create a Replication Controller**: `kubectl apply -f replication-controller.yaml`
- **Get Replication Controllers**: `kubectl get rc`
- **Describe a Replication Controller**: `kubectl describe rc my-replication-controller`
- **Delete a Replication Controller**: `kubectl delete rc my-replication-controller`

### References

- [Kubernetes Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/)