---
layout: default
title: Home
nav_order: 1
description: "Syracuse University Research Computing documentation hub"
permalink: /
---

# Syracuse Research Computing Documentation

Welcome! This is your central hub for Syracuse University's research computing resources, including computing clusters, GPU access, software environments, and support.

---

## 🚀 New to Research Computing?

{: .highlight }
> **Need computing resources?** Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) to request a consultation. **Accounts are not active by default** - all access begins with consultation to ensure proper resource assignment and compliance with data sensitivity requirements.

{: .note }
**Just received credentials?** Start with our [Getting Started Guide]({% link getting-started.md %}) to learn the basics of cluster computing.

---

## 📖 What's Different About Research Computing?

Coming from a laptop or desktop? Research clusters work differently:

| Your Laptop | Research Cluster |
|:------------|:-----------------|
| Click "Run" in Jupyter/IDE | Write submission script |
| See results immediately | Submit to queue, check later |
| Use all resources yourself | Share with hundreds of users |
| GUI tools work | Command-line only |
| Install software freely | Use conda/containers/modules |
| Pick your own hardware | We match you to the right resource |

**Why batch computing?**
- Fair resource sharing among researchers
- Running jobs too large for any single computer
- Queuing hundreds of jobs automatically
- Accessing specialized hardware (GPUs, high-memory nodes)

**Why consultation?**
- You get the right resource for your needs
- Data sensitivity and compliance requirements are met
- Your workflow matches the resource capabilities
- You have the best support and examples for your platform

---

## 🖥️ Our Computing Resources

We operate two research computing clusters, private cloud environments, GPU infrastructure, and support cloud partnerships:

- **OrangeGrid** - High-throughput computing cluster (over 80,000 cores)
- **Zest** - High-performance computing cluster (over 25,000 cores)
- **SUrge** - GPU infrastructure (hundreds of GPUs supporting both clusters)
- **AVHE** - Private cloud for unique research needs
- **Crush** - Virtual private cloud for computationally intense needs
- **Azure** - Cloud partnership for specific use cases

See our complete [Resources Overview]({% link resources-overview.md %}) to understand all options.

{: .warning }
**Data Sensitivity & Compliance:** Tell us about data requirements upfront! Many grants have specific data security agreements (HIPAA, FERPA, export controls, etc.). This significantly impacts which resources are appropriate.

---

## 📊 Cluster Specifications

### OrangeGrid (HTCondor)

**Scale:** Over 80,000 cores | **Scheduler:** HTCondor

**Best for:** Many independent jobs, parameter sweeps, batch processing, single-node GPU jobs

**Resources:**
- AMD and Intel processors
- High-memory nodes available
- GPU nodes: A100, L40S, A6000 (via SUrge)
- Storage: 4TB home directory (default)

**Key commands:**
- Submit: `condor_submit job.sub`
- Status: `condor_q netid`
- Cancel: `condor_rm jobid`

📊 [Detailed specifications]({% link resources/orangegrid-specifications.md %})

### Zest (Slurm)

**Scale:** Over 25,000 cores with InfiniBand | **Scheduler:** Slurm

**Best for:** Multi-node parallel jobs, MPI, tightly-coupled work, long runtimes

**Resources:**
- InfiniBand interconnect for fast node-to-node communication
- Multiple partitions (20-40 day max runtime)
- GPU nodes: A40 (via SUrge)
- Storage: 4TB home directory (default)

**Key commands:**
- Submit: `sbatch script.sh`
- Status: `squeue -u netid`
- Cancel: `scancel jobid`

📊 [Detailed specifications]({% link resources/zest-specifications.md %})

---

## 💻 Code Examples

Ready-to-use job scripts and examples:

- [**OrangeGrid Examples**](https://github.com/SyracuseUniversity/OrangeGridExamples) - Python, PyTorch, Ollama, R, Julia, and more
- [**Zest Examples**](https://github.com/SyracuseUniversity/ZestExamples) - Python, MPI, GPU jobs, GROMACS

Clone to your cluster home:
```bash
git clone https://github.com/SyracuseUniversity/OrangeGridExamples.git
git clone https://github.com/SyracuseUniversity/ZestExamples.git
```

---

## ❓ Common Tasks

**Submit a job:**
- OrangeGrid: `condor_submit job.sub`
- Zest: `sbatch script.sh`

**Check job status:**
- OrangeGrid: `condor_q netid`
- Zest: `squeue -u netid`

**Cancel a job:**
- OrangeGrid: `condor_rm jobid`
- Zest: `scancel jobid`

**Use GPUs:**
- OrangeGrid: Add `+request_gpus = 1` to submit file
- Zest: Add `#SBATCH --gres=gpu:1` to script

**Transfer files:**
```bash
# Small files
scp file.txt netid@cluster:~/path/

# Large files (resumable)
rsync -avz --progress /local/data/ netid@cluster:~/data/
```

**For large data transfers (TBs):** Contact [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) for optimized options.

---

## 📞 Getting Help

### Request Access
📧 Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) with:
- Brief description of your research
- What you're trying to compute
- **Data sensitivity or compliance requirements** (HIPAA, FERPA, grant agreements, etc.)
- Your department and PI/advisor

We'll schedule a consultation to match you to the right resource.

### Technical Support
- 📧 Email: [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
- 📅 Events: [Workshops and office hours](https://researchcomputing.syr.edu/events/)

### External Documentation
- [Slurm Documentation](https://slurm.schedmd.com/)
- [HTCondor Documentation](https://htcondor.readthedocs.io/)
- [Singularity User Guide](https://docs.sylabs.io/guides/latest/user-guide/)
