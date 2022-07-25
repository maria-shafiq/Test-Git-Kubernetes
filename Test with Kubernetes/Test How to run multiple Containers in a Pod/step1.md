---
title: Step 1

---
<!--intro-->

Kubernetes, unlike Docker or Docker Swarm, use a Pod as the smallest deployable unit.
The Pod logically wraps the container and manages it. It is represented by a single instance of a running process in a cluster. However, a Pod can run multiple containers.

When a Pod runs multiple containers, the containers share the same Pod resources. They are managed as a single entity.

Containers in the same Pod share the same IPC namespace.
IPC namespaces are a Linux Kernet mechanism providing a a speration of shared memory segments, message queues and semaphores.

Let's jump to the next step to see how it's possible to run multiple containers in a single Pod.