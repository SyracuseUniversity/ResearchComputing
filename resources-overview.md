---
layout: default
title: Resources Overview
nav_order: 3
has_children: true
---

# Syracuse Research Computing Resources

{: .highlight }
> **Consultation-Based Resource Assignment**  
> We don't offer à la carte services. Instead, we work with you to understand your research needs and match you to the optimal computing solution. This ensures you have the right resources, proper support, and meet any compliance requirements.  
> **📧 Start here:** [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

---

## Our Computing Resources

Syracuse Research Computing provides a range of computing resources to support diverse research needs:

- **OrangeGrid**, a high-throughput computing (HTC) cluster
- **Zest**, a high-performance computing (HPC) cluster
- **Academic Virtual Hosting Environment** (AVHE), a private cloud focused on the unique needs of the research community
- **Crush**, a virtual private cloud for computationally intense research computing needs
- **SUrge**, a growing computing cluster with hundreds of GPUs, supporting GPU enabled applications and allowing development with CUDA and OpenCL

Through our continued partnerships, we also support research computing needs in the cloud, including Microsoft Azure.

---

## Resource Comparison

| Resource | Type | Cost | Best For |
|:---------|:-----|:-----|:---------|
| **OrangeGrid** | HTC Cluster | No charge | Many independent jobs |
| **Zest** | HPC Cluster | No charge | Parallel, multi-node jobs |
| **SUrge** | GPU Infrastructure | No charge | Provides GPUs to clusters |
| **AVHE** | Private Cloud | No charge | CPU VMs, unique research needs |
| **Crush** | Private Cloud | No charge | Intense computing, dynamic solutions |
| **Cloud (Azure)** | Cloud Partnership | Usage-based cost | Specific needs, cloud services |

{: .warning }
**Data Sensitivity & Compliance Requirements**  
Before requesting resources, tell us about your data:
- **Sensitive data?** HIPAA, FERPA, controlled exports, or other regulated data
- **Grant requirements?** Many funding sources have specific data security agreements
- **Compliance needs?** IRB approvals, data use agreements, export controls
  
Data sensitivity requirements significantly impact which computing resources are appropriate and how we configure your access. Some resources cannot be used for certain data types. We need this information during your consultation to ensure compliance and proper resource selection.

---

## What We Need to Know

When requesting computing resources, provide information about:

### Computational Requirements
- **CPU needs:** How many cores? Parallel or independent jobs?
- **Memory needs:** How much RAM per job?
- **Storage needs:** How much data? How long to keep it?
- **GPU needs:** What type of work? How many GPUs?
- **Runtime:** Minutes, hours, days, or weeks per job?

### Data & Compliance Requirements
- **Data sensitivity level:** Public, restricted, controlled?
- **Compliance requirements:** HIPAA, FERPA, ITAR, CUI, etc.?
- **Grant-specific agreements:** NIH, NSF, DOD data requirements?
- **IRB or data use agreements:** Any restrictions on data handling?

### Workflow Information
- **Software/tools:** What will you be running?
- **Interactivity needs:** Batch-friendly or requires GUI?
- **Timeline:** When do you need results?
- **Scale:** One-time analysis or ongoing research?

---

# OrangeGrid - High-Throughput Computing

**Cluster Type:** High-Throughput Computing (HTC) | **Scheduler:** HTCondor

## What is OrangeGrid?

OrangeGrid is Syracuse University's largest computing cluster with **over 80,000 cores**, optimized to perform a large number of parallel jobs and provide high processing capacity over extended periods. The cluster utilizes a mixture of dedicated and scavenged compute nodes managed by HTCondor.

{: .note }
**Best For:**
- Many independent jobs (hundreds to thousands)
- Parameter sweeps and batch processing
- Embarrassingly parallel workloads
- Single-node high-memory or GPU jobs
- LLM inference across multiple inputs

## Technical Overview

**Scale:** Over 80,000 cores across heterogeneous pool of compute nodes

**CPU Architecture:**
- Mix of AMD and Intel processors
- Varying core counts and configurations
- Opportunistic scheduling matches jobs to available resources

**GPU Capabilities:**
- GPU nodes available through SUrge infrastructure
- Models include: NVIDIA A100, L40S, A6000, and others
- Request with `+request_gpus = 1` in submit files
- Best for single-node GPU jobs (training, inference, rendering)

**Job Characteristics:**
- Single-node jobs (one job per machine)
- High-core count available (up to 64+ cores per node on some machines)
- High-memory nodes available (256GB+ on select nodes)
- Fair-share scheduling across all users

**Storage:** 4TB home directory (default), NetApp-based, automatically mounted on compute nodes

**Access:** SSH via `its-og-loginX.syr.edu`

## How It Works

Submit jobs using HTCondor submit files. Each job runs independently on an available node in the pool:

1. Create your script and HTCondor submit file
2. Submit with `condor_submit job.sub`
3. HTCondor matches your job to available resources
4. Job runs when resources become available
5. Results saved to your home directory

## Typical Use Cases

- Processing thousands of images with the same pipeline
- Running parameter sweeps for optimization studies
- LLM inference or fine-tuning across multiple datasets
- Batch data analysis (R, Python, Julia)
- Rendering farms (Blender, etc.)
- Monte Carlo or stochastic simulations

📚 **Learn More:**
- [OrangeGrid Technical Specifications]({% link resources/orangegrid-specifications.md %})
- [OrangeGrid Code Examples](https://github.com/SyracuseUniversity/OrangeGridExamples)

---

# Zest - High-Performance Computing

**Cluster Type:** High-Performance Computing (HPC) | **Scheduler:** Slurm

## What is Zest?

Zest is Syracuse University's high-performance computing cluster with **over 25,000 cores**, designed for research work that requires tying together multiple compute nodes or cannot be split into smaller components. Compute nodes are interconnected with InfiniBand to pass information between nodes with much lower latency than Ethernet.

{: .note }
**Best For:**
- Multi-node parallel jobs (MPI)
- Tightly-coupled computations requiring fast interconnect
- Large-scale parallel workloads (hundreds of cores)
- GPU-accelerated research
- Long-running jobs (up to 40 days)
- High-memory workloads

## Technical Overview

**Scale:** Over 25,000 cores with InfiniBand interconnect

**Architecture:**
- Traditional HPC cluster with uniform compute nodes
- InfiniBand fabric for low-latency node-to-node communication
- Optimized for MPI and parallel workloads
- Multiple partitions for different workload types

**Job Capabilities:**
- Multi-node jobs (scale across dozens or hundreds of nodes)
- MPI parallel computing with fast interconnect
- High core count (hundreds of cores per job)
- High-memory configurations available
- Extended runtimes (20-40 days depending on partition)

**GPU Capabilities:**
- GPU nodes available through SUrge infrastructure
- Primarily NVIDIA A40 GPUs
- Request with `--gres=gpu:1` in SBATCH scripts
- GPU partitions available for accelerated computing

**Storage:** 4TB home directory (default), NetApp-based, automatically mounted on all compute nodes

**Access:** SSH via `its-zest-loginX.syr.edu`

## Partitions

| Partition | Purpose | Max Runtime |
|:----------|:--------|:------------|
| normal (default) | CPU-intensive workloads | 20 days |
| compute_zone2 | CPU-intensive workloads | 20 days |
| longjobs | Extended runtime needs | 40 days |
| gpu, gpu_zone2 | GPU computations | 20 days |

## Typical Use Cases

- Molecular dynamics simulations (GROMACS, NAMD)
- Deep learning model training with GPUs
- Computational fluid dynamics
- Multi-node parallel computations (MPI)
- Weather/climate modeling
- Finite element analysis

📚 **Learn More:**
- [Zest Technical Specifications]({% link resources/zest-specifications.md %})
- [Zest Code Examples](https://github.com/SyracuseUniversity/ZestExamples)

---

# SUrge - GPU Infrastructure

**Type:** GPU Computing Cluster | **Scale:** Hundreds of GPUs

## What is SUrge?

SUrge is a growing computing cluster with **hundreds of GPUs** that provides GPU resources to both OrangeGrid and Zest clusters. It supports GPU-enabled applications and enables development with CUDA and OpenCL.

{: .important }
**SUrge is Infrastructure, Not Standalone Access**  
You don't request "SUrge access" directly. SUrge provides the GPU infrastructure that powers GPU computing on our clusters.  
**To use SUrge GPUs:** Request cluster access (OrangeGrid or Zest), submit GPU jobs through the cluster schedulers, and your jobs automatically use SUrge GPU nodes when requesting GPUs.

## GPU Hardware

**Available GPU Models (hundreds total):**
- NVIDIA A100 (80GB) - Top-tier compute GPUs
- NVIDIA L40S (48GB) - High-performance datacenter GPUs
- NVIDIA A6000 - Workstation-class GPUs
- NVIDIA A40 - Datacenter GPUs
- NVIDIA RTX series - Various models
- And other NVIDIA GPU models

## How SUrge Integrates with Clusters

**OrangeGrid + SUrge:**
- Submit HTCondor jobs requesting GPUs
- HTCondor scheduler assigns jobs to available SUrge GPU nodes
- Great for many independent GPU jobs (batch inference, parameter sweeps with GPUs)

**Zest + SUrge:**
- Submit Slurm jobs to GPU partitions
- Slurm scheduler allocates SUrge GPU nodes to your job
- Great for GPU-accelerated parallel jobs, multi-GPU training, long GPU workloads

## Supported Applications

**CUDA and OpenCL development:**
- NVIDIA CUDA toolkit available
- cuDNN for deep learning
- OpenCL for cross-platform GPU computing

**Common GPU workloads:**
- Deep learning training (PyTorch, TensorFlow, JAX)
- LLM fine-tuning and inference
- Molecular dynamics (GPU-accelerated GROMACS, NAMD)
- Computer vision and image processing
- Scientific simulations with GPU acceleration
- Rendering and visualization

{: .note }
When you request cluster access and indicate GPU needs during consultation, we'll assign you to the appropriate cluster (OrangeGrid or Zest) based on your workflow. You'll then submit GPU jobs through that cluster's scheduler, and they'll run on SUrge GPU nodes.

📧 Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) to discuss GPU computing needs.

---

# Academic Virtual Hosting Environment (AVHE)

**Type:** Private Cloud | **Cost:** No charge to researchers

## What is AVHE?

The Academic Virtual Hosting Environment (AVHE) is a private cloud focused on the unique needs of the research community. It uses virtualization to provide flexibility and hardware sharing, allowing multiple researchers to operate on underlying server and storage infrastructure. This lowers the entry barrier for small to medium-sized research efforts.

{: .note }
**What AVHE Supports:**
- Traditional and non-traditional computational research
- CPU-only virtual machines (Linux and Windows)
- Small to medium-sized clustered research environments
- Persistent environments for long-running services
- Medium-scale storage for research data and archives

## Key Features

**Virtualization Benefits:**
- High availability with automatic workload migration on hardware failure
- Flexible resource allocation
- Multiple researchers can share underlying infrastructure
- Backup services provided to all researchers

**Platform Options:**
- Linux VMs (various distributions)
- Windows VMs
- Custom configurations based on research needs

**Storage:**
- Medium-scale storage included
- Research data storage and archiving supported
- Over 3 petabytes of research data currently hosted
- Backup services available

## When AVHE is Appropriate

- Small to medium-sized research projects
- CPU-only computational needs
- Workflows requiring persistent, dedicated environments
- Building custom research computing environments
- Applications not suitable for batch cluster submission

**Access & Support:** AVHE VMs are assigned based on consultation. If assigned an AVHE VM, you'll receive specific IP address for SSH access, configuration details, and setup guidance.

{: .warning }
**Data Compliance:** AVHE environments can be configured to meet various compliance requirements. Discuss data sensitivity needs during your consultation to ensure proper security configurations.

---

# Crush - Virtual Private Cloud

**Type:** Virtual Private Cloud | **Cost:** No charge to researchers

## What is Crush?

Crush is a virtual private cloud for computationally intense research computing needs. This infrastructure supports both our research clusters and provides dynamic solutions for specialized research requirements that extend beyond standard cluster configurations.

{: .note }
**What Crush Supports:**
- Cluster infrastructure: Provides compute resources that power OrangeGrid and Zest
- Dynamic solutions: Custom configurations for intense computational needs
- Specialized workloads: Research that requires tailored environments
- Flexible resource allocation: Solutions matched to unique research workflows

## Capabilities

Crush enables us to provide flexible computing resources that support both standard cluster operations and specialized research needs:

- Computationally intense workloads with high-performance configurations
- Large memory environments exceeding standard cluster nodes
- Specialized GPU access when specific configurations are needed
- Custom software stacks requiring specific configurations
- Long-running services and persistent computational environments

## Resource Assignment

Crush-based solutions are determined collaboratively during consultation based on research requirements. We assess whether standard cluster resources meet your needs, or if a Crush-based dynamic solution is more appropriate.

If assigned Crush-based resources, you'll receive specific access details and configuration guidance based on your research needs.

{: .warning }
Crush resources are assigned based on specific research requirements that cannot be met by our standard cluster offerings. Contact [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) to discuss your needs.

---

# Azure Cloud Partnership

## Cloud Computing Through Microsoft Azure

Through our continued partnership with Microsoft Azure, we can support research computing needs in the cloud. This option is available for specific scenarios where on-premises resources don't align with research requirements.

{: .warning }
**Usage-Based Cost**  
Cloud computing involves usage-based costs that will be billed to your project. You'll work with our business office to set up billing arrangements. Costs vary based on resources used (compute time, storage, data transfer, etc.).

{: .note }
**When Cloud Solutions Are Appropriate:**
- Specific timelines: Project deadlines that can't accommodate cluster queue times
- Dedicated resources: Need guaranteed access for extended periods
- Azure-specific services: Research requires Azure ML, specific cloud APIs, or integrations
- Grant-funded cloud work: Project budget specifically includes cloud computing
- Scalability beyond on-prem: Temporary need for resources beyond our infrastructure

## What Azure Offers

- **Compute VMs:** On-demand virtual machines with various configurations
- **GPU instances:** High-end NVIDIA GPUs available
- **Azure ML:** Machine learning platform and services
- **Scalable storage:** Blob storage, file shares, managed databases
- **Specialized services:** Various Azure cloud services for research

## Cost Considerations

**Important factors:**
- Charged by usage (compute hours, storage, data transfer)
- Costs can scale quickly with continuous use
- Budget planning required
- Business office coordination for billing

**Cost comparison:** For most workloads, our clusters provide substantially more computational capacity at no direct charge than equivalent cloud spending would deliver. We'll help analyze whether cloud is cost-effective for your specific needs.

## Getting Started with Azure

During your consultation, we'll review:
1. Whether cloud computing is appropriate for your research
2. Estimated costs based on your requirements
3. Funding source and budget availability
4. Business office billing setup process
5. Alternative on-premises options that may better suit your needs

{: .highlight }
**Interested in Cloud Computing?**  
Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) with:
- Your research project and timeline
- Why you're considering cloud computing
- Your funding source and budget
- Computational requirements (CPU, GPU, storage)

We'll schedule a consultation to review options and help determine if cloud computing is the right fit - or if our on-premises resources can meet your needs.

---

# Requesting Computing Resources

Access to Syracuse Research Computing resources begins with a consultation. This ensures you're matched to the right resource and that we understand any compliance or data security requirements.

## The Consultation Process

```
📧 1. Email us at researchcomputing@syr.edu
         ↓
🤝 2. We schedule a consultation (remote or in-person)
         ↓
💬 3. We discuss your research, computational needs, and data requirements
         ↓
🎯 4. We recommend the optimal resource(s) for your work
         ↓
✅ 5. We set up your account with appropriate access and configurations
         ↓
🚀 6. We support you with examples, documentation, and troubleshooting
```

## What to Include in Your Request

### Research Overview
- Brief description of your research project
- Your department and PI/advisor (if applicable)
- Timeline for when you need to start computing
- Funding source (if requesting cloud resources)

### Computational Requirements

Help us understand your computing needs:
- **CPUs:** How many cores? One big job or many small jobs?
- **Memory:** How much RAM per job? (e.g., 8GB, 64GB, 256GB)
- **Storage:** How much data? How long to keep it?
- **GPUs:** Do you need GPUs? For what type of work?
- **Runtime:** Minutes, hours, days, or weeks per job?
- **Quantity:** One job at a time or hundreds/thousands?

*It's okay if you don't know exact numbers! We'll help you figure this out during consultation.*

### Data Sensitivity & Compliance (Critical!)

{: .warning }
**We must know about any data sensitivity or compliance requirements upfront.**

**Tell us if your data involves:**
- **Protected health information (PHI):** HIPAA requirements
- **Student data:** FERPA requirements
- **Export-controlled data:** ITAR, EAR restrictions
- **Controlled unclassified information (CUI):** Federal data requirements
- **Personally identifiable information (PII):** Privacy requirements
- **Grant-specific requirements:** NIH, NSF, DOD data agreements

**Why this is critical:**
- Different resources have different security configurations
- Some data types cannot be used on certain resources
- Compliance violations can affect your research and the university
- We need to configure appropriate access controls and logging

**When in doubt, tell us!** We'd rather discuss data requirements that turn out not to be applicable than miss critical compliance needs.

### Workflow & Software Information
- What software or tools will you use? (Python, R, MATLAB, custom code, etc.)
- Do you need interactive access or can work be batch-submitted?
- Are there specific software licensing requirements?
- Have you used HPC/HTC clusters before?

## Sample Request Email

**To:** [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)  
**Subject:** Research Computing Resource Request

```
Hi Research Computing Team,

I'm requesting access to research computing resources for my project.

Research Overview:
Project: [Brief description of your research]
Department: [Your department]
PI/Advisor: [Name, if applicable]
Timeline: [When you need to start]

Computational Needs:
- CPUs: [e.g., 4 cores per job, running 100 jobs]
- Memory: [e.g., 16GB per job]
- Storage: [e.g., 500GB dataset]
- GPUs: [Yes/No - if yes, what for?]
- Runtime: [e.g., 6 hours per job]

Data Sensitivity:
- Sensitive data: [Yes/No - if yes, what type?]
- Compliance requirements: [HIPAA/FERPA/None/etc.]
- Grant data agreements: [Any specific requirements from funding source]
- IRB approval: [If working with human subjects data]

Software & Workflow:
- Software: [Python, R, TensorFlow, etc.]
- Batch-friendly: [Can your work be submitted as jobs?]
- Previous experience: [New to clusters / have used HPC before]

Looking forward to discussing the best computing solution for my research!

Best,
[Your name]
```

## What Happens Next?

1. **We'll respond within 1-2 business days** to schedule a consultation
2. **Consultation meeting** (typically 30-60 minutes, remote or in-person)
3. **We'll discuss:**
   - Your research workflow in detail
   - Data compliance and security needs
   - Computational requirements
   - Recommended resource(s)
   - Timeline for getting started
4. **Account setup** (typically 1-3 days after consultation)
5. **Welcome email** with login credentials and getting-started instructions
6. **Ongoing support** as you get up and running

{: .highlight }
**What Makes a Good Consultation**  
Come prepared to discuss: What you're trying to compute (not just what resources you think you need), your workflow from start to finish, any data sensitivity or compliance concerns, your timeline and pressure points, and previous computing experience. We'll help you match to the right resource, understand batch computing, optimize your workflow, meet compliance needs, and get started successfully.
