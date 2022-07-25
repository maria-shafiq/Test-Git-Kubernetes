---
title: Step 5

---
<!--failure policy 2/2 -->

The other choice we have is setting the restart polocy to "Never".

Apply the following configuration.

Create a new file "init-container-app-restart-never.yaml":

```
touch init-container-app-restart-never.yaml{{ execute }}
```

Then add the following YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-container-app-restart-never
spec:
  restartPolicy: Never
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: website-volume
      mountPath: /usr/share/nginx/html
  initContainers:
  - name: init-container
    image: busybox
    command: ['sh', '-c', '$((0/0))']
    volumeMounts:
    - name: website-volume
      mountPath: "/website"
  volumes:
  - name: website-volume
{{copy fileName='init-container-app-restart-never.yaml'}}
```  

The pod should crash and unlike the previous one, it will never restart.

Executing the get pods command will show how the pod will never restart after the first execution:

```
kubectl get pods{{ execute }}
```

You should get a similar outout to the following one:

```
NAME                                READY   STATUS                  RESTARTS   AGE
init-container-app-restart-never   0/1     Init:0/1                0          2s
```