---
layout: default
title: Zest (HPC)
parent: Resources Overview
nav_order: 2
has_children: true
---

# Zest - High-Performance Computing

**Cluster Type:** High-Performance Computing (HPC) | **Scheduler:** Slurm

---

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

---

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

---

## Partitions

| Partition | Purpose | Max Runtime |
|:----------|:--------|:------------|
| normal (default) | CPU-intensive workloads | 20 days |
| compute_zone2 | CPU-intensive workloads | 20 days |
| longjobs | Extended runtime needs | 40 days |
| gpu, gpu_zone2 | GPU computations | 20 days |

---

## How It Works

Submit jobs using Slurm batch scripts:

1. Create your SBATCH script with resource requests
2. Submit with `sbatch script.sh`
3. Slurm schedules based on availability and priority
4. Job runs on allocated compute nodes
5. Results saved to your home directory

---

## Typical Use Cases

- Molecular dynamics simulations (GROMACS, NAMD)
- Deep learning model training with GPUs
- Computational fluid dynamics
- Multi-node parallel computations (MPI)
- Weather/climate modeling
- Finite element analysis

---

## Learn More

📊 [Zest Technical Specifications](zest-specifications)  
💻 [Zest Code Examples](https://github.com/SyracuseUniversity/ZestExamples){:target="_blank"}
