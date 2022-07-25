---
title: Step 2

---
Kubernetes `run` command will start running 1 or more instances of a container image on our cluster. It is used as follows:

```
kubectl create deployment <deployment_name> <properties>
```

In this example, we are going to deploy the image from `brainarator/httpserver` which is a simple web server.

Use the following command to create the deployment:

```
kubectl create deployment httpserver --image=brainarator/httpserver:latest{{ execute }}
```

Once the deployment is created, we use the following command to list it:

```
kubectl get deployments{{ execute }}
```

We can also get information about our deployment using:

```
kubectl describe deployment httpserver{{ execute }}
```