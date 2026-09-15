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
**There is no separate GPU cluster.** Our GPUs are compute nodes inside OrangeGrid and Zest. You do not request "GPU access" on its own. You request access to a cluster, then ask for GPUs in your job submission. If you already have an OrangeGrid or Zest account, you can submit GPU jobs today.

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

The pool changes as hardware is added. To see what is currently available:

```bash
# OrangeGrid: one line per GPU node with GPU count, model, and memory in MB
condor_status -constraint 'TotalGPUs > 0' -af Machine TotalGPUs CUDADeviceName CUDAGlobalMemoryMb | sort -u

# Zest: GPU nodes, GPUs per node, and whether each node is idle, mixed, or allocated
sinfo -p gpu,gpu_zone2 -N -o "%n %G %T"
```

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

The first line restricts your job to nodes that have GPUs. The second tells HTCondor how many you need. Leave out the first and your job can land on a CPU node and silently run without a GPU. Leave off the `+` and your job will sit idle forever.

To target GPU memory or compute capability, extend the `Requirements` line:

```htcondor
# At least 40 GB of GPU memory
Requirements = TotalGPUS > 0 && CUDAGlobalMemoryMb >= 40000
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

These are complete, tested job scripts you can copy and adapt.

**OrangeGrid** ([OrangeGridExamples](https://github.com/SyracuseUniversity/OrangeGridExamples){:target="_blank"})
- [PyTorch](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/PyTorch){:target="_blank"} - Conda environment, GPU detection, training on a single GPU
- [Ollama](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/Ollama){:target="_blank"} - LLM inference in a container on a GPU node
- [tensorflow](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/tensorflow){:target="_blank"} - TensorFlow GPU job
- [JAX](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/JAX){:target="_blank"} - JIT-compiled numerics, multi-GPU data distribution
- [CUDA13](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/CUDA13){:target="_blank"} - Running a newer CUDA than the node driver provides
- [Checkpointing](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/Checkpointing){:target="_blank"} - Save and resume long GPU jobs
- [blender](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/blender){:target="_blank"} - GPU rendering

**Zest** ([ZestExamples](https://github.com/SyracuseUniversity/ZestExamples){:target="_blank"})
- [GPU](https://github.com/SyracuseUniversity/ZestExamples/tree/main/GPU){:target="_blank"} - Submit to the GPU partitions and verify the GPU with `nvidia-smi`
- [GROMACS](https://github.com/SyracuseUniversity/ZestExamples/tree/main/GROMACS){:target="_blank"} - GPU-accelerated molecular dynamics

---

## CUDA and GPU Software

- **You choose your CUDA version on OrangeGrid.** Install the CUDA runtime your code needs into a Conda or pip environment (for example a `+cu128` PyTorch build). It will work with the drivers on any OrangeGrid GPU node, so do not add a CUDA driver version requirement to your job.
- **CUDA 13 and newer** need one extra compatibility package. Follow the [CUDA13 example](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/CUDA13){:target="_blank"}.
- **On Zest, use CUDA 12 builds.** Pick the CUDA 12 variant of your framework (for example PyTorch's `cu126` wheel, or `tensorflow[and-cuda]` and `jax[cuda12]`, which already are). `module load cuda` provides the CUDA 12 toolkit for compiling. See the [Zest GPU example](https://github.com/SyracuseUniversity/ZestExamples/tree/main/GPU){:target="_blank"}.
- **Containers** (Apptainer/Singularity) with GPU support run on both clusters. See the [Apptainer example](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/Examples/Apptainer){:target="_blank"}.
- **Common frameworks**: PyTorch, TensorFlow, JAX, Ollama, vLLM, GROMACS, NAMD, LAMMPS with Kokkos, MATLAB with Parallel Computing Toolbox, Blender.

See [Software & Environments]({% link getting-started/software.md %}) for setting up Conda environments.

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
