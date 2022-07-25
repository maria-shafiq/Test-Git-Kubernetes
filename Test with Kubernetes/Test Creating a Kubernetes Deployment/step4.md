---
title: Step 4

---
The deployment are up and running. Let's see how to scale it.

Remember that the main use case of a deployment is providing a desired state. For instance, we want to have a pod running a given image, label and name.. etc 

We can also "describe" (using YAML) the number of pod replicas we run. For example, we can scale the number of httpservers to 3. 

Update "deployment.yaml":

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpserver
spec:
  replicas: 3
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

We only changed `replicas` from 1 to 3 in the previous YAML.