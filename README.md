# Syracuse University Research Computing

Welcome to Syracuse University's Research Computing documentation hub! This is your central resource for computing clusters, GPU access, software environments, and research computing support.

> **New to research computing?** Start with our [Interactive Getting Started Guide](./getting-started/index.html) to learn the basics of cluster computing.

---

## 🚀 Quick Start

**Just got your cluster account?**
1. 📖 Read our [Getting Started Guide](./getting-started/)
2. 🔑 [Set up SSH keys](./access/ssh-keys.md) for easier login
3. 🎯 [Choose your cluster](./getting-started/choosing-a-cluster.md) (Zest or OrangeGrid)
4. ✅ Submit your [first job](./getting-started/first-job.md)

**Need GPUs?**
- 📧 Email us first: [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
- 📚 Read [GPU Resources Overview](./resources/gpu-resources.md)

**Looking for examples?**
- [Zest Examples Repository](https://github.com/SyracuseUniversity/ZestExamples) - Slurm job examples
- [OrangeGrid Examples Repository](https://github.com/SyracuseUniversity/OrangeGridExamples) - HTCondor job examples

---

## 📚 Documentation Sections

### Getting Started
Perfect for new users transitioning to cluster computing.

- [**Interactive vs. Batch Computing**](./getting-started/interactive-vs-batch.md) - Understanding the fundamental shift
- [**Python: Local vs. Cluster**](./getting-started/python-comparison.md) - See the difference with real examples
- [**Linux Command Line Basics**](./getting-started/linux-basics.md) - Essential commands you need
- [**Choosing Your Cluster**](./getting-started/choosing-a-cluster.md) - Zest vs. OrangeGrid
- [**Your First Job**](./getting-started/first-job.md) - Step-by-step walkthrough

### Cluster Documentation

#### Zest (Slurm)
High-Performance Computing cluster for parallel jobs, GPUs, and long-running workloads.

- [Connecting to Zest](./clusters/zest/connecting.md)
- [Slurm Commands & Basics](./clusters/zest/slurm-basics.md)
- [Job Submission Guide](./clusters/zest/job-submission.md)
- [GPU Jobs on Zest](./clusters/zest/gpu-jobs.md)
- [Available Modules (Lmod)](./clusters/zest/modules.md)
- [Partitions & Resources](./clusters/zest/partitions.md)
- [📁 Zest Code Examples](https://github.com/SyracuseUniversity/ZestExamples)

#### OrangeGrid (HTCondor)
High-Throughput Computing cluster for many independent jobs and batch processing.

- [Connecting to OrangeGrid](./clusters/orangegrid/connecting.md)
- [HTCondor Commands & Basics](./clusters/orangegrid/htcondor-basics.md)
- [Job Submission Guide](./clusters/orangegrid/job-submission.md)
- [GPU Jobs on OrangeGrid](./clusters/orangegrid/gpu-jobs.md)
- [Multiple Jobs & Arrays](./clusters/orangegrid/multiple-jobs.md)
- [📁 OrangeGrid Code Examples](https://github.com/SyracuseUniversity/OrangeGridExamples)

### Connection & Access
How to connect to clusters from anywhere.

- [**SSH Key Setup**](./access/ssh-keys.md) - Secure, password-free login
- [**Connecting from Off-Campus**](./access/off-campus.md) - RDS and VPN options
- [**Remote Desktop Services (RDS)**](./access/rds.md) - Windows environment for cluster access
- [**Azure VPN**](./access/azure-vpn.md) - Alternative connection method
- [**File Transfer**](./access/file-transfer.md) - SCP, WinSCP, and rsync

### Computing Resources
Understanding your computing options at Syracuse.

- [**GPU Resources**](./resources/gpu-resources.md) - Clusters, VMs, Azure, and Colab
- [**Azure for Research**](./resources/azure.md) - Cloud computing options
- [**Google Colab**](./resources/google-colab.md) - Development and prototyping
- [**Storage Options**](./resources/storage.md) - Where to keep your data
- [**Resource Comparison**](./resources/comparison.md) - Which option is right for you?

### Software & Environments
Installing and managing software on the clusters.

- [**Conda Environments**](./software/conda.md) - Python package management
- [**UV Package Manager**](./software/uv.md) - Modern Python packaging
- [**Singularity Containers**](./software/singularity.md) - Complex software stacks
- [**Available Modules**](./software/modules.md) - Pre-installed software (Lmod)
- [**Python Setup**](./software/python.md) - Virtual environments and packages
- [**R Setup**](./software/r.md) - Installing R packages
- [**Julia Setup**](./software/julia.md) - Julia environments

### Guides & How-Tos
Specific workflows and use cases.

- [**Machine Learning on Clusters**](./guides/machine-learning.md) - PyTorch, TensorFlow, GPU setup
- [**LLM Work**](./guides/llms.md) - Ollama, LlamaCPP, fine-tuning, inference
- [**Parallel Computing**](./guides/parallel-computing.md) - MPI jobs and multi-node work
- [**Long-Running Jobs**](./guides/long-jobs.md) - Checkpointing and job management
- [**Data Processing Pipelines**](./guides/pipelines.md) - Batch processing workflows
- [**Molecular Dynamics**](./guides/molecular-dynamics.md) - GROMACS and similar tools

### Support & Resources

- [**Getting Help**](./support/getting-help.md) - How to contact us
- [**FAQ**](./support/faq.md) - Common questions answered
- [**Troubleshooting**](./support/troubleshooting.md) - Solving common problems
- [**Workshops & Training**](./support/workshops.md) - Upcoming events
- [**External Resources**](./support/external-resources.md) - Slurm, HTCondor, and other docs

---

## 🎯 Common Tasks

### I need to...

**Submit a job**
- [Zest/Slurm job submission](./clusters/zest/job-submission.md)
- [OrangeGrid/HTCondor job submission](./clusters/orangegrid/job-submission.md)

**Use GPUs**
- [GPU Resources overview](./resources/gpu-resources.md)
- [GPU jobs on Zest](./clusters/zest/gpu-jobs.md)
- [GPU jobs on OrangeGrid](./clusters/orangegrid/gpu-jobs.md)

**Install Python packages**
- [Conda environments](./software/conda.md)
- [UV package manager](./software/uv.md)

**Run machine learning code**
- [Machine learning guide](./guides/machine-learning.md)
- [PyTorch examples](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/PyTorch)
- [TensorFlow examples](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/tensorflow)

**Work with LLMs**
- [LLM guide](./guides/llms.md)
- [Ollama examples](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Ollama)

**Connect from home**
- [Off-campus connection guide](./access/off-campus.md)
- [RDS setup](./access/rds.md)

**Transfer files**
- [File transfer guide](./access/file-transfer.md)

---

## 💡 What's Different About Cluster Computing?

Coming from a laptop or desktop? Here's what changes:

| **Your Laptop** | **The Cluster** |
|----------------|----------------|
| Click "Run" in Jupyter/RStudio | Write a submission script |
| See results immediately | Submit job to queue, check results later |
| Use all resources yourself | Share with hundreds of researchers |
| GUI and interactive tools | Command-line only, batch jobs |
| Install software freely | Use conda/containers |

**Why batch computing?** It enables:
- ✅ Sharing expensive resources fairly
- ✅ Running computations too large for any single computer
- ✅ Queuing hundreds of jobs to run automatically
- ✅ Accessing specialized hardware (GPUs, high-memory nodes)

Learn more in our [Interactive vs. Batch Computing guide](./getting-started/interactive-vs-batch.md).

---

## 🏫 Our Clusters at a Glance

### Zest (Slurm)
**High-Performance Computing**

- **Best for:** Parallel jobs, MPI, GPUs, long runtimes
- **Scheduler:** Slurm
- **Resources:** Multiple partitions, GPU nodes (A40, A100), high-memory nodes
- **Max runtime:** 20-40 days
- **Submit command:** `sbatch script.sh`
- **Examples:** [ZestExamples](https://github.com/SyracuseUniversity/ZestExamples)

### OrangeGrid (HTCondor)
**High-Throughput Computing**

- **Best for:** Many independent jobs, parameter sweeps, batch processing
- **Scheduler:** HTCondor
- **Resources:** Large pool of CPU and GPU nodes
- **Max runtime:** Varies by job
- **Submit command:** `condor_submit job.sub`
- **Examples:** [OrangeGridExamples](https://github.com/SyracuseUniversity/OrangeGridExamples)

Not sure which to use? See our [cluster comparison guide](./getting-started/choosing-a-cluster.md).

---

## 📞 Getting Help

### Request Cluster Access
Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) with:
- Your research project description
- Which cluster you need (or let us help you decide)
- Your advisor/PI information (if applicable)

### Technical Support
Have questions or issues?
- 📧 **Email:** [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
- 📖 **Check:** [FAQ](./support/faq.md) and [Troubleshooting](./support/troubleshooting.md)
- 💬 **Attend:** Our [workshops and office hours](./support/workshops.md)

### Report Issues
Found a bug in the documentation? [Open an issue](https://github.com/SyracuseUniversity/ResearchComputing/issues) or submit a pull request!

---

## 🔗 Quick Links

### Essential URLs
- 🌐 [Research Computing Website](https://researchcomputing.syr.edu)
- 📧 [Email Support](mailto:researchcomputing@syr.edu)
- 📅 [Events & Workshops](https://researchcomputing.syr.edu/events/)

### Code Examples
- [Zest Examples](https://github.com/SyracuseUniversity/ZestExamples)
- [OrangeGrid Examples](https://github.com/SyracuseUniversity/OrangeGridExamples)

### External Documentation
- [Slurm Documentation](https://slurm.schedmd.com/)
- [HTCondor Documentation](https://htcondor.readthedocs.io/)
- [Singularity User Guide](https://docs.sylabs.io/guides/latest/user-guide/)

---

## 🎓 Learning Path for New Users

**Week 1: Basics**
1. Read [Getting Started Guide](./getting-started/)
2. [Set up SSH keys](./access/ssh-keys.md)
3. Learn [Linux basics](./getting-started/linux-basics.md)
4. Submit your [first simple job](./getting-started/first-job.md)

**Week 2: Your Research**
1. [Choose your cluster](./getting-started/choosing-a-cluster.md)
2. Set up [software environment](./software/) (conda/singularity)
3. Adapt one of our [examples](https://github.com/SyracuseUniversity/ZestExamples) to your code
4. Submit a real research job

**Week 3: Optimization**
1. Learn about [GPU resources](./resources/gpu-resources.md) (if needed)
2. Optimize job parameters
3. Set up efficient workflows
4. Attend a [workshop](./support/workshops.md)

---

## 📜 About This Documentation

This documentation is maintained by the Syracuse University Research Computing team. We welcome contributions, corrections, and suggestions!

- **Repository:** [github.com/SyracuseUniversity/ResearchComputing](https://github.com/SyracuseUniversity/ResearchComputing)
- **Last Updated:** February 2026
- **Contributing:** See [CONTRIBUTING.md](./CONTRIBUTING.md)

---

<div align="center">

**Syracuse University Research Computing**

*Empowering research through advanced computing resources*

[Website](https://researchcomputing.syr.edu) | [Email](mailto:researchcomputing@syr.edu) | [Events](https://researchcomputing.syr.edu/events/)

</div>
