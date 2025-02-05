# Services Cluster IP

## What is a Services Cluster IP?

A Services Cluster IP is a virtual IP address that is assigned to a service in a Kubernetes cluster. This IP address is stable and remains constant for the lifetime of the service, allowing other components within the cluster to reliably communicate with the service.

## What Problem Does It Solve?

The Services Cluster IP solves the problem of dynamic and ephemeral IP addresses of individual pods. In Kubernetes, pods can be created and destroyed frequently, and each pod gets a unique IP address. This makes it difficult for other services to keep track of the current IP addresses of the pods they need to communicate with.

By assigning a stable Cluster IP to a service, Kubernetes provides a consistent endpoint for communication. This allows services to discover and communicate with each other reliably, regardless of the underlying pod IP addresses.

### Key Benefits:
- **Stable Endpoint:** Provides a consistent IP address for services.
- **Service Discovery:** Simplifies the process of finding and connecting to services.
- **Load Balancing:** Distributes traffic across multiple pods behind the service.

### Example:

```yaml
apiVersion: v1
kind: Service
metadata:
    name: back-end
spec:
    type: ClusterIP
    selector:
        app: MyApp
        type: back-end
    ports:
        - protocol: TCP
            port: 80
            targetPort: 9376
    clusterIP: 10.0.171.239
```

In this example, the service `my-service` is assigned a Cluster IP `10.0.171.239`, which other components in the cluster can use to communicate with the pods selected by the label `app: MyApp`.