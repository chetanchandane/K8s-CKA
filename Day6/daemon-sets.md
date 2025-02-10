# Daemon Sets

A DaemonSet ensures that all (or some) nodes run a copy of a pod. As nodes are added to the cluster, pods are added to them. As nodes are removed from the cluster, those pods are garbage collected. Deleting a DaemonSet will clean up the pods it created.

## Use Cases

- Running a cluster storage daemon on every node.
- Running a logs collection daemon on every node.
- Running a node monitoring daemon on every node.

## Creating a DaemonSet

Here is an example of a DaemonSet configuration:

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
    name: example-daemonset
    labels:
        app: example
spec:
    selector:
        matchLabels:
            app: example
    template:
        metadata:
            labels:
                app: example
        spec:
            containers:
            - name: example-container
                image: example-image
                resources:
                    limits:
                        memory: "200Mi"
                        cpu: "0.5"
```

## Managing DaemonSets

- **Create a DaemonSet**: `kubectl apply -f daemonset.yaml`
- **List DaemonSets**: `kubectl get daemonsets`
- **Describe a DaemonSet**: `kubectl describe daemonset <daemonset-name>`
- **Delete a DaemonSet**: `kubectl delete daemonset <daemonset-name>`

## Updating a DaemonSet

To update a DaemonSet, you can use `kubectl apply` with the updated configuration file. Kubernetes will ensure that the changes are applied to all nodes.

## Conclusion

DaemonSets are a powerful feature in Kubernetes that ensure a pod is running on all or selected nodes, making them ideal for cluster-wide services.


## Resources

- [Beginner friendly intro - DaemenSets(Video)](https://www.youtube.com/watch?v=49jgQADF638)
- [Basics Deamon Sets - video](https://www.youtube.com/watch?v=cdY67JqGbIc)