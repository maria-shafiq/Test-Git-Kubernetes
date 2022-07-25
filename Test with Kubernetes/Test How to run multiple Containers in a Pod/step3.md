---
title: Step 3

---
In order to create the second container in the same Pod, we simply need to add another container definition.
Before doing that, let's remove the first container:

```
kubectl delete -f containers.yaml{{ execute }}
```

Let's edit the same file (container.yaml) and add the configuration for the second container. The final result should look like follows:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  containers:
  - image: busybox
    command: ["/bin/sh","-c"]
    args: ["echo Hello from container 1; while true; do sleep 9999999; done"]
    name: container1
***  - image: busybox
    command: ["/bin/sh","-c"]
    args: ["echo Hello from container 1; while true; do sleep 9999999; done"]
    name: container2
***
{{copy fileName='containers.yaml'}}
```

Deploy our containers by running:

```
kubectl apply -f containers.yaml{{ execute }}
```

You can now check that we have 2 containers running out of 2:

```
kubectl get pods{{ execute }}
```