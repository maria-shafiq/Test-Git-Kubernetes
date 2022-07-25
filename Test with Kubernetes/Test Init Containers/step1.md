---
title: Step 1

---
<!--introduction-->

In this scenario, we are going to understand what init containers are and how they work.

In some cases, containers need to be intialized or setup before starting. Init containers provide a Kubernetes native way to run utilities or setup scripts. Usually, an init container will execute instructions before exiting. The main container will run just after.

Init containers always run to completion. When you setup multiple init containers, each one of them must complete before the next one starts.

We are going to see some use cases here.