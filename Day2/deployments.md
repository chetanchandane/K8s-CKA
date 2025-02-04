# Types of Deployments in Kubernetes

Kubernetes supports several types of deployments to manage applications. Here are the main types:

## 1. Recreate Deployment
This deployment strategy involves terminating all existing pods before creating new ones. It is useful when you need to ensure that no old pods are running during the deployment of new ones.

## 2. Rolling Update Deployment
This is the default deployment strategy in Kubernetes. It gradually replaces old pods with new ones, ensuring that some pods are always available during the update process. This strategy helps in minimizing downtime.

## 3. Blue-Green Deployment
In this strategy, two separate environments (blue and green) are maintained. The new version of the application is deployed to the green environment while the blue environment serves the live traffic. Once the new version is verified, traffic is switched to the green environment.

## 4. Canary Deployment
Canary deployments involve rolling out the new version to a small subset of users before making it available to the entire infrastructure. This allows for testing the new version in a production environment with minimal risk.

## 5. A/B Testing Deployment
This strategy involves running two or more versions of the application simultaneously to test which one performs better. Traffic is split between the versions based on predefined rules.

## 6. Shadow Deployment
In a shadow deployment, the new version of the application receives a copy of the real-time traffic without impacting the live environment. This helps in testing the new version under real-world conditions.

Each deployment strategy has its own use cases and benefits, and the choice of strategy depends on the specific requirements of the application and the desired level of availability during the deployment process.

## Commands Related to Deploying Images

Here are some common `kubectl` commands used for deploying images in Kubernetes:

### Deploying an Image
To create a deployment using a specific image, you can use the following command:
```sh
kubectl create deployment <deployment-name> --image=<image-name>
```
Example:
```sh
kubectl create deployment nginx-deployment --image=nginx:1.14.2
```

### Updating an Image
To update the image of an existing deployment, use the `set image` command:
```sh
kubectl set image deployment/<deployment-name> <container-name>=<new-image-name>
```
Example:
```sh
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.0
```

### Rolling Back an Update
If you need to roll back to a previous version of the deployment, use the `rollout undo` command:
```sh
kubectl rollout undo deployment/<deployment-name>
```
Example:
```sh
kubectl rollout undo deployment/nginx-deployment
```

### Viewing the Status of a Deployment
To check the status of a deployment, use the `rollout status` command:
```sh
kubectl rollout status deployment/<deployment-name>
```
Example:
```sh
kubectl rollout status deployment/nginx-deployment
```

### Scaling a Deployment
To scale the number of replicas in a deployment, use the `scale` command:
```sh
kubectl scale deployment/<deployment-name> --replicas=<number-of-replicas>
```
Example:
```sh
kubectl scale deployment/nginx-deployment --replicas=3
```

These commands help in managing the lifecycle of your application deployments in Kubernetes.