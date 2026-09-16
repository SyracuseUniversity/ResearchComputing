---
layout: default
title: GPU Computing
parent: Resources Overview
nav_order: 3
redirect_from:
  - /resources/surge
  - /resources/surge.html
---

# GPU Computing

**Hundreds of NVIDIA GPUs** | **Available in OrangeGrid and Zest** | **No separate access request**

---

{: .important }
Research Computing at Syracuse University provides hundreds of GPUs to our computing clusters. **Note that there is no separate GPU cluster.** Our GPUs are compute nodes inside OrangeGrid and dedicated partitions in Zest. There is no need to request "GPU access" on its own. If you require GPUs for your computations work, simply request [access to a cluster](https://docs.syr.edu/ResearchComputing/resources/requesting-access.html), then simply request GPUs in your job submissions. If you already have an OrangeGrid or Zest account, you can submit GPU jobs today!

---

## What Is Available

The bulk of our GPUs are in OrangeGrid, with a smaller pool in Zest. Both clusters are free to use for faculty-sponsored research.

| Cluster | GPU model | GPU memory | Scheduler | Notes |
|:--------|:----------|:-----------|:----------|:------|
| **OrangeGrid** | NVIDIA H100 80GB HBM3 | 80 GB | HTCondor | 16 GPUs across 2 nodes, NVLink within a node, **3-day runtime cap** |
| | NVIDIA A100 80GB PCIe | 80 GB | HTCondor | |
| | NVIDIA L40S | 48 GB | HTCondor | |
| | NVIDIA A40 | 48 GB | HTCondor | |
| | Quadro RTX 6000 | 24 GB | HTCondor | Good fit for inference and smaller models |
| | Quadro RTX 5000 | 16 GB | HTCondor | |
| **Zest** | NVIDIA A40 | 48 GB | Slurm | `gpu` and `gpu_zone2` partitions, up to 4 GPUs per job, 20-day runtime limit |  

{: .note }
**H100 nodes** are our scarcest resource and demand is high. Jobs on them are capped at three days of runtime. Request them only when you are ready to use them, and checkpoint anything that runs longer than a day. See the [Checkpointing example](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/Checkpointing){:target="_blank"}.

---

## Which Cluster for GPU Work?

Your welcome email tells you which cluster you have been assigned. If you are not yet a user, this is what we consider during consultation.

| Your workload | Cluster | Why |
|:--------------|:--------|:----|
| Many independent GPU jobs (batch inference, hyperparameter sweeps, per-dataset fine-tuning) | **OrangeGrid** | Largest GPU pool, jobs run as soon as any matching GPU is free |
| Single-node training or fine-tuning, including multi-GPU on one node | **OrangeGrid** | H100 and A100 nodes with NVLink between GPUs on the same node |
| LLM inference with Ollama or similar | **OrangeGrid** | Working examples, wide choice of GPU memory sizes |
| Multi-node GPU jobs communicating over MPI | **Zest** | InfiniBand interconnect, Slurm multi-node support |
| GPU job that also needs many CPU cores or a long guaranteed runtime | **Zest** | 20-day runtime limit, uniform nodes |

Most GPU users are on OrangeGrid. If your needs change, email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) and we can add access to the other cluster.

---

## Requesting GPUs in a Job

### OrangeGrid (HTCondor)

A GPU job needs **two** lines in the submit file. Both are required.

```htcondor
Requirements = TotalGPUS > 0
+request_gpus = 1
```  
{: .note }
The first line restricts your job to nodes that have GPUs. The second tells HTCondor how many you need. 
**If you have no requirements line, your job can land on a CPU node and silently run without a GPU. Leave off the `+` and your job may sit idle indefinitely.**

To target GPU memory or compute capability, extend the `Requirements` line:

```htcondor
# At least 40 GB of GPU memory
Requirements = CUDAGlobalMemoryMb >= 40000
+request_gpus = 1
```

Full details, common mistakes, and how to diagnose an idle GPU job are in the [OrangeGrid GPU Resources](orangegrid-specifications#gpu-resources) section.

### Zest (Slurm)

Request a GPU partition and the number of GPUs:

```bash
#SBATCH --partition=gpu_zone2,gpu
#SBATCH --gres=gpu:1

module load cuda
```

Listing both partitions lets Slurm use whichever has a free GPU first. You can request up to four GPUs with `--gres=gpu:4` if your code can use them. See [Zest GPU Resources](zest-specifications#gpu-resources) for details.

---

## Working Examples

We have complete, tested job scripts you can copy and adapt in our [OrangeGridExamples](https://github.com/SyracuseUniversity/OrangeGridExamples){:target="_blank"} and [ZestExamples](https://github.com/SyracuseUniversity/ZestExamples){:target="_blank"} repositories. 

---

## CUDA and GPU Software

- **You choose your CUDA version on OrangeGrid.** Install the CUDA runtime your code needs into a Conda or pip environment (for example a `+cu128` PyTorch build). It will work with the drivers on any OrangeGrid GPU node, so do not add a CUDA driver version requirement to your job.
- **CUDA 13 and newer** need one extra compatibility package. Follow the [CUDA13 example](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/CUDA13){:target="_blank"}.
- **On Zest, use CUDA 12 builds.** Pick the CUDA 12 variant of your framework (for example PyTorch's `cu126` wheel, or `tensorflow[and-cuda]` and `jax[cuda12]`, which already are). `module load cuda` provides the CUDA 12 toolkit for compiling. See the [Zest GPU example](https://github.com/SyracuseUniversity/ZestExamples/tree/main/GPU){:target="_blank"}.
- **Containers** (Apptainer/Singularity) with GPU support run on both clusters. See the [Apptainer example](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/Apptainer){:target="_blank"}.
- **Common frameworks**: PyTorch, TensorFlow, JAX, Ollama, vLLM, GROMACS, NAMD, LAMMPS with Kokkos, Octave, Blender.

---

## Good GPU Citizenship

GPUs are the most contended resource we have. A few habits keep them available for everyone:

- **Request only the GPUs you can use.** A job that asks for two GPUs but uses one blocks a GPU for someone else.
- **Request capabilities, not models.** Asking for `CUDAGlobalMemoryMb >= 40000` matches more nodes and starts sooner than asking for a specific card.
- **Do not claim a GPU before you are ready.** Idle time on a claimed GPU is the single most disruptive thing on our scarcest hardware.
- **Do not remove idle jobs just to resubmit them.** Queue waits are normal under fair-share scheduling, and resubmitting does not move you forward.
- **Checkpoint long jobs.** Hardware failures and runtime caps happen. A checkpointed job resumes; an unchecked one starts over.

The full [Good Neighbor Policy]({% link good-neighbor-policy.md %}) applies to GPU nodes as it does everywhere else.

---

## Getting Access

GPU access comes with cluster access. Follow the [Requesting Access](requesting-access) process and tell us:

- What you are running (training, inference, simulation, rendering)
- Roughly how much GPU memory your model or dataset needs
- Whether jobs are independent or need to talk to each other
- How long a single job runs

We will place you on the right cluster and point you to a working example that matches your workflow.

Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) with any GPU questions.
