---
title: Step 5

---
<!-- Print a custom table -->

We have seen that both of the following commands `kubectl get pods` and  `kubectl get pods -o wide` will output tables. We also understood that the second command will print more detailed information.

In some cases, we need to customize the output of the table. This is what we are going to understand here.

In order to that, we should use the option `-o custom-columns=<spec>`.

This is an example:

Let's get the name of the Pod:

```
POD=`kubectl get pods -l name=busybox -o=jsonpath='{.items[0].metadata.name}'`{{ execute }}
```

Then use it with `kubectl get pods` command:
```
kubectl get pods $POD -o custom-columns=NAME:.metadata.name{{ execute }}
```

This will print a table but only with the name of the Pod.

We can also add other columns to the table. For example: namespace, host IP, Pod IP and QoS class:

```
kubectl get pods $POD -o custom-columns=NAME:.metadata.name,NAMSPACE:.metadata.namespace,"HOST IP":.status.hostIP,"POD IP":.status.podIP,OoS:.status.qosClass{{ execute }}
```