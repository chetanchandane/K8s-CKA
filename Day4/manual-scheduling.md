# Manual Scheduling

Manual scheduling in Kubernetes allows you to assign a pod to a specific node without relying on the scheduler. This can be useful for debugging or testing purposes.

## Steps for Manual Scheduling

1. **Identify the Node**: Determine the node where you want to schedule the pod.
2. **Create a Pod Manifest**: Define the pod specification in a YAML file and specify the node name.
3. **Apply the Manifest**: Use `kubectl` to create the pod.

### Example

Here is an example of a pod manifest for manual scheduling:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: manually-scheduled-pod
spec:
    containers:
    - name: nginx
        image: nginx
    nodeName: <node-name>
```

Replace `<node-name>` with the name of the node where you want to schedule the pod.

### Commands

1. **Apply the Pod Manifest**:
     ```sh
     kubectl apply -f pod-manifest.yaml
     ```

2. **Verify the Pod**:
     ```sh
     kubectl get pods -o wide
     ```

This will show the node where the pod is running.

## Manual Scheduling of an Existing Pod

To manually schedule an already existing pod, you need to delete the pod and recreate it with the nodeName specified.

### Steps

1. **Identify the Pod**: Determine the name of the pod you want to reschedule.
2. **Delete the Pod**: Use `kubectl` to delete the pod.
3. **Create a New Pod Manifest**: Define the pod specification in a YAML file and specify the node name.
4. **Apply the Manifest**: Use `kubectl` to create the pod.

### Example

Here is an example of a pod manifest for rescheduling an existing pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: existing-pod
spec:
    containers:
    - name: nginx
        image: nginx
    nodeName: <node-name>
```

Replace `<node-name>` with the name of the node where you want to schedule the pod.

### Commands

1. **Delete the Existing Pod**:
     ```sh
     kubectl delete pod existing-pod
     ```

2. **Apply the New Pod Manifest**:
     ```sh
     kubectl apply -f new-pod-manifest.yaml
     ```

3. **Verify the Pod**:
     ```sh
     kubectl get pods -o wide
     ```

This will show the node where the pod is running.

## Binding API

Kubernetes provides a Binding API that allows you to bind a pod to a specific node programmatically. This can be useful for custom schedulers or advanced scheduling scenarios.

### Binding Object

The Binding object is used to bind a pod to a node. It is defined in the `v1` API group and requires the pod name and the target node name.

### Example

Here is an example of a Binding object in JSON format:

```json
{
    "apiVersion": "v1",
    "kind": "Binding",
    "metadata": {
        "name": "manually-scheduled-pod"
    },
    "target": {
        "apiVersion": "v1",
        "kind": "Node",
        "name": "<node-name>"
    }
}
```

Replace `<node-name>` with the name of the node where you want to schedule the pod.

### Commands

1. **Create the Binding**:
         ```sh
         kubectl create -f binding.json
         ```

2. **Verify the Pod**:
         ```sh
         kubectl get pods -o wide
         ```

This will show the node where the pod is running.

## Conclusion

Manual scheduling is a straightforward way to control pod placement in Kubernetes. It is useful for specific scenarios but should be used with caution in production environments. The Binding API provides an additional method for programmatically binding pods to nodes.