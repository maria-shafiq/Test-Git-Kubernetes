---
title: Step 4

---
If the init container fails, the main container (Nginx in our case) will never be launched. 

Kubernetes will restart the pod in case it fails and returns an error. This is the default behavior. 

In some specific cases, we don't need the the pod to run indefinitely when the init container fails. This is when `restartPolicy` is useful.

Let's try running an init container that will execute a division by zero, therefore dies with an error.

The first thing we will try is setting `restartPolicy` to `always` (which is the default behavior).

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-container-app-restart-always
spec:
  restartPolicy: Always
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
{{copy fileName='init-container-app-restart-always.yaml'}}
```

Use the following command to apply the configuration:

```
kubectl apply -f init-container-app-restart-always.yaml{{ execute }}
```

After applying this manifest, execute `kubectl get pods -w`, you will be able to see that the pod is restarting. The reason, of course, is that it fails to make a division by zero, so it will keep dying and restarting.

```bash
NAME                                READY   STATUS                  RESTARTS   AGE
init-container-app-restart-always   0/1     Init:0/1                0          2s
init-container-app-restart-always   0/1     Init:Error              0          3s
init-container-app-restart-always   0/1     Init:Error              1          5s
init-container-app-restart-always   0/1     Init:CrashLoopBackOff   1          6s
init-container-app-restart-always   0/1     Init:Error              2          19s
init-container-app-restart-always   0/1     Init:CrashLoopBackOff   2          31s
init-container-app-restart-always   0/1     Init:Error              3          44s
init-container-app-restart-always   0/1     Init:CrashLoopBackOff   3          59s
init-container-app-restart-always   0/1     Init:Error              4          90s
init-container-app-restart-always   0/1     Init:CrashLoopBackOff   4          103s
init-container-app-restart-always   0/1     Init:Error              5          2m59s
init-container-app-restart-always   0/1     Init:CrashLoopBackOff   5          3m12s
init-container-app-restart-always   0/1     Init:Error              6          5m48s
init-container-app-restart-always   0/1     Init:CrashLoopBackOff   6          6m1s
```

Use `CTRL/CMD + c` to exit.