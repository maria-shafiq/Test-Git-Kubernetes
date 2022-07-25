---
title: Step 5

---
When we created the first Deployment, we used the `kubectl create -f <yaml_file> --save-config` command. For updates, we can use the `kubectl apply` command:

```
kubectl apply -f deployment.yaml{{ execute }}
```

The desired state is updated and we can view the updated deployment using:

```
kubectl get deployment{{ execute }}
```

You should have 3 pods running now.