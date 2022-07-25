---
title: Step 2

---
<!-- creating a pod -->

To play with kubectl outputs, let's create the following Deployment.

Create "deployment-1.yaml":

``` yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: busybox
spec:
  replicas: 1
  selector:
    matchLabels:
      name: busybox
  template:
    metadata:
      labels:
        name: busybox
    spec:
      containers:
        - name: busybox
          image: busybox
          command: ["/bin/sh","-c"]
          args: ["echo Hello from container 1; while true; do sleep 604800; done"]       
{{copy fileName='deployment-1.yaml'}}
```

Use the following command in order to create this deployment:

```
kubectl apply -f deployment-1.yaml{{ execute }}
```

This will create a Pod that we named "busybox". It uses Busbox image and launch the infinite loop `while true; do sleep 604800; done` to stay up and running during 1 week (604800 seconds).


Now when we use 

```
kubectl get pods{{ execute }}
```
we will get the basic representation of kubectl output:

```bash
NAME    READY   STATUS    RESTARTS   AGE
<name>  <x/y>   <status>  <restarts> <age>
```