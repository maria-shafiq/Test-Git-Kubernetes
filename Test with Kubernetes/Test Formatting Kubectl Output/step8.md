---
title: Step 8

---
<!-- Output YAML -->

The YAML output is more verbose than the 3 previous formats, as it shows more details like the metadata information, DNS, restart policies, volumes ..etc.

In order to use this formatter, execute the following command:

```
kubectl get pods -o yaml{{ execute }}
```

The output is a long YAML object, with the necessary details that you need to understand the state of a Kubernetes object.

When we run `kubectl get pods -o yaml`, we are printing the output of all pods, but sometimes we need to view a single Pod (or a signle object in general).

It is possible to use the formatter with a single Pod using `kubectl get pods <pod_name> -o yaml`

If you want to try this, let's get the name of the pod using:

```
POD=`kubectl get pod -l name=busybox -o jsonpath="{.items[0].metadata.name}"`{{ execute }}
```

Now, let's execute the YAML formatter on the same pod using:

```
kubectl get pods $POD -o yaml{{ execute }}
```

With the YAML formatter you can use commands like [yq](https://github.com/mikefarah/yq) to make getting specific data from a YAML output easy.