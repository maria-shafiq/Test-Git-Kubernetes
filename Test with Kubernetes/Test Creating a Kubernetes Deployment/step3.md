---
title: Step 3

---
Kubernetes deployment main responsability is keeping a set of pods running. Let's create a deployment that runs `brainarator/httpserver` image in a pod.

Create "deployment.yaml":

```
touch deployment.yaml{{ execute }}
```

Then add the following YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpserver
spec:
  replicas: 1
  selector:
    matchLabels:
      app: httpserver
  template:
    metadata:
      labels:
        app: httpserver
    spec:
      containers:
      - name: httpserver
        image: brainarator/httpserver:latest
        ports:
        - containerPort: 80
{{copy fileName='deployment.yaml'}}
```

Create the deployment:

```
kubectl create -f deployment.yaml{{ execute }}
```

Once the deployment is ready, you see it using:

```
kubectl get deployment httpserver{{ execute }}
```

If you want to see a list of all deployments, use:

```
kubectl get deployment{{ execute }}
```

or

```
kubectl get deployments{{ execute }}
```

or:

```
kubectl get deploy{{ execute }}
```