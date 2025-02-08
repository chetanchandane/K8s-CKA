# Pod Anti-Affinity

Pod anti-affinity is a Kubernetes feature that allows you to constrain which nodes your pod is eligible to be scheduled based on the labels of other pods already running on the nodes. This can help improve the availability and resilience of your application by ensuring that certain pods do not co-locate on the same node.

## Example

Here is an example of how to configure pod anti-affinity in a Kubernetes manifest:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
    name: example-deployment
spec:
    replicas: 3
    selector:
        matchLabels:
            app: example
    template:
        metadata:
            labels:
                app: example
        spec:
            affinity:
                podAntiAffinity:
                    requiredDuringSchedulingIgnoredDuringExecution:
                        - labelSelector:
                                matchExpressions:
                                    - key: app
                                        operator: In
                                        values:
                                            - example
                            topologyKey: "kubernetes.io/hostname"
            containers:
                - name: example-container
                    image: nginx
```

In this example, the `podAntiAffinity` rule ensures that the pods with the label `app: example` are not scheduled on the same node.

## Key Fields

- `requiredDuringSchedulingIgnoredDuringExecution`: This field specifies that the rule must be met for a pod to be scheduled.
- `labelSelector`: Defines the labels that the anti-affinity rule applies to.
- `topologyKey`: Specifies the topology domain, such as `kubernetes.io/hostname`, to which the anti-affinity rule applies.

## Use Cases

- **High Availability**: Distribute pods across different nodes to avoid a single point of failure.
- **Resource Management**: Prevent resource contention by ensuring that certain pods do not run on the same node.

## Resources

- [Kubernetes documentation on Pod Anti-Affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity).
- [Pod anti affinity]()
