---
layout: default
title: Getting Started
nav_order: 3
has_children: true
---

# Getting Started with Syracuse Research Computing

{: .note }
**You've been assigned a cluster account!** This guide will help you transition from interactive computing to batch computing on your assigned resource. Check your welcome email for your specific login information, assigned cluster, and home directory details.

---

## What You'll Learn

This guide covers everything you need to get started with cluster computing:

- [**Interactive vs. Batch Computing**]({% link getting-started/interactive-vs-batch.md %}) - Understanding the fundamental shift in how you'll work
- [**Python: Local vs. Cluster**]({% link getting-started/python-comparison.md %}) - See a concrete example of the difference
- [**Linux CLI Basics**]({% link getting-started/linux-basics.md %}) - Essential commands you need (skip if you're comfortable with Linux)
- [**OrangeGrid vs. Zest**]({% link getting-started/orangegrid-vs-zest.md %}) - Understand your assigned cluster and how it works
- [**Connecting**]({% link getting-started/connecting.md %}) - SSH, off-campus access, and file transfer methods
- [**Software & Environments**]({% link getting-started/software.md %}) - Conda, UV, and Singularity setup
- [**Your First Job**]({% link getting-started/first-job.md %}) - Step-by-step walkthroughs for both clusters

{: .warning }
**CRITICAL: Login Nodes vs. Compute Nodes**  
The login node is NOT where your work runs. When you SSH in, you're on a shared login node used by all researchers to submit jobs. Login nodes are ONLY for: light text editing, creating conda/UV environments, testing singularity containers load, submitting jobs, and checking job status. Do NOT run computational code, install software outside conda/UV/singularity, use IDEs, leave tmux sessions running, or keep unused SSH connections open. Your work runs on dedicated compute nodes after you submit it as a job. Need a development environment? Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

---

## How to Use This Guide

Navigate through sections using the left sidebar. Suggested path for new users:

1. **Interactive vs. Batch** - Understand the fundamental shift
2. **Python Comparison** - See concrete examples of the difference
3. **Linux Basics** - Essential commands (skip if familiar with Linux)
4. **OrangeGrid vs Zest** - Understand your assigned cluster
5. **Connecting** - Get connected and learn file transfers
6. **Software** - Set up your software environment
7. **First Job** - Submit your first job

{: .note }
**Want to understand all our computing options?** See our [complete resource overview]({% link resources-overview.md %}) for information about clusters, virtual machines, GPU infrastructure, and cloud solutions.
