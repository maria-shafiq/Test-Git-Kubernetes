---
title: Step 2

---

Open the file editor and create the `index.html` file.

```
touch index.html{{ execute }}
```

Then add the following HTML code:

```html
<h1>This is a web server</h1>
{{copy fileName='index.html'}}
```

On the same folder, let's create a Dockerfile.

```
touch Dockerfile{{ execute }}
```

Then add:

```Dockerfile
FROM python:3.8.1-slim-buster
COPY index.html /
EXPOSE 80
CMD python -m http.server 80
{{copy fileName='Dockerfile'}}
```

The above Dockerfile will download the base image `python:3.8.1-slim-buster`, then it will copy `index.html` file on the root of the container.

It will also expose the port 80 then when the container runs it will run the Python command `python -m http.server 80` which will open a simple web server on port 80.

In order to use this image, you should push it to a (private or public) repository using the Docker push command: `docker push [OPTIONS] NAME[:TAG]`

Example: `docker build -t brainarator/httpserver:latest . && docker push brainarator/httpserver:latest`

Our image becomes accessible publically on [Dockerhub](https://hub.docker.com/repository/docker/brainarator/httpserver).