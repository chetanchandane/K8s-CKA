# Static Pods

Static Pods are managed directly by the kubelet daemon on a specific node, without the API server observing them. They are mainly used in scenarios where the API server is not available, such as during the initial setup of a Kubernetes cluster.

## Creating Static Pods

To create a static pod, you need to place a pod manifest file in a specific directory on the node. The kubelet watches this directory and automatically creates/deletes the static pods as needed.

### Example

1. **Create a Pod Manifest File**

    Create a YAML file for your static pod, for example, `nginx-static-pod.yaml`:

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: nginx
      namespace: default
    spec:
      containers:
      - name: nginx
         image: nginx:latest
         ports:
         - containerPort: 80
    ```

2. **Place the Manifest File**

    Copy the `nginx-static-pod.yaml` file to the static pod directory on your node. The default directory is `/etc/kubernetes/manifests`:

    ```sh
    sudo cp nginx-static-pod.yaml /etc/kubernetes/manifests/
    ```

3. **Verify the Static Pod**

    Check if the static pod is running:

    ```sh
    kubectl get pods -o wide
    ```

## Managing Static Pods

- **Updating a Static Pod**: Modify the manifest file and the kubelet will automatically update the pod.
- **Deleting a Static Pod**: Remove the manifest file from the directory and the kubelet will delete the pod.

## Use Cases

- Bootstrapping a Kubernetes cluster.
- Running critical system pods that should not be managed by the API server.

Static pods are a powerful tool for managing critical components of your Kubernetes cluster, especially in scenarios where the API server is not available.


## Resources

- [Static Pods walkthrough - video](https://www.youtube.com/watch?v=-9iM9XTaxpE)