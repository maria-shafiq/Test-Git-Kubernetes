---
title: Step 2

---
<!--Networking: How containers refer to each others-->

When 2 containers run inside a single pod, they share the same resources of the pod including networking and filesystem.

Since "webserver" container is running a web server listening on port 80, it should be accessible from the "alpine" container.

Let's connect to "alpine" container using:

```
kubectl exec -it my-pod -c alpine sh{{ execute }}
```

Once we are inside the container, we can check if the Nginx container is accessible using the port 80. 
Execute the following command in "alpine" container to install Curl:

```
apk --no-cache add curl{{ execute }}
```

Once the package is installed, we can use it check the Nginx index page (sent by "webserver" container on port 80):

```
curl http://localhost:80{{ execute }}
```

The output should be the Nginx default page:

```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

As we can see, both containers share the same localhost address, they also share the same ports managed by the Pod.