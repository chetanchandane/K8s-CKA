# Pod Affinity

Pod affinity and anti-affinity allow you to constrain which nodes your pod is eligible to be scheduled based on the labels of other pods already running on the node rather than on the labels on nodes. This can be useful for ensuring that related pods are scheduled together or that certain pods are kept apart.

## Pod Affinity

Pod affinity is used to attract a pod to a set of nodes based on the labels of other pods running on those nodes. This can be specified using `requiredDuringSchedulingIgnoredDuringExecution` or `preferredDuringSchedulingIgnoredDuringExecution`.

### Example

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: pod-with-affinity
spec:
    affinity:
        podAffinity:
            requiredDuringSchedulingIgnoredDuringExecution:
                - labelSelector:
                        matchExpressions:
                            - key: security
                                operator: In
                                values:
                                    - S1
                    topologyKey: "kubernetes.io/hostname"
    containers:
        - name: nginx
            image: nginx
```

## Difference Between Pod Affinity and Node Affinity

Pod affinity and node affinity are both used to influence the scheduling of pods, but they operate on different criteria:

- **Pod Affinity**: This is used to schedule a pod based on the labels of other pods that are already running on the nodes. It helps in co-locating related pods on the same node or in the same topology domain.
- **Node Affinity**: This is used to schedule a pod based on the labels on the nodes themselves. It helps in placing pods on nodes that meet certain criteria, such as specific hardware or geographic location.

### Example of Node Affinity

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: pod-with-node-affinity
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
        - name: nginx
            image: nginx
```

## Resources

- [Pod affinity](https://www.youtube.com/watch?v=S0ICBR_l9Es)