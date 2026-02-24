---
layout: default
title: OrangeGrid (HTC)
parent: Resources Overview
nav_order: 1
has_children: true
---

# OrangeGrid - High-Throughput Computing

**Cluster Type:** High-Throughput Computing (HTC) | **Scheduler:** HTCondor

---

## What is OrangeGrid?

OrangeGrid is Syracuse University's largest computing cluster with **over 80,000 cores**, optimized to perform a large number of parallel jobs and provide high processing capacity over extended periods. The cluster utilizes a mixture of dedicated and scavenged compute nodes managed by HTCondor.

{: .note }
**Best For:**
- Many independent jobs (hundreds to thousands)
- Parameter sweeps and batch processing
- Embarrassingly parallel workloads
- Single-node high-memory or GPU jobs
- LLM inference across multiple inputs

---

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

---

## How It Works

Submit jobs using HTCondor submit files. Each job runs independently on an available node in the pool:

1. Create your script and HTCondor submit file
2. Submit with `condor_submit job.sub`
3. HTCondor matches your job to available resources
4. Job runs when resources become available
5. Results saved to your home directory

---

## Typical Use Cases

- Processing thousands of images with the same pipeline
- Running parameter sweeps for optimization studies
- LLM inference or fine-tuning across multiple datasets
- Batch data analysis (R, Python, Julia)
- Rendering farms (Blender, etc.)
- Monte Carlo or stochastic simulations

---

## Learn More

📊 [OrangeGrid Technical Specifications](orangegrid-specifications)  
💻 [OrangeGrid Code Examples](https://github.com/SyracuseUniversity/OrangeGridExamples){:target="_blank"}
