# Taints and Tolerations

## Taints

Taints are applied to nodes and allow a node to repel a set of pods. This ensures that pods are not scheduled onto inappropriate nodes. Taints are configured using the `kubectl taint` command.

### Example

```sh
kubectl taint nodes <node-name> key=value:taint-effect
```
## Removing Taints

To remove a taint from a node, you can use the `kubectl taint` command with a minus sign (`-`) at the end of the taint.

### Example

```sh
kubectl taint nodes <node-name> key:taint-effect-
```
## Tolerations

Tolerations are applied to pods and allow them to be scheduled onto nodes with matching taints. Tolerations are specified in the pod specification.

### Example

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: my-pod
spec:
    tolerations:
    - key: "key"
      operator: "Equal"
      value: "value"
      effect: "NoSchedule"
```

## Analogy

Think of taints and tolerations like a bug landing on a human. Imagine a person has a special lotion (taint) that repels bugs. This lotion ensures that bugs do not land on the person. However, some bugs have developed a resistance (toleration) to the lotion and can still land on the person despite the repellent. In Kubernetes, taints work like the lotion to repel certain pods from nodes, while tolerations allow specific pods to resist the taint and be scheduled on those nodes.

## Checking Taints on All Nodes

To check the taints applied to all nodes in your Kubernetes cluster, you can use the following command:

```sh
kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, taints: .spec.taints}'
```

This command retrieves the list of nodes in JSON format and uses `jq` to filter and display the node names along with their taints.

## Checking Taints on a Specified Node

To check the taints applied to a specific node in your Kubernetes cluster, you can use the following command:

```sh
kubectl describe node <node-name> | grep -i taints
```

This command describes the specified node and filters the output to display the taints applied to that node.

## Resource
 
- [What are Taint and Toleration](https://www.youtube.com/watch?v=-L1Mewq0nfA) 
- [TroubleShooting walkthrough - (Time Stamp-31:10)](https://www.youtube.com/watch?v=O61HDmGUBJM)