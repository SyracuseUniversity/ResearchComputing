---
layout: default
title: SUrge (GPU Infrastructure)
parent: Resources Overview
nav_order: 3
---

# SUrge - GPU Infrastructure

**Type:** GPU Computing Cluster | **Scale:** Hundreds of GPUs

---

## What is SUrge?

SUrge is a growing computing cluster with **hundreds of GPUs** that provides GPU resources to both OrangeGrid and Zest clusters. It supports GPU-enabled applications and enables development with CUDA and OpenCL.

{: .important }
**SUrge is Infrastructure, Not Standalone Access**  
You don't request "SUrge access" directly. SUrge provides the GPU infrastructure that powers GPU computing on our clusters.

**To use SUrge GPUs:**
- Request cluster access (OrangeGrid or Zest)
- Submit GPU jobs through the cluster schedulers
- Your jobs automatically use SUrge GPU nodes when requesting GPUs

---

## GPU Hardware

**Available GPU Models (hundreds total):**
- **NVIDIA A100 (80GB)** - Top-tier compute GPUs
- **NVIDIA L40S (48GB)** - High-performance datacenter GPUs
- **NVIDIA A6000** - Workstation-class GPUs
- **NVIDIA A40** - Datacenter GPUs
- **NVIDIA RTX series** - Various models
- And other NVIDIA GPU models

---

## How SUrge Integrates with Clusters

### OrangeGrid + SUrge
- Submit HTCondor jobs requesting GPUs
- HTCondor scheduler assigns jobs to available SUrge GPU nodes
- Great for many independent GPU jobs (batch inference, parameter sweeps with GPUs)

**Request GPUs in submit file:**
```
+request_gpus = 1
```

### Zest + SUrge
- Submit Slurm jobs to GPU partitions
- Slurm scheduler allocates SUrge GPU nodes to your job
- Great for GPU-accelerated parallel jobs, multi-GPU training, long GPU workloads

**Request GPUs in SBATCH script:**
```bash
#SBATCH --partition=gpu_zone2,gpu
#SBATCH --gres=gpu:1
```

---

## Supported Applications

### CUDA and OpenCL Development
- NVIDIA CUDA toolkit available
- cuDNN for deep learning
- OpenCL for cross-platform GPU computing

### Common GPU Workloads
- Deep learning training (PyTorch, TensorFlow, JAX)
- LLM fine-tuning and inference
- Molecular dynamics (GPU-accelerated GROMACS, NAMD)
- Computer vision and image processing
- Scientific simulations with GPU acceleration
- Rendering and visualization

---

## GPU Job Examples

📁 [OrangeGrid GPU Examples](https://github.com/SyracuseUniversity/OrangeGridExamples) - PyTorch, TensorFlow, Ollama  
📁 [Zest GPU Examples](https://github.com/SyracuseUniversity/ZestExamples) - CUDA, GPU jobs

{: .note }
When you request cluster access and indicate GPU needs during consultation, we'll assign you to the appropriate cluster (OrangeGrid or Zest) based on your workflow. You'll then submit GPU jobs through that cluster's scheduler, and they'll run on SUrge GPU nodes.

📧 Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) to discuss GPU computing needs.
