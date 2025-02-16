# Multiple Schedulers in Kubernetes

## Why Do We Need Multiple Schedulers?

In Kubernetes, the default scheduler is responsible for assigning pods to nodes based on resource availability and other constraints. However, in some cases, you may need more control over the scheduling process. Multiple schedulers allow you to:

- Implement custom scheduling logic.
- Handle specific workloads with different scheduling requirements.
- Improve resource utilization and efficiency.
- Isolate certain workloads for security or compliance reasons.

## What Are They?

Multiple schedulers are additional scheduling components that you can deploy alongside the default Kubernetes scheduler. Each scheduler can have its own scheduling policies and logic, allowing you to tailor the scheduling process to meet specific needs.

## How Do We Make Use of Them?

To use multiple schedulers in Kubernetes, follow these steps:

1. **Deploy the Custom Scheduler**: Create and deploy a custom scheduler as a Kubernetes deployment.
2. **Specify the Scheduler in Pod Spec**: In the pod specification, specify the scheduler to be used by setting the `schedulerName` field.
3. **Monitor and Manage**: Monitor the performance and behavior of the custom scheduler and make adjustments as needed.

## Example

### Custom Scheduler Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
    name: custom-scheduler
    namespace: kube-system
spec:
    replicas: 1
    selector:
        matchLabels:
            component: custom-scheduler
    template:
        metadata:
            labels:
                component: custom-scheduler
        spec:
            containers:
            - name: custom-scheduler
                image: my-custom-scheduler:latest
                command:
                - ./custom-scheduler
                - --leader-elect=true
```

### Pod Spec with Custom Scheduler

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: my-pod
spec:
    schedulerName: custom-scheduler
    containers:
    - name: my-container
        image: nginx
```

In this example, the pod `my-pod` will be scheduled using the `custom-scheduler` instead of the default scheduler.


## Resources

-[Multiple Schedulers](https://www.youtube.com/watch?v=bezQz-mIO7U)