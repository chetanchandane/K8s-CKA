# Node Selectors in Kubernetes

Node selectors are a simple way to constrain pods to nodes with specific labels. They allow you to ensure that certain pods only run on nodes that meet specific criteria.

## How to Use Node Selectors

To use a node selector, you need to add a `nodeSelector` field to your pod specification. Here is an example:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: my-pod
spec:
    containers:
    - name: my-container
        image: nginx
    nodeSelector:
        disktype: ssd
```

In this example, the pod will only be scheduled on nodes that have a label `disktype=ssd`.

## Adding Labels to Nodes

Before you can use a node selector, you need to label your nodes. You can add a label to a node using the following command:

```sh
kubectl label nodes <node-name> disktype=ssd
```

Replace `<node-name>` with the name of your node.

## Example

1. Label a node:

        ```sh
        kubectl label nodes node1 disktype=ssd
        ```

2. Create a pod with a node selector:

        ```yaml
        apiVersion: v1
        kind: Pod
        metadata:
            name: my-pod
        spec:
            containers:
            - name: my-container
                image: nginx
            nodeSelector:
                disktype: ssd
        ```

3. Apply the pod configuration:

        ```sh
        kubectl apply -f my-pod.yaml
        ```

The pod will be scheduled on `node1` because it has the `disktype=ssd` label.

## Limitations of Node Selectors

While node selectors are useful, they have some limitations:

1. **Static Binding**: Node selectors provide a static binding between pods and nodes. If the labeled node becomes unavailable, the pod will not be rescheduled to another node automatically.
2. **Limited Expressiveness**: Node selectors only support equality-based requirements. You cannot use more complex expressions like inequalities or set-based requirements.
3. **No Weighting**: Node selectors do not support prioritization or weighting. All nodes with the specified label are considered equally suitable.
4. **Manual Labeling**: You need to manually label nodes, which can be error-prone and requires additional management effort.

## Conclusion

Node selectors are a straightforward way to control which nodes your pods are scheduled on. By using labels and node selectors, you can ensure that your workloads run on the appropriate nodes in your Kubernetes cluster.

For more advanced scheduling requirements, consider using node affinity or taints and tolerations.


## Resources

- [TroubleShooting walkthrough](https://www.youtube.com/watch?v=O61HDmGUBJM)