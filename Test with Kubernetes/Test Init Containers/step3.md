---
title: Step 3

---
<!--Creating an init container -->

In order better understand how to use init containers, we are going to create an Nginx server hosting a simple static HTML page. 
Before the NGINX server start, an init container will create the HTML page, add it to the web server directory then die.

On a fresh Nginx installation, the default index page is found in `/usr/share/nginx/html/index.html`. 
If we need another container (the init container in our case) to update the index.html page, we need to mount the folder to a volume. The volume will be shared with the init container. The init container will be able to create the index page.

Let's start by creating an Nginx container and map the `/usr/share/nginx/html` to a volume.

Open a new file "init-container-app.yaml":

```
touch init-container-app.yaml{{ execute }}
```

Then add the following YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-container-app
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: website-volume
      mountPath: /usr/share/nginx/html
  volumes:
  - name: website-volume
{{copy fileName='init-container-app.yaml'}}
```

The second step is adding the init container. Update "init-container-app.yaml" so that it look like this:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-container-app
spec:
  containers:
  - name: nginx-container
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: website-volume
      mountPath: /usr/share/nginx/html
***  initContainers:
  - name: init-container
    image: busybox
    command: ['sh', '-c', 'echo This index page was created by the init container > /website/index.html']
    volumeMounts:
    - name: website-volume
      mountPath: "/website"
***
  volumes:
  - name: website-volume
{{copy fileName='init-container-app.yaml'}}
```

This configuration deploys the "init-container". It also mounts `/usr/share/nginx/html` on "nginx-container" to `/website` on "init-container" by mapping the volume "website-volume" to the container "init-container". 

In other words, if "init-container" writes to `/website`, all modifications will be also written to `/usr/share/nginx/html` on "nginx-container".

Apply the new configuration:

```
kubectl apply -f init-container-app.yaml{{ execute }}
``` 

The init container will be executed first, it may take some seconds to create the new "index.html" page. The init container dies after completing the execution. 

You can check the new index page using:

```
kubectl exec -it init-container-app curl http://0.0.0.0{{ execute }}
```

You should be able to see:

```bash
This index page was created by the init container
```