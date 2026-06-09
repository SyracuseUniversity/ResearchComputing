---
layout: default
title: Cloud Bursting
parent: OrangeGrid (HTC)
nav_order: 3
nav_exclude: true
search_exclude: true
---

# OrangeGrid Cloud Bursting

Cloud bursting extends OrangeGrid capacity into cloud infrastructure, allowing jobs to run on dynamically provisioned workers when on-premises resources are fully utilized.

---

## Component Overview

| Package | Role | Source |
|---|---|---|
| [Nebula](https://github.com/slackhq/nebula) | Mesh VPN connecting provisioner, relay, cache proxy, and workers | github.com/slackhq/nebula |
| [knfsd-cache-utils](https://github.com/GoogleCloudPlatform/knfsd-cache-utils) | NFS cache/proxy helper tooling and design reference | github.com/GoogleCloudPlatform/knfsd-cache-utils |
| [FS-Cache / CacheFiles](https://docs.kernel.org/filesystems/caching/fscache.html) | Linux network filesystem caching used in the NFS cache path | docs.kernel.org |
| [Caddy](https://github.com/caddyserver/caddy) | TLS/mTLS reverse proxy in provisioner | github.com/caddyserver/caddy |
| [NetBox](https://github.com/netbox-community/netbox) | IPAM / source of truth for Nebula IPs and worker state | github.com/netbox-community/netbox |
| [FastAPI](https://github.com/fastapi/fastapi) | Python API framework for provisioner, signing service, and orchestrator | github.com/fastapi/fastapi |
| [Docker Compose](https://github.com/docker/compose) | Compose stack orchestration | github.com/docker/compose |

---

{: .note }
For questions about cloud bursting access or availability, email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu).
