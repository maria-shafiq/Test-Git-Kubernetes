---
title: Step 4

---
<!-- The wide output -->

Let's view the default kubectl output using `kubectl get pods`.

What we get uses this format:

```bash
NAME    READY   STATUS    RESTARTS   AGE
<name>  <x/y>   <status>  <restarts> <age>
```

Another output that is similar to the previous one is the wide output and it can be viewed using:

```
kubectl get pods -o wide{{ execute }}
```

This command will show more infromation like the IP and the node name.

If it's applied to another resource type like Deployment, it will show different columns. You can see this using 

```
kubectl get deployments --output=wide{{ execute }}
```

The wide output is basically the same basic outout but with more details.