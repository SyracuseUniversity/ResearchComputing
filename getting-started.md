---
layout: default
title: Getting Started
nav_order: 2
has_children: true
permalink: /getting-started
---

# Getting Started with Syracuse Research Computing

{: .note }
**You've been assigned a cluster account!** This guide will help you transition from interactive computing to batch computing on your assigned resource. Check your welcome email for your specific login information.

---

## What You'll Learn

- The fundamental difference between interactive and batch computing
- How to work in a Linux command-line environment  
- Understanding OrangeGrid vs Zest clusters
- How to connect and submit your first computational job
- Managing software with conda, UV, and Singularity

{: .warning }
**CRITICAL: Login Nodes vs. Compute Nodes**  
The login node is NOT where your work runs. When you SSH in, you're on a shared login node used by all researchers to submit jobs. Login nodes are ONLY for: light text editing, creating conda/UV environments, testing singularity containers load, submitting jobs, and checking job status. Do NOT run computational code, install software outside conda/UV/singularity, use IDEs, leave tmux sessions running, or keep unused SSH connections open. Your work runs on dedicated compute nodes after you submit it as a job. Need a development environment? Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

---

## How to Use This Guide

Navigate through sections using the left sidebar. Suggested path:

1. **Interactive vs. Batch** - Understand the fundamental shift
2. **Python Comparison** - See concrete examples
3. **Linux Basics** - Essential commands (skip if familiar)
4. **OrangeGrid vs Zest** - Understand your assigned cluster
5. **Connecting** - Get connected and learn file transfers
6. **Software** - Set up environments
7. **First Job** - Submit your first job

{: .note }
**Want to understand all our computing options?** See our [complete resource overview]({% link resources-overview.md %}), which includes information about clusters, virtual machines, and cloud solutions.
