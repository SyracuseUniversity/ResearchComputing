---
layout: default
title: Home
nav_order: 1
permalink: /
---

![Syracuse Research Computing](https://researchcomputing.syr.edu/wp-content/uploads/cropped-waveform-700x441.jpg)

# Syracuse Research Computing Documentation

Welcome! This is your central hub for Syracuse University's research computing resources, including computing clusters, GPU access, software environments, and support.

---

## 🚀 Quick Start

**Need Computing Resources?**

📧 **Request Access:** Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

Tell us about your research, computational needs, and any data sensitivity requirements. We'll schedule a consultation to match you to the right resource. 

**Accounts are not active by default** - all access begins with consultation to ensure proper resource assignment and compliance.

**[📝 Complete request guide - What to include in your email →](resources/requesting-access)**

**Our Resources:** We operate two research computing clusters (OrangeGrid and Zest), private cloud environments (AVHE and Crush), GPU infrastructure (SUrge), and support cloud partnerships. Learn more in our [complete resource overview](resources-overview).

---

**Just Received Your Credentials?**

📖 **Start Here:** [Getting Started Guide](getting-started)

Your welcome email contains login information and instructions specific to your assigned resource.

---

**Looking for Something Specific?**

- [🖥️ Computing Resources Overview](resources-overview)
- [📊 OrangeGrid Specs](resources/orangegrid-specifications) | [📊 Zest Specs](resources/zest-specifications)
- [💻 OrangeGrid Examples](https://github.com/SyracuseUniversity/OrangeGridExamples){:target="_blank"} | [💻 Zest Examples](https://github.com/SyracuseUniversity/ZestExamples){:target="_blank"}

---

## 💡 What's Different About Research Computing?

Coming from a laptop or desktop? Research clusters work differently:

| Your Laptop | Research Cluster |
|:------------|:-----------------|
| Click "Run" in Jupyter/IDE | Write submission script |
| See results immediately | Submit to queue, check later |
| Use all resources yourself | Share with hundreds of users |
| GUI tools work | Command-line only |
| Install software freely | Use conda/containers/modules |
| Pick your own hardware | We match you to the right resource |

**Why batch computing?** It enables fair resource sharing, running jobs too large for any single computer, queuing hundreds of jobs automatically, and accessing specialized hardware.

**Why consultation?** We ensure you get the right resource, data sensitivity requirements are met, your workflow matches the resource capabilities, and you have the best support.

{: .warning }
**Data Sensitivity & Compliance:** Tell us about data requirements upfront! Many grants have specific data security agreements (HIPAA, FERPA, export controls, etc.). This significantly impacts which resources are appropriate.

---

## 🖥️ Our Computing Resources

We operate two research computing clusters, private cloud environments, GPU infrastructure, and support cloud partnerships:

- **OrangeGrid** - High-throughput computing cluster (over 80,000 cores)
- **Zest** - High-performance computing cluster (over 25,000 cores)
- **SUrge** - GPU infrastructure (hundreds of GPUs)
- **AVHE** & **Crush** - Private clouds
- **Azure** - Cloud partnership

[View complete resource overview →](resources-overview)

---

## 📊 Cluster Quick Reference

### OrangeGrid (HTCondor)

**Scale:** Over 80,000 cores | **Scheduler:** HTCondor | **Access:** `its-og-loginX.syr.edu`

**Best for:** Many independent jobs, parameter sweeps, batch processing

**Key commands:**
```bash
condor_submit job.sub     # Submit job
condor_q netid            # Check status
condor_rm jobid           # Cancel job
```

**GPUs:** A100, L40S, A6000 (via SUrge) - Request with `+request_gpus = 1`

[OrangeGrid Details →](resources/orangegrid) | [Technical Specs →](resources/orangegrid-specifications)

### Zest (Slurm)

**Scale:** Over 25,000 cores with InfiniBand | **Scheduler:** Slurm | **Access:** `its-zest-loginX.syr.edu`

**Best for:** Multi-node parallel, MPI, tightly-coupled work, long runtimes

**Key commands:**
```bash
sbatch script.sh          # Submit job
squeue -u netid           # Check status
scancel jobid             # Cancel job
```

**GPUs:** A40 (primary, via SUrge) - Request with `#SBATCH --gres=gpu:1`

[Zest Details →](resources/zest) | [Technical Specs →](resources/zest-specifications)

---

## 💻 Code Examples

Ready-to-use job scripts:

- [**OrangeGrid Examples**](https://github.com/SyracuseUniversity/OrangeGridExamples){:target="_blank"} - Python, PyTorch, Ollama, R, Julia
- [**Zest Examples**](https://github.com/SyracuseUniversity/ZestExamples){:target="_blank"} - Python, MPI, GPU jobs, GROMACS

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

**Request Access:**  
📧 Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) with your research description, computational needs, and any data sensitivity requirements.

[Complete request guide →](resources/requesting-access)

**Technical Support:**
- 📧 Email: [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
- 📅 Events: [Workshops and office hours](https://researchcomputing.syr.edu/events/){:target="_blank"}

**External Documentation:**
- [Slurm Documentation](https://slurm.schedmd.com/){:target="_blank"}
- [HTCondor Documentation](https://htcondor.readthedocs.io/){:target="_blank"}
- [Singularity User Guide](https://docs.sylabs.io/guides/latest/user-guide/){:target="_blank"}
