---
title: Step 1

---
<!--Introduction -->
In this scenario, we are going to understand how to run multiple containers inside the same pod and share internal resources between them.

In order to understand how things work, we are going to deploy two containers. 

Create "two-containers.yaml" file:

```
touch two-containers.yaml{{ execute }}
```

Then add the following YAML code:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: default
spec:
  containers:
  - name: webserver
    image: nginx
    ports:
    - containerPort: 80    
  - name: alpine
    image: alpine:3.2
    command:
      - /bin/sh
      - "-c"
      - "sleep 60m"
{{copy fileName:'two-containers.yaml'}}
```  

Apply the configuration using:


```
kubectl apply -f two-containers.yaml{{ execute }}
```

This code will create two containers:

- The first one is called "webserver". This container is an Nginx server listening on port 80.
- The second one is called "alpine". The alpine container launches a process when it's up and running and, executes the command `/bin/sh -c sleep 60m`.

Let's check if the pod is running using:

```
kubectl get pods{{ execute }}
```