---
title: Step 5

---
<!-- updating the app -->

When using containerized applications, you usually build an Docker image including a certain version of your code, then deploy it. When you release a newer version, you build another image with the newer version. Let's see, in the following example, how we can upgrade an image from v1 to v2. 

Start by creating a deployment using the 1st version:

```
kubectl create deployment httpserver-bis --image=brainarator/httpserver:v1{{ execute }}
```

We want to upgrade the used image to the v2. This can be done using the `kubectl set image` command:

```
kubectl set image deployments/httpserver-bis httpserver=brainarator/httpserver:v2{{ execute }}
```

This is what we call a rolling update.

This is the structure of the command:

```bash
kubectl set image deployments/<deployment_name> <container_name>=<image>
```

We can notice the image was upgraded using:

```
kubectl get pods{{ execute }}
```

or

```
kubectl describe deployment httpserver-bis | grep Image{{ execute }}
```