---
title: Step 6

---
In this part we are going to create a Kubernetes service. Let's understand some basic concepts first.

A service is an abstraction used to define a logical set of Pods and a policy by which to access them.

Let's start by a simple and basic use case in which we are going to define how we can access the http server we already deployed.

As for now, our Deployment runs the httpserver container, but the server itself can not be accessed by simply using a deployment object, hence the use of the service object.

Create "service.yaml" file:

```
touch service.yaml{{ execute }}
```

Then add the following YAML code:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: httpserver-service
  labels:
    app: httpserver
spec:
  type: NodePort
  ports:
  - port: 80
    nodePort: 32767
  selector:
    app: httpserver
{{copy fileName='service.yaml'}}
```

Create the service:

```
kubectl create -f service.yaml{{ execute }}
```

Once the service is ready, you see it using:

```
kubectl get service httpserver-service{{ execute }}
```

If you want to see all your services, you can use:

```
kubectl get service{{ execute }}
```

or

```
kubectl get services{{ execute }}
```

or even:

```
kubectl get svc{{ execute }}
```

The httpserver service should now be accessible in our local development environment. We can test this by using a curl command:

```
curl http://localhost:32767{{ execute }}
```