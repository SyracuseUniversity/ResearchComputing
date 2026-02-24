---
layout: default
title: Getting Started
nav_order: 3
has_children: true
---

# Getting Started with Syracuse Research Computing

{: .note }
**You've been assigned a cluster account!** This guide will help you transition from interactive computing to batch computing on your assigned resource. Check your welcome email for your specific login information, assigned cluster, and home directory details.

{: .warning }
**CRITICAL: Login Nodes vs. Compute Nodes**  
The login node is NOT where your work runs. When you SSH in, you're on a shared login node used by all researchers to submit jobs. Login nodes are ONLY for: light text editing, creating conda/UV environments, testing singularity containers load, submitting jobs, and checking job status. Do NOT run computational code, install software outside conda/UV/singularity, use IDEs, leave tmux sessions running, or keep unused SSH connections open. Your work runs on dedicated compute nodes after you submit it as a job. Need a development environment? Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

---

## How to Use This Guide

Use the navigation on the left to explore each topic, or work through them in order for a complete introduction to cluster computing.

{: .note }
**Want to understand all our computing options?** See our [complete resource overview](../resources-overview) for information about clusters, virtual machines, GPU infrastructure, and cloud solutions.
