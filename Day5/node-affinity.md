# Node Affinity

Node affinity is a feature in Kubernetes that allows you to constrain which nodes your pod is eligible to be scheduled based on labels on the nodes. It is similar to nodeSelector but offers more expressive rules.

## Types of Node Affinity

There are two types of node affinity:

1. **RequiredDuringSchedulingIgnoredDuringExecution**: The scheduler will not schedule the pod unless the rule is met. However, if the rule is no longer met at some point in the future, the pod will not be evicted.
2. **PreferredDuringSchedulingIgnoredDuringExecution**: The scheduler will try to enforce the rule, but it is not mandatory. If the rule is not met, the pod can still be scheduled.

## Example

Here is an example of a pod with node affinity:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: my-pod
spec:
    affinity:
        nodeAffinity:
            requiredDuringSchedulingIgnoredDuringExecution:
                nodeSelectorTerms:
                - matchExpressions:
                    - key: disktype
                        operator: In
                        values:
                        - ssd
    containers:
    - name: my-container
        image: nginx
```

In this example, the pod will only be scheduled on nodes that have a label `disktype` with the value `ssd`.

## Conclusion

Node affinity is a powerful feature that allows you to control the scheduling of your pods based on node labels. It provides more flexibility than nodeSelector and can help ensure that your pods are running on the most appropriate nodes.

## Resources

- [Kubernetes documentation on node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity).
- [Node Affinity](https://www.youtube.com/watch?v=6ZHjqpn9dck)
- [TroubleShooting walkthrough - (Time Stamp-23:00)](https://www.youtube.com/watch?v=O61HDmGUBJM)