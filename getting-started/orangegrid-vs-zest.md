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

## Our Two Clusters: Side by Side

<table>
<tr>
<td width="50%" style="background: #fff3e0; padding: 20px; border-left: 5px solid #F76900;">

<h3>OrangeGrid (HTCondor)</h3>

**High-Throughput Computing (HTC)**

**Best for:** Many independent jobs, parameter sweeps, batch processing, embarrassingly parallel workloads

**Scheduler:** HTCondor  
**Login:** `its-og-loginX.syr.edu`

**Key Commands:**
- Submit: `condor_submit job.sub`
- Status: `condor_q`
- Cancel: `condor_rm jobid`

**GPUs:** A100, L40S, A6000 (via SUrge)

**Examples:** Processing thousands of images, Monte Carlo simulations, batch data analysis, Ollama inference

💻 [OrangeGrid Code Examples](https://github.com/SyracuseUniversity/OrangeGridExamples)

</td>
<td width="50%" style="background: #e3f2fd; padding: 20px; border-left: 5px solid #2196F3;">

<h3>Zest (Slurm)</h3>

**High-Performance Computing (HPC)**

**Best for:** Parallel jobs, MPI, tightly-coupled computations, long-running workloads

**Scheduler:** Slurm  
**Login:** `its-zest-loginX.syr.edu`

**Key Commands:**
- Submit: `sbatch script.sh`
- Status: `squeue`
- Cancel: `scancel jobid`

**GPUs:** Primarily A40s (via SUrge)

**Examples:** GROMACS simulations, deep learning training, computational fluid dynamics, molecular dynamics

💻 [Zest Code Examples](https://github.com/SyracuseUniversity/ZestExamples)

</td>
</tr>
</table>

{: .note }
**Want more details?** See our [complete resource overview]({% link resources-overview.md %}) for information about all computing resources including clusters, virtual machines, and cloud solutions. For technical specifications, see [OrangeGrid Specifications]({% link resources/orangegrid-specifications.md %}) and [Zest Specifications]({% link resources/zest-specifications.md %}).

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
- 📧 Email us at [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
- We can discuss moving you to a different cluster if appropriate
- We can provide access to both clusters if your work spans different types
- We're here to ensure you always have the right tools
