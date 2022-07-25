---
title: Step 4

---
<!--scaling the deployment to zero-->

You can scale your deplyment to any desired number of replicas depending on your cluster capacity. 
Note that when you scale it to 0, all of your pods and deployments will be terminated:

You can try this using:

```
kubectl scale --replicas=0 deployment httpserver{{ execute }}
```

Then:

```
kubectl get pods{{ execute }}
```

Or:

```
kubectl get deployments{{ execute }}
```

At the moment, let's get back our pods by scaling them to a number of replicas greater or equal to 1.

```
kubectl scale --replicas=1 deployment httpserver{{ execute }}
```