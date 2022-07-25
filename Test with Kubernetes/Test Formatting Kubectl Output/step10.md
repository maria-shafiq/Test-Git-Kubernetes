---
title: Step 10

---
<!-- Using jsonpath expressions -->

JSONPath is used to select and extract a JSON document's property values. Kubectl supports JSONPath template.

The JSON output obtained when we execute the following command contains many details:

```
kubectl get pods $POD -o json{{ execute }}
```

Sometimes, we need to get some elements from the JSON output. This is when we can leverage JSONPath support.

JSONPath expressions are used when we need to execute more complex operations and view a more customized output.

For example, to list all container images running in a cluster, we should iterate through the pods inside the output of `kubectl get pods --all-namespaces -o jsonpath="{.items[*]}`, then for each iteration we need to get the `.spec.containers` of each Pod, then iterate through each container to get the `.image`.

This is how we transalte this to an expression:

```
kubectl get pods --all-namespaces -o jsonpath="{.items[*].spec.containers[*].image}"{{ execute }}
```

We call `{.items[*].spec.containers[*].image}` a JSONPath expression.

Note that you need to use double quotes to quote text inside JSONPath expressions.

Another way to do the same thing is **recursively** parsing the output of `kubectl get pods --all-namespaces` to find the `image` field:

```
kubectl get pods --all-namespaces -o jsonpath="{..image}"{{ execute }}
```

To make the output more readable, we can use everyday Linux command like "tr" and replace the space by a new line: 

```
kubectl get pods --all-namespaces -o jsonpath="{..image}"  | tr -s '[[:space:]]' '\n' {{ execute }}
```

JSONPath regular expressions are not supported, you can use jq in this case.