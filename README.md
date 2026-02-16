# Syracuse University Research Computing

Welcome to Syracuse University's Research Computing documentation hub! This is your central resource for computing clusters, GPU access, software environments, and research computing support.

> **New to research computing?** Start with our [Interactive Getting Started Guide](./getting-started/index.html) to learn the basics of cluster computing.

---

## 🚀 Quick Start

**New to Research Computing at Syracuse?**
1. 📧 **Request access:** Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
2. 🤝 **Consultation:** We'll schedule a meeting to discuss your research needs
3. 🎯 **Get matched:** We'll assign you to the right computing resource
4. 📖 **Get started:** Follow the guide for your assigned resource

**Just received your account credentials?**
1. 📖 Read our [Getting Started Guide](./getting-started/)
2. 🔑 [Set up SSH keys](./access/ssh-keys.md) for easier login
3. 📚 Review documentation for your assigned resource (Zest, OrangeGrid, etc.)
4. ✅ Submit your [first job](./getting-started/first-job.md)

**Looking for code examples?**
- [Zest Examples Repository](https://github.com/SyracuseUniversity/ZestExamples) - Slurm job examples
- [OrangeGrid Examples Repository](https://github.com/SyracuseUniversity/OrangeGridExamples) - HTCondor job examples

---

## 📚 Documentation Sections

### Getting Started
Perfect for new users transitioning to cluster computing.

- [**Interactive vs. Batch Computing**](./getting-started/interactive-vs-batch.md) - Understanding the fundamental shift
- [**Python: Local vs. Cluster**](./getting-started/python-comparison.md) - See the difference with real examples
- [**Linux Command Line Basics**](./getting-started/linux-basics.md) - Essential commands you need
- [**Understanding Your Assigned Resource**](./getting-started/understanding-resources.md) - What you've been given and why
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
Understanding the resources available at Syracuse.

> **Note:** Resources are assigned based on consultation with our team. We match you to the best option for your research needs.

- [**Resource Overview**](./resources/overview.md) - All computing options explained
- [**Cluster Computing**](./resources/clusters.md) - Zest (HPC) and OrangeGrid (HTC)
- [**Custom Virtual Machines**](./resources/custom-vms.md) - AVHE and Crush environments
- [**Azure Cloud Computing**](./resources/azure.md) - Paid cloud options
- [**GPU Resources**](./resources/gpu-resources.md) - Where and how to access GPUs
- [**Google Colab**](./resources/google-colab.md) - Development and prototyping
- [**Storage Options**](./resources/storage.md) - Where to keep your data

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

**Get access to computing resources**
- [Request access via consultation](./support/getting-help.md#request-computing-resources)
- Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

**Submit a job**
- [Zest/Slurm job submission](./clusters/zest/job-submission.md)
- [OrangeGrid/HTCondor job submission](./clusters/orangegrid/job-submission.md)

**Understand my assigned resource**
- [Understanding Your Resource](./getting-started/understanding-resources.md)
- [Resource Overview](./resources/overview.md)

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

## 💡 What's Different About Research Computing?

Coming from a laptop or desktop? Here's what changes:

| **Your Laptop** | **Research Computing** |
|----------------|----------------|
| Click "Run" in Jupyter/RStudio | Write a submission script |
| See results immediately | Submit job to queue, check results later |
| Use all resources yourself | Share with hundreds of researchers |
| GUI and interactive tools | Command-line only, batch jobs |
| Install software freely | Use conda/containers |
| Pick your own hardware | We match you to the right resource |

**Why batch computing?** It enables:
- ✅ Sharing expensive resources fairly
- ✅ Running computations too large for any single computer
- ✅ Queuing hundreds of jobs to run automatically
- ✅ Accessing specialized hardware (GPUs, high-memory nodes)

**Why consultation?** We ensure:
- ✅ You get the right resource for your needs (not too little, not too much)
- ✅ You don't pay for cloud resources when free clusters will work
- ✅ Your workflow matches the resource capabilities
- ✅ You have the best support and examples for your platform

Learn more in our [Interactive vs. Batch Computing guide](./getting-started/interactive-vs-batch.md).

---

## 🏫 Our Computing Resources

We offer multiple computing resources to match different research needs. **During your consultation, we'll help determine which resource is best for your work.**

### Zest - High-Performance Computing (HPC)

- **Best for:** Parallel jobs, MPI, GPUs, long runtimes, tightly-coupled computations
- **Scheduler:** Slurm
- **Resources:** Multiple partitions, GPU nodes (A40, A100), high-memory nodes
- **Max runtime:** 20-40 days
- **Submit command:** `sbatch script.sh`
- **Examples:** [ZestExamples](https://github.com/SyracuseUniversity/ZestExamples)

### OrangeGrid - High-Throughput Computing (HTC)

- **Best for:** Many independent jobs, parameter sweeps, batch processing
- **Scheduler:** HTCondor
- **Resources:** Large pool of CPU and GPU nodes
- **Max runtime:** Varies by job
- **Submit command:** `condor_submit job.sub`
- **Examples:** [OrangeGridExamples](https://github.com/SyracuseUniversity/OrangeGridExamples)

### Custom Virtual Machines

**AVHE Environment**
- CPU-only VMs for specific use cases
- Persistent environment with more control
- Assigned based on research requirements

**Crush Environment**
- Larger VMs with optional GPU support
- For workloads requiring dedicated resources
- Interactive or long-running services

### Azure Cloud Computing (Paid)

- On-demand cloud resources through Microsoft Azure
- Best for dedicated GPU needs or specific timelines
- Requires working with business office for billing
- Cost-effective for certain research scenarios

**Not sure what you need?** That's exactly why we start with a consultation! Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) to discuss your research.

---

## 📞 Getting Help

### Request Computing Resources
**Start here if you're new or need access:**

📧 Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) with:
- Brief description of your research project
- What you're trying to compute (simulations, data processing, machine learning, etc.)
- Any specific requirements you know about (GPUs, large memory, long runtimes)
- Your department and advisor/PI (if applicable)

**What happens next:**
1. We'll schedule a consultation meeting (remote or in-person)
2. We'll discuss your workflow and computing needs
3. We'll recommend the best resource for your work
4. We'll set up your account and provide getting-started guidance

**No need to know which resource you need!** That's our job. We'll match you to the right solution.

### Technical Support
Already have access and need help?
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

**Before You Have Access**
1. Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) to request consultation
2. Prepare to discuss your research needs in the meeting
3. We'll recommend the right resource and set up your account

**Week 1: Getting Started**
1. Receive your account credentials via email
2. Read [Getting Started Guide](./getting-started/) for your assigned resource
3. [Set up SSH keys](./access/ssh-keys.md)
4. Learn [Linux basics](./getting-started/linux-basics.md) (if needed)
5. Submit your [first simple job](./getting-started/first-job.md)

**Week 2: Your Research**
1. Review [examples](https://github.com/SyracuseUniversity/ZestExamples) for your platform
2. Set up [software environment](./software/) (conda/singularity/modules)
3. Adapt an example to your code
4. Submit a real research job

**Week 3: Optimization**
1. Learn about [GPU resources](./resources/gpu-resources.md) (if you have GPU access)
2. Optimize job parameters for efficiency
3. Set up efficient workflows
4. Attend a [workshop](./support/workshops.md) to learn advanced techniques

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
