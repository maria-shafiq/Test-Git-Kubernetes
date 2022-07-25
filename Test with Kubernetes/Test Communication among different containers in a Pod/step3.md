---
title: Step 3

---
<!--shared volumes part 1-->
We can change the default Nginx "index.html" page by creating a new index page on `/usr/share/nginx/html`.

Let's disconnect the alpine container using the following command

```
exit{{ execute }}
```

Connect to "webserver" container, then execute

```
kubectl exec -it my-pod -c  webserver bash{{ execute }}
```

Now execute the following command inside the container:

```
echo "This is the new index page" > /usr/share/nginx/html/index.html{{ execute }}
```

Now connect to "alpine" container and try using curl again to check the new web page:

```
kubectl exec -it my-pod -c  alpine sh{{ execute }}
```

Then:

```
curl http://localhost{{ execute }}
```

You should be able to see the new page.