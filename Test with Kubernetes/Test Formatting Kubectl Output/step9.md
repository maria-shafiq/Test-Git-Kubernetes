---
title: Step 9

---
<!-- Output JSON -->

The JSON output is like the YAML output as it is more verbose than the other formats. 

It shows more details like the metadata information, DNS, restart policies, volumes ..etc.

In order to use this formatter, execute the following command:

```
kubectl get pods -o json{{ execute }}
```

We can also execute the same command on a single object (eg. the busybox pod): 

```
kubectl get pods $POD -o json{{ execute }}
```

You can use both JSON formtter and a command like [jq](https://stedolan.github.io/jq/) to make getting specific data from a JSON output easy.

For example, use this command to get the namespace: 

```
kubectl get pods $POD  -o json | jq -r  .metadata.namespace{{ execute }}
```

This one is used to get the "hostIP":

```
kubectl get pods $POD  -o json | jq -r  .status.hostIP{{ execute }}
```

And this one is used to get the "podIP":

```
kubectl get pods $POD  -o json | jq -r  .status.podIP{{ execute }}
```

We can also use the "jq" command to get a sub part of the JSON output.

For example:

```
kubectl get pods $POD  -o json | jq -r  .metadata{{ execute }}
```

or 

```
kubectl get pods $POD  -o json | jq -r  .status{{ execute }}
```

The same results get be obtained when we use JSONPath. This is what we are going to see next.