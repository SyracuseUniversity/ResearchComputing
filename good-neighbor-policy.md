---
layout: default
title: Good Neighbor Policy
nav_order: 2
---

# Research Computing Good Neighbor Policy

Research Computing provides access to many compute resources at no cost for the purpose of academic research performed or overseen by a faculty member. Use of these resources is governed by the [Syracuse University Information Technology Resources Acceptable Use Policy](https://policies.syr.edu/policies/free-speech/information-technology-resources-acceptable-use-policy/).

These resources are shared by the entire campus research community. We ask that users act as good neighbors to the people they are sharing with. The guidelines below are examples rather than an exhaustive list. Research Computing staff monitor the health of the clusters continually, and any process that impacts other users or the cluster as a whole is likely to be shut down. Repeated disruptive activity may, in extreme cases, result in an account being temporarily suspended.

---

## Be Mindful of Other Users

For many people the clusters will be their first time on a shared system after years of working on personal computers. At any moment dozens of other users may be logged into the login nodes (`its-og-login*`, `its-zest-login*`, etc.). Every command you run there consumes memory and CPU that nobody else can use.

Keep your activity on the login nodes light — editing files, submitting and monitoring jobs, and short tests that run no more than a couple of minutes. Anything that needs real resources should be submitted to the cluster rather than run on the login node.

We know IDEs like VSCode are useful, so we allow them inside constrained sandboxes. These sandboxes cap the memory and CPU available, so these tools may not perform as well as you expect. If you need a real development environment, contact [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) and we will talk through the options.

---

## The Clusters Are Not Suitable for Interactive Use

The login nodes should not be used for interactive processes or development work. Neither should cluster execute nodes, even though reserving one and working on it directly is technically possible.

Compute resources are most efficient when they are constantly busy, running at 100% CPU or GPU. Development work does not look like that — it runs hard for a few moments, then sits idle for much longer. Those idle cycles are wasted, and the cluster is better served by handing those resources to jobs that will keep them busy.

---

## Be Mindful of Security

Beyond what University policy already covers, help keep the clusters safe for yourself and everyone else.

Do not:
- Share your password or your SSH private keys
- Let anyone else run work under your credentials, including labmates and collaborators
- Run untrusted binaries, on either the login nodes or as cluster jobs
- Run servers or any software that opens a port, including reverse SSH tunnels
- Download large amounts of data from third-party sites

You are responsible for everything that happens under your account, whether you were at the keyboard or not.

Heavy automated downloading can look like a denial of service attempt to the remote site. When that happens they block the address range, and the block lands on Syracuse University rather than on the individual user. Some research legitimately needs to do these things — get in touch at [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) and we will set it up safely. Do the same right away if you think your account or your keys have been compromised.

---

## Be Mindful of Scheduling Policies and Shared Resources

Both schedulers — HTCondor on OrangeGrid and Slurm on Zest — use fair share so that no single user can monopolize the cluster. When one user has recently consumed significant resources, new jobs from other users get priority. This can be frustrating when a deadline is close.

When that happens it is tempting to work around the scheduler and claim resources before you actually need them. GPUs are where we see this most, since they are the scarcest resource we have. Please don't. The same goes for locks our team occasionally puts on resources, whether for internal work or to clear the way for a group facing a deadline.

If you need dedicated resources for a short stretch, contact [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu). We would rather find you something than have you fight the scheduler for it.

---

## Be Mindful of Agentic Tools

Everything above applies to tools acting on your behalf, not just to you personally. We are not banning them — just understand that an account can be suspended for disruptive activity whether a person or a program caused it. If your agent scrapes a site or floods the login node, that is still your account and still your responsibility.

---

## Enforcement

Enforcement decisions rest with Research Computing. If your access has been suspended, or you have questions about an action we took, contact [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu).
