---
title: Step 7

---
<!-- Printing the resource name -->

The wide format shows more information than the default output. This is useful in case you need more details, but sometimes, you need fewer details. For example, you only need to output the name of the resource.Let's do this. 

So in order to only print names, we should use the "name" formatter:

```
kubectl get pods --output name{{ execute }}
```

or 

```
kubectl get pods -o name{{ execute }}
```


This command will print the names of all pods running in out cluster. We can also apply it to other resources like Deployment:

```
kubectl get deployments -o name{{ execute }}
```

The output here is quite similar to the one generated when executing `kubectl get <resource> -o custom-columns=NAME:.metadata.name`.

This formatter is useful in some cases when, for instance, you need to run a for loop over resource names in order to execute another command.

Example:

```
kubectl get pod -o name | xargs kubectl describe{{ execute }}
```