# Syracuse University Research Computing Documentation

Welcome to Syracuse University's Research Computing documentation. This repository provides comprehensive guides for using our computing resources, clusters, and support services.

---

## 🚀 Quick Start

### Need Computing Resources?

**📧 Request Access:** Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

Tell us about your research and we'll schedule a consultation to match you to the right resource (clusters, VMs, or cloud). No prior experience needed - we'll guide you through everything!

### Just Received Your Credentials?

**📖 Start Here:** [Getting Started Guide](./getting-started.html)

Your welcome email contains login information and instructions specific to your assigned resource. The getting started guide will walk you through:
- Understanding batch computing vs. interactive work
- Connecting to your resource
- Linux command-line basics
- Submitting your first job
- Software environments (conda, singularity)

### Looking for Something Specific?

Jump directly to what you need:
- [🖥️ Computing Resources Overview](https://syracuseuniversity.github.io/ResearchComputing/resources-overview.html) - All available resources explained
- [📊 Cluster Specifications](#cluster-specifications) - CPUs, GPUs, partitions, limits
- [💻 Code Examples](#code-examples) - Ready-to-use job scripts
- [❓ Common Tasks](#common-tasks) - Quick command reference

---

## Cluster Specifications

Technical details for our HTC and HPC clusters.

### OrangeGrid (HTCondor) - High-Throughput Computing

**Cluster Type:** Large pool of CPU and GPU nodes for many independent jobs

**Best For:**
- Parameter sweeps and batch processing
- Many independent jobs (hundreds to thousands)
- Embarrassingly parallel workloads
- LLM inference across multiple inputs

**Available GPUs:**
- NVIDIA A100, L40S, A6000, and other models
- Request with `+request_gpus = 1`

**Storage:**
- Home directory: `/home/netid/` (accessible from submit nodes)
- Job-specific data transferred as specified in submit files

**Job Limits:**
- Varies by workload and availability
- Fair-share scheduling across all users

📊 **Detailed specifications:** [OrangeGrid Technical Details](./resources/orangegrid-specifications.md)

### Zest (Slurm) - High-Performance Computing

**Cluster Type:** High-performance computing cluster with over 25,000 cores and InfiniBand interconnect

**Best For:**
- Multi-node parallel jobs (MPI)
- Tightly-coupled computations requiring fast interconnect
- Large-scale parallel workloads (hundreds of cores)
- GPU-accelerated research
- Long-running jobs (up to 40 days)
- High-memory workloads

**Partitions & Runtimes:**

| Partition | Purpose | Max Runtime | Default |
|-----------|---------|-------------|---------|
| normal | CPU-intensive workloads | 20 days | ✓ Yes |
| compute_zone2 | CPU-intensive workloads | 20 days | |
| longjobs | Extended runtime workloads | 40 days | |
| gpu | GPU computations | 20 days | |
| gpu_zone2 | GPU computations | 20 days | |

**Available GPUs:**
- NVIDIA A40 (primary, via SUrge)
- Other models available - use constraints to specify

**Storage:**
- Home directory: `/home/netid/` (NetApp, mounted on all nodes at job start)
- Create scratch directories within your home for temporary job files

**Resources:**
- Over 25,000 cores interconnected with InfiniBand
- Use `sinfo` command for current node availability
- Multiple partitions optimized for different workloads

📊 **Detailed specifications:** [Zest Technical Details](./resources/zest-specifications.md)

---

## Code Examples

Ready-to-use examples for common tasks.

### OrangeGrid Examples
[📁 OrangeGridExamples Repository](https://github.com/SyracuseUniversity/OrangeGridExamples)

- Basic HTCondor submission (hostname, simple scripts)
- Python jobs (conda, UV package manager)
- PyTorch and TensorFlow (GPU training)
- LLM work (Ollama, LlamaCPP)
- R and Julia examples
- Multiple job submission and arrays
- Parallelism patterns
- Blender rendering

### Zest Examples
[📁 ZestExamples Repository](https://github.com/SyracuseUniversity/ZestExamples)

- Basic Slurm job submission (hostname, simple scripts)
- Python jobs (anaconda, conda environments)
- GPU jobs (PyTorch, TensorFlow, CUDA)
- MPI parallel jobs
- GROMACS molecular dynamics
- Checkpointing long jobs

---

## Documentation

### Interactive Guides
Comprehensive, navigable tutorials with everything you need.

- [**Getting Started Guide**](https://syracuseuniversity.github.io/ResearchComputing/getting-started.html) - Complete tutorial for new cluster users (batch computing, Linux basics, connecting, first jobs)
- [**Resources Overview**](https://syracuseuniversity.github.io/ResearchComputing/resources-overview.html) - All computing resources explained (OrangeGrid, Zest, SUrge, AVHE, Crush, Azure)

### Cluster Technical Specifications

- [OrangeGrid Specifications](./resources/orangegrid-specifications.md) - Pool details, GPUs, job submission
- [Zest Specifications](./resources/zest-specifications.md) - Partitions, InfiniBand, GPUs, modules

### Additional Documentation
Additional guides and documentation pages will be added here as they are created. For now, the interactive guides above cover everything new users need to get started.

---

## Common Tasks

**Submit a job:**
- Zest: `sbatch script.sh` - [Job submission guide](./clusters/zest/job-submission.md)
- OrangeGrid: `condor_submit job.sub` - [Job submission guide](./clusters/orangegrid/job-submission.md)

**Check job status:**
- Zest: `squeue -u netid` - [Slurm commands](./clusters/zest/slurm-commands.md)
- OrangeGrid: `condor_q netid` - [HTCondor commands](./clusters/orangegrid/htcondor-commands.md)

**Cancel a job:**
- Zest: `scancel jobid`
- OrangeGrid: `condor_rm jobid`

**Install Python packages:**
- [Create conda environment](./software/conda.md)
- [Use UV package manager](./software/uv.md)

**Use GPUs:**
- Zest: Add `#SBATCH --gres=gpu:1` to script - [GPU guide](./clusters/zest/gpu-jobs.md)
- OrangeGrid: Add `+request_gpus = 1` to submit file - [GPU guide](./clusters/orangegrid/gpu-jobs.md)

**Transfer files:**
- `scp file.txt netid@cluster:~/path/` - [File transfer guide](./access/file-transfer.md)

**Load software modules** (Zest only):
- `module avail` - see available modules
- `module load anaconda3` - [Modules guide](./software/modules.md)

---

## Understanding Batch Computing

Coming from a laptop or desktop? Here's what's different:

| Your Laptop | Research Cluster |
|-------------|------------------|
| Click "Run" in Jupyter/IDE | Write submission script |
| See results immediately | Submit to queue, check later |
| Use all resources yourself | Share with hundreds of users |
| GUI tools work | Command-line only |
| Install software freely | Use conda/containers/modules |

**Why batch?** It enables:
- Fair resource sharing among researchers
- Running jobs too large for any single computer
- Queuing hundreds of jobs automatically
- Accessing specialized hardware (GPUs, high-memory nodes)

Learn more in the [Getting Started Guide](./getting-started.html).

---

## Quick Reference

### Zest Commands
```bash
sbatch script.sh          # Submit job
squeue -u netid           # Check your jobs
scancel jobid             # Cancel job
sinfo                     # View node info
sacct                     # Job accounting
module avail              # Available software
```

### OrangeGrid Commands
```bash
condor_submit job.sub     # Submit job
condor_q netid            # Check your jobs
condor_rm jobid           # Cancel job
condor_status             # View pool
condor_userprio           # See priorities
```

### Essential Linux
```bash
pwd                       # Where am I?
ls -la                    # List files
cd directory              # Change directory
nano file.txt             # Edit file
cp file1 file2            # Copy file
mv old new                # Move/rename
rm file                   # Delete file
```

---

## Getting Help

### Request Access
📧 Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) with:
- Brief description of your research
- What you're trying to compute
- **Data sensitivity or compliance requirements** (HIPAA, FERPA, grant agreements, etc.)
- Any specific requirements (GPUs, long runtime, large storage, etc.)
- Your department and PI/advisor

We'll schedule a consultation to match you to the right resource and ensure compliance needs are met.

### Technical Support
Already have access and need help?
- 📧 Email: [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
- 📖 Check the [Getting Started Guide](https://syracuseuniversity.github.io/ResearchComputing/getting-started.html) for common topics
- 💬 Attend workshops and office hours (see [Events page](https://researchcomputing.syr.edu/events/))

### Found an Issue?
Documentation problem or suggestion? [Open an issue](https://github.com/SyracuseUniversity/ResearchComputing/issues) or submit a pull request!

---

## Additional Resources

### Syracuse Links
- 🌐 [Research Computing Website](https://researchcomputing.syr.edu)
- 📅 [Events & Workshops](https://researchcomputing.syr.edu/events/)
- 📧 [Email Support](mailto:researchcomputing@syr.edu)

### External Documentation
- [Slurm Documentation](https://slurm.schedmd.com/)
- [Slurm Cheat Sheet PDF](https://slurm.schedmd.com/pdfs/summary.pdf)
- [HTCondor Documentation](https://htcondor.readthedocs.io/)
- [HTCondor Quick Start](https://htcondor.readthedocs.io/en/latest/users-manual/quick-start-guide.html)
- [Singularity User Guide](https://docs.sylabs.io/guides/latest/user-guide/)

---

## About This Documentation

Maintained by Syracuse University Research Computing. We welcome contributions!

**Last Updated:** February 2026  
**Repository:** [github.com/SyracuseUniversity/ResearchComputing](https://github.com/SyracuseUniversity/ResearchComputing)  
**Contributing:** See [CONTRIBUTING.md](./CONTRIBUTING.md)

---

**Syracuse University Research Computing**

*Empowering research through advanced computing resources*

[Website](https://researchcomputing.syr.edu) • [Email](mailto:researchcomputing@syr.edu) • [Events](https://researchcomputing.syr.edu/events/)
