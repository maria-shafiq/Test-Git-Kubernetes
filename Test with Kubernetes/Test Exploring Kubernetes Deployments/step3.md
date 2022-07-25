---
title: Step 3

---
<!--scaling the deployment-->

Our deployment is running using a single replica as we saw after running the *get deployments* command.

```
kubectl get deployments{{ execute }}
```

In order to scale it, we need to use the *kubectl scale* command:

```
kubectl scale --replicas=<replicas_number> deployment <deployment_name>
```

In order to have 3 replicas of the httpserver deployment, we use the following command:

```
kubectl scale --replicas=3 deployment httpserver{{ execute }}
```

We can verify this using the *get deployment* command:

```
kubectl get deployments{{ execute }}
```

Another way to check that we are running 3 replicas of the same deployment is by checking the number of running pods:

```
kubectl get pods{{ execute }}
```