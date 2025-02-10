# Resource Requirements and Limits

In Kubernetes, you can specify resource requests and limits for containers to ensure they have the necessary resources to run efficiently. This helps in better resource management and ensures that no single container monopolizes the resources.

## Resource Requests

Resource requests are the minimum amount of CPU and memory that a container needs. Kubernetes uses these values to schedule the container on a node with sufficient resources.

Example:
```yaml
resources:
    requests:
        memory: "64Mi"
        cpu: "250m"
```

## Resource Limits

Resource limits are the maximum amount of CPU and memory that a container can use. If the container tries to exceed these limits, it may be throttled or terminated.

Example:
```yaml
resources:
    limits:
        memory: "128Mi"
        cpu: "500m"
```

## Full Example

Here is a full example of a pod specification with resource requests and limits:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: resource-demo
spec:
    containers:
    - name: demo-container
        image: nginx
        resources:
            requests:
                memory: "64Mi"
                cpu: "250m"
            limits:
                memory: "128Mi"
                cpu: "500m"
```

By setting resource requests and limits, you can ensure that your applications run smoothly and efficiently within the Kubernetes cluster.

## Handling Resource Scenarios

Kubernetes handles different scenarios based on the resource requests and limits set for containers:

1. **Underutilization**: If a container uses fewer resources than requested, the unused resources are available for other containers on the same node.
2. **Exact Utilization**: If a container uses exactly the requested resources, it runs smoothly without any throttling.
3. **Overutilization**: If a container tries to use more resources than requested but within the limits, it may be throttled to stay within the limits.
4. **Exceeding Limits**: If a container exceeds its resource limits, it may be terminated or restarted based on the policy defined.

By understanding these scenarios, you can better manage your Kubernetes cluster and ensure optimal performance for your applications.

## Pod Termination Decisions

When Kubernetes needs to terminate pods, it follows a specific order of eviction to maintain cluster stability:

1. **Priority**: Pods with lower priority are terminated before those with higher priority.
2. **Quality of Service (QoS) Class**: Pods are terminated based on their QoS class in the following order: BestEffort, Burstable, and Guaranteed.
3. **Age**: Among pods with the same priority and QoS class, the oldest pods are terminated first.

By following these rules, Kubernetes ensures that critical applications remain running while less critical ones are terminated during resource constraints.


## Resources

- [Conceptual video](https://www.youtube.com/watch?v=xjpHggHKm78)
- [Resource and limits - video](https://www.youtube.com/watch?v=Q-mk6EZVX_Q)
