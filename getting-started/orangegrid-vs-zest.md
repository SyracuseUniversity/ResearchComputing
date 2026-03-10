---
layout: default
title: OrangeGrid vs. Zest
parent: Getting Started
nav_order: 4
---

# OrangeGrid vs. Zest: Understanding Your Cluster

Syracuse University operates two computing clusters, each optimized for different types of computational work. Your welcome email specifies which cluster you've been assigned based on your research needs.

{: .highlight }
**Your Home Directory:** By default, you have a **4TB home directory** at `/home/netid/`. This NetApp-based storage is automatically mounted on all compute nodes when your jobs run. Use it for scripts, code, data, conda environments, and results. You can also create scratch directories within your home (like `~/scratch/`) for temporary files during computations.

---

## OrangeGrid (HTCondor) - High-Throughput Computing

**Scheduler:** HTCondor  
**Login:** `its-og-loginX.syr.edu`

**Best for:** Many independent jobs, parameter sweeps, batch processing, embarrassingly parallel workloads

**Key Commands:**
- Submit: `condor_submit job.sub`
- Status: `condor_q`
- Cancel: `condor_rm jobid`

**GPUs:** A100, L40S, A6000 (via SUrge)

**Examples:** Processing thousands of images, Monte Carlo simulations, batch data analysis, Ollama inference

[OrangeGrid Code Examples](https://github.com/SyracuseUniversity/OrangeGridExamples){:target="_blank"}

---

## Zest (Slurm) - High-Performance Computing

**Scheduler:** Slurm  
**Login:** `its-zest-loginX.syr.edu`

**Best for:** Parallel jobs, MPI, tightly-coupled computations, long-running workloads

**Key Commands:**
- Submit: `sbatch script.sh`
- Status: `squeue`
- Cancel: `scancel jobid`

**GPUs:** Primarily A40s (via SUrge)

**Examples:** GROMACS simulations, deep learning training, computational fluid dynamics, molecular dynamics

[Zest Code Examples](https://github.com/SyracuseUniversity/ZestExamples){:target="_blank"}

---

{: .note }
**Want more details?** See our [complete resource overview](../resources-overview) for information about all computing resources. For technical specifications, see [OrangeGrid Specifications](../resources/orangegrid-specifications) and [Zest Specifications](../resources/zest-specifications).

---

## Quick Command Comparison

| Task | OrangeGrid (HTCondor) | Zest (Slurm) |
|:-----|:----------------------|:-------------|
| Submit job | `condor_submit job.sub` | `sbatch script.sh` |
| Check status | `condor_q netid` | `squeue -u netid` |
| Cancel job | `condor_rm jobid` | `scancel jobid` |
| View resources | `condor_status` | `sinfo` |
| Job history | `condor_history` | `sacct` |

---

## What If My Needs Change?

Research evolves! If your computational needs change:
- Email us at [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
- We can discuss moving you to a different cluster if appropriate
- We can provide access to both clusters if your work spans different types
- We're here to ensure you always have the right tools
