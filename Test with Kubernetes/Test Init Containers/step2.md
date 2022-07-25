---
title: Step 2

---
<!-- use cases -->

To better understand init containers, nothing is better than understanding their use cases.

One of the most common use cases is when a container need to wait for another container or a service before launching. 

For example, a web server should wait for the database server until it is deployed. The init container, in this case, will try to connect to the database and when it's deployed, it exits to let the web server execute. Usually web applications will fail when a timeour connection to the database happens. In consequence, all the web server pods will fail and exit. 

Init containers are usually lightweight applications since they don't run any applicative heavy load. They provide a mechanism to ensure the necessary resources or dependencies are satisfied before starting the intended application.