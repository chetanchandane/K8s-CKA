# Labels and Selectors

## Labels

Labels are key/value pairs that are attached to objects, such as pods. They are used to organize and select subsets of objects. For example:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: mypod
    labels:
        app: myapp
        env: production
spec:
    containers:
    - name: mycontainer
        image: myimage
```

## Selectors

Selectors are used to filter and select objects based on their labels. There are two types of selectors: equality-based and set-based.

### Equality-Based Selectors

Equality-based selectors allow filtering by label keys and values. For example:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: mypod
    labels:
        app: myapp
        env: production
spec:
    containers:
    - name: mycontainer
        image: myimage
---
apiVersion: v1
kind: Service
metadata:
    name: myservice
spec:
    selector:
        app: myapp
    ports:
    - protocol: TCP
        port: 80
        targetPort: 9376
```

### Set-Based Selectors

Set-based selectors allow filtering by a set of values. For example:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: mypod
    labels:
        app: myapp
        env: production
spec:
    containers:
    - name: mycontainer
        image: myimage
---
apiVersion: v1
kind: Service
metadata:
    name: myservice
spec:
    selector:
        matchLabels:
            app: myapp
        matchExpressions:
        - { key: env, operator: In, values: [production, staging] }
    ports:
    - protocol: TCP
        port: 80
        targetPort: 9376
```

## Conclusion

Labels and selectors are powerful tools in Kubernetes for organizing and managing resources. They enable efficient grouping and selection of objects, which is essential for managing large-scale applications.

## Resources

- [Labels and Selectors](https://www.youtube.com/watch?v=zsovXtOFhDE&t=8s)