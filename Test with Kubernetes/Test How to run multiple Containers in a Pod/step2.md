---
title: Step 2

---
<!--manipulation-->

Let's start by creating the following YAML file:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  containers:
  - image: busybox
    command: ["/bin/sh","-c"]
    args: ["echo Hello from container 1; while true; do sleep 9999999; done"]
    name: container1
{{copy fileName='containers.yaml'}}
```  

The above code will create a pod called "busybox" in the default namespace then download the Busybox image from Dockerhub and create a container from the same image. 

We also instruct the container to write "Hello from container 1" to STDOUT, then sleep for a long time (9999999s).

```bash
echo Hello from container 1; while true; do sleep 9999999; done
```

Apply the YAML file using:

```
kubectl apply -f containers.yaml{{ execute }}
```

After executing the above command, you can check the number of containers running inside our Pod:

```
kubectl get pods{{ execute }}
```

Check that the READY column is set to 1/1, which means there is a single container running in our Pod.

You can also execute the *describe* command:

```
kubectl describe pod busybox{{ execute }}
```

On the containers section, you can see that there's a single container running:

```bash
Containers:
  container1:
    Container ID:  docker://-
    Image:         busybox
    Image ID:      docker-pullable://busybox@sha256:-
    Port:          <none>
    Host Port:     <none>
    Command:
      /bin/sh
      -c
    Args:
      echo Hello from container 1; while true; do sleep 9999999; done
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-z259l (ro)
```