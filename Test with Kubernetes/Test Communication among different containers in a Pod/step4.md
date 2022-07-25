---
title: Step 4

---
<!--shared volumes part 2-->
In the previous step, we updated the index page by getting into "webserver" container. In order to demonstrate how containers share the volumes inside a Pod, we are going to do this differently.


In order to avoid any inconsistency problem, delete the pod before proceeding:

```
kubectl delete pod my-pod{{ execute }}
```

Let's create a shared volume by adding the following code the the Pod spec:

```
  volumes:
  - name: shared-volume
    emptyDir: {}      
```

Then we need to mount it to both containers:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: default
spec:
  containers:
  - name: webserver
    image: nginx
    ports:
    - containerPort: 80  
    volumeMounts:
    - name: shared-volume
      mountPath: /usr/share/nginx/html
  - name: alpine
    image: alpine:3.2
    command:
      - /bin/sh
      - "-c"
      - "sleep 60m"
***    volumeMounts:
    - name: shared-volume
      mountPath: /data
  volumes:
  - name: shared-volume
    emptyDir: {}
***
{{copy fileName:'two-containers.yaml'}}
```

Now, apply the new configuration using:


```
kubectl apply -f two-containers.yaml{{ execute }}
```

When "webserver" container write a file to `/usr/share/nginx/html`, the change will be reflected in the volume. Since the volume is also mapped to `/data` on "alpine" container, the file will be also created on the "alpine" container.

The reverse operation will give the same result. When we create a file under `/data` in "alpine" container, the same file will be created on"webserver" under `/usr/share/nginx/html`.

Get into "alpine" container using:

```
kubectl exec -it my-pod -c  alpine sh{{ execute }}
```

Then create a new  `index.html` using:

```
echo "This is the newest index page" > /data/index.html{{ execute }}
```

Install curl again:

```
apk --no-cache add curl{{ execute }}
```

Then check the localhost on port 80 to check if the Nginx server is using the new index page:

```
curl http://localhost:80{{ execute }}
```

You will be able to see the new line we added to the index page:

```
This is the newest index page
```

The volume is part of the Pod, but it can be shared easily between containers without any headache. Containers in the same Pod share the same resources including volumes and network. 