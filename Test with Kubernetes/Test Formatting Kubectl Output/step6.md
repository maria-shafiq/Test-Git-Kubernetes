---
title: Step 6

---
<!-- Print a custom table using a file -->

Previsouly in this scenario we used the following command to customize the columns of a table and show name, namespace, host IP, Pod IP and QoS class of the Pod:

```
kubectl get pods $POD -o custom-columns=NAME:.metadata.name,NAMSPACE:.metadata.namespace,"HOST IP":.status.hostIP,"POD IP":.status.podIP,OoS:.status.qosClass{{ execute }}
```

If you are going to use this representation more than once, type all of the above command each time is not a good idea. A solution is uinsg template files.

Let's create a file called "template.txt". 

```
touch template.txt{{ execute }}
```

Add the following text to the file:

```bash
NAME                NAMSPACE                HOSTIP              PODIP           OoS
metadata.name       metadata.namespace      status.hostIP       status.podIP    status.qosClass
{{copy fileName='template.txt'}}
```

As you can see, we create the template using the same specs for each column.

In order to use this format, we should use `-o custom-columns-file=<filename>`. In our case, we need to execute the following command:

```
kubectl get pods $POD  -o custom-columns-file=template.txt{{ execute }}
```