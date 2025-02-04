# Kube-Proxy

Kube-Proxy is a network proxy that runs on each node in a Kubernetes cluster. It maintains network rules on nodes, allowing network communication to your Pods from network sessions inside or outside of your cluster.

## Key Features

- **Service Discovery**: Kube-Proxy helps in service discovery by maintaining network rules to route traffic to appropriate backend services.
- **Load Balancing**: It performs simple TCP, UDP, and SCTP stream forwarding with round-robin load balancing.

## How It Works

Kube-Proxy uses three different modes to manage network rules:

1. **Userspace Mode**: This mode uses the `iptables` tool to manage network rules. It is deprecated and not recommended for production use.
2. **iptables Mode**: This mode uses `iptables` to manage network rules. It is more efficient than userspace mode.
3. **IPVS Mode**: This mode uses IP Virtual Server (IPVS) to manage network rules. It is the most efficient and scalable mode.

## Configuration

Kube-Proxy can be configured using a configuration file or command-line flags. Here is an example of a configuration file:

```yaml
apiVersion: kubeproxy.config.k8s.io/v1alpha1
kind: KubeProxyConfiguration
mode: "ipvs"
clusterCIDR: "10.244.0.0/16"
```

## Common Commands

- **Check Kube-Proxy Logs**:
    ```sh
    kubectl logs -n kube-system -l k8s-app=kube-proxy
    ```

- **Restart Kube-Proxy**:
    ```sh
    kubectl -n kube-system rollout restart daemonset kube-proxy
    ```

## Troubleshooting

- **Check Network Rules**:
    ```sh
    iptables -L -t nat
    ```

- **Verify IPVS Rules**:
    ```sh
    ipvsadm -L -n
    ```

## References

- [Kubernetes Official Documentation](https://kubernetes.io/docs/concepts/services-networking/service/)
- [Kube-Proxy Configuration](https://kubernetes.io/docs/reference/config-api/kube-proxy-config.v1alpha1/)

# Kubelet

Kubelet is an essential component of Kubernetes that runs on each node in the cluster. It ensures that containers are running in a Pod by interacting with the container runtime.

## Key Features

- **Pod Lifecycle Management**: Kubelet watches for PodSpecs via the Kubernetes API server and ensures that the containers described in those PodSpecs are running and healthy.
- **Node Status Management**: It regularly reports the status of the node and the Pods running on it to the Kubernetes API server.

## How It Works

Kubelet works by:

1. **Registering the Node**: It registers the node with the Kubernetes API server.
2. **Monitoring PodSpecs**: It watches for changes to PodSpecs and ensures that the desired state is maintained.
3. **Interacting with Container Runtime**: It communicates with the container runtime (e.g., Docker, containerd) to manage the lifecycle of containers.

## Configuration

Kubelet can be configured using a configuration file or command-line flags. Here is an example of a configuration file:

```yaml
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
address: "0.0.0.0"
port: 10250
```

## Common Commands

- **Check Kubelet Logs**:
    ```sh
    journalctl -u kubelet
    ```

- **Restart Kubelet**:
    ```sh
    systemctl restart kubelet
    ```

## Troubleshooting

- **Check Node Status**:
    ```sh
    kubectl get nodes
    ```

- **Describe Node**:
    ```sh
    kubectl describe node <node-name>
    ```

## References

- [Kubernetes Official Documentation](https://kubernetes.io/docs/concepts/overview/components/#kubelet)
- [Kubelet Configuration](https://kubernetes.io/docs/reference/config-api/kubelet-config.v1beta1/)
- [Kubelet + Kube-Proxy](https://www.youtube.com/watch?v=qzjpPUAvGHc)
- [What is Kubelet?](https://www.youtube.com/watch?v=7dX7trVXVPs)