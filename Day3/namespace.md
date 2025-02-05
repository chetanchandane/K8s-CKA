# Kubernetes Namespaces

## What are Namespaces in Kubernetes?

Namespaces in Kubernetes are a way to divide cluster resources between multiple users. They provide a mechanism for isolating groups of resources within a single cluster. Namespaces are intended for use in environments with many users spread across multiple teams, or projects.

## General Commands for Namespaces

- **List all namespaces:**
    ```sh
    kubectl get namespaces
    ```

- **Create a new namespace:**
    ```sh
    kubectl create namespace <namespace-name>
    ```

- **Delete a namespace:**
    ```sh
    kubectl delete namespace <namespace-name>
    ```

- **Describe a namespace:**
    ```sh
    kubectl describe namespace <namespace-name>
    ```

## How to Set Context Permanently

To set the default namespace for the current context, use the following command:
```sh
kubectl config set-context --current --namespace=<namespace-name>
```

## How to Switch Among Namespaces

To switch between namespaces, you can use the `--namespace` flag with your `kubectl` commands:
```sh
kubectl get pods --namespace=<namespace-name>
```

## Shorthand for Namespace Commands

You can use the following shorthand commands to work with namespaces:

- **List all namespaces:**
    ```sh
    kubectl get ns
    ```

- **Create a new namespace:**
    ```sh
    kubectl create ns <namespace-name>
    ```

- **Delete a namespace:**
    ```sh
    kubectl delete ns <namespace-name>
    ```

- **Describe a namespace:**
    ```sh
    kubectl describe ns <namespace-name>
    ```
Alternatively, you can change the default namespace for your current context as shown above.
