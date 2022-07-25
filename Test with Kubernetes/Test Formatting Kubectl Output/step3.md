---
title: Step 3

---
<!-- Using kubectl flags-->


The default output of kubctl is a table as we can see in the previous step, but to output details to this terminal another format, you can add either the -o or --output flags.

These are some examples:

```bash
kubeclt get pods -o <format>
kubeclt get pods --output <format>
```

Another way to do the same this is:

```bash
kubeclt get pods -o=<format>
kubeclt get pods --output=<format>
```

We can use the output flag with Kubernetes resources such as:

- Persistant volumes
- Config maps
- Service accounts
- Secrets
- Ingress
- Services
- Deployments
- Stateful sets
- Horizontal Pod Autoscalers
- Jobs
- Cron jobs


Note that not all Kubernetes resources supports the output flag.