---
title: Step 6

---
<!-- Multiple init containers -->

If you have many tasks that the init container should execute, a good practice is breaking tasks into a number of steps, each handled by a different init container in order to easily identify the failing initializations.

In order to understand how multiple containers are executed, create "multiple-init-container-app.yaml" file:

```
touch multiple-init-container-app.yaml{{ execute }}
```

Then add the following manifest. 

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multiple-init-container-app
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: website-volume
      mountPath: /usr/share/nginx/html
  initContainers:
  - name: init-container-1
    image: busybox
    command: ['sh', '-c', 'echo This index page was created by the init container 1 > /website/index.html']
    volumeMounts:
    - name: website-volume
      mountPath: "/website"
  - name: init-container-2
    image: busybox
    command: ['sh', '-c', 'echo This index page was created by the init container 2 >> /website/index.html']
    volumeMounts:
    - name: website-volume
      mountPath: "/website"      
  - name: init-container-3
    image: busybox
    command: ['sh', '-c', 'echo This index page was created by the init container 3 >> /website/index.html']
    volumeMounts:
    - name: website-volume
      mountPath: "/website"           
  volumes:
  - name: website-volume
{{copy fileName='multiple-init-container-app.yaml'}}
```

Apply the manifest using:

```
kubectl apply -f multiple-init-container-app.yaml{{ execute }}
```

The previous configuration create 3 init containers: "init-container-1", "init-container-2" and "init-container-3". 

Init containers will be executed in the order they are defined. This can be verified by executing `curl http://0.0.0.0` on "nginx-container".

```
kubectl exec -it multiple-init-container-app curl http://0.0.0.0{{ execute }}
```

You should be able to see:

```bash
This index page was created by the init container 1
This index page was created by the init container 2
This index page was created by the init container 3
```