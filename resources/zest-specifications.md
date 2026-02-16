# Zest Cluster Specifications

Technical specifications for the Zest High-Performance Computing (HPC) cluster.

---

## Overview

**Scheduler:** Slurm  
**Type:** High-Performance Computing (HPC)  
**Best For:** Parallel jobs, MPI, GPU acceleration, long-running workloads  
**Access:** SSH via `its-zest-loginX.syr.edu` (X = your assigned login node)

---

## Partitions

Zest has multiple partitions optimized for different workloads. If no partition is specified, jobs use the **normal** partition by default.

| Partition | Purpose | Max Runtime | Default |
|-----------|---------|-------------|---------|
| **normal** | CPU-intensive workloads | 20 days | ✓ Yes |
| **compute_zone2** | CPU-intensive workloads | 20 days | |
| **longjobs** | Extended runtime workloads | 40 days | |
| **gpu** | GPU computations | 20 days | |
| **gpu_zone2** | GPU computations | 20 days | |

### Specifying Partitions in Job Scripts

```bash
# Single partition
#SBATCH --partition=gpu

# Multiple partitions (job will use first available)
#SBATCH --partition=gpu_zone2,gpu

# CPU partitions
#SBATCH --partition=compute_zone2,normal
```

---

## GPU Resources

### Available GPU Models

- **NVIDIA A40** - Primary GPU (most common)
- Other models may be available

### Requesting GPUs

**Basic GPU request:**
```bash
#SBATCH --partition=gpu_zone2,gpu
#SBATCH --gres=gpu:1
```

**Request specific GPU model (if required by your code):**
```bash
#SBATCH --partition=gpu_zone2,gpu
#SBATCH --gres=gpu:1
#SBATCH --constraint=gpu_type:A40
```

**Multiple GPUs:**
```bash
#SBATCH --gres=gpu:2
```

**Best Practice:** Only specify GPU model if your code requires it. Leaving it unspecified allows the scheduler to assign any available GPU, which can get your job running faster.

---

## CPU and Memory

### Requesting Resources

```bash
# Number of nodes
#SBATCH --nodes=1

# Tasks per node
#SBATCH --ntasks-per-node=20

# CPUs per task
#SBATCH --cpus-per-task=1

# Memory (specify M for megabytes or G for gigabytes)
#SBATCH --mem=4G              # Total memory per node
#SBATCH --mem-per-cpu=2G      # Memory per CPU
```

### Resource Limits

Check current node availability and specifications:
```bash
sinfo                    # Basic node information
sinfo -o "%n %c %m %f"  # Detailed: node, CPUs, memory, features
```

---

## Storage

### Home Directory
- **Path:** `/home/netid/`
- **Type:** NFS-based
- **Accessibility:** Available throughout the cluster
- **Use for:** Scripts, code, small data files, conda environments

### Job Temporary Storage
- **Path:** `/tmp/`
- **Type:** Fast local storage on compute node
- **Persistence:** Only during job runtime
- **Use for:** Large temporary files, scratch space during computation
- **Warning:** Files in `/tmp/` are deleted when job ends

### Best Practices
- Store code and small data in `/home/`
- Use `/tmp/` for large temporary files during job execution
- Clean up `/tmp/` at end of job if generating many files
- For very large datasets, contact [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) about storage options

---

## Available Software

### Using Lmod Modules

Zest uses Lmod for managing software environments.

```bash
# List all available modules
module avail

# Search for specific module
module spider python

# Load a module
module load anaconda3

# List currently loaded modules
module list

# Unload a module
module unload anaconda3

# Unload all modules
module purge
```

### Commonly Used Modules

| Module | Version | Description |
|--------|---------|-------------|
| anaconda3 | 2023.9 | Python environment (Conda) |
| cuda | 12.3 | NVIDIA CUDA libraries |
| openmpi4 | 4.1.6 | MPI implementation |
| gromacs | 2023.2 | Molecular dynamics |
| singularity | 3.7.1 | Container runtime |
| gnu12 | 12.3.0 | GNU compiler family |

For a complete up-to-date list, use `module spider` on the cluster.

---

## Job Submission Limits

### Runtime Limits
- **normal, compute_zone2, gpu, gpu_zone2:** 20 days maximum
- **longjobs:** 40 days maximum

### Resource Recommendations
- Start with conservative estimates
- Monitor first few jobs to optimize requests
- Under-requesting memory will cause job failures
- Over-requesting resources means longer queue times

---

## Checking Cluster Status

```bash
# View partition and node information
sinfo

# View your jobs
squeue -u netid

# View all jobs in a partition
squeue -p gpu

# Detailed node information
scontrol show nodes

# Job accounting information
sacct

# Detailed job information
scontrol show job <jobid>
```

---

## Common Job Patterns

### Basic CPU Job
```bash
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G
#SBATCH --time=02:00:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=netid@syr.edu

module load anaconda3
python my_script.py
```

### GPU Job
```bash
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=10
#SBATCH --mem=32G
#SBATCH --partition=gpu_zone2,gpu
#SBATCH --gres=gpu:1
#SBATCH --time=1-00:00:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=netid@syr.edu

module load cuda
module load anaconda3
python train_model.py
```

### MPI Parallel Job
```bash
#!/bin/bash
#SBATCH --nodes=4
#SBATCH --ntasks-per-node=20
#SBATCH --cpus-per-task=1
#SBATCH --time=12:00:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=netid@syr.edu

module load openmpi4
mpirun my_parallel_program
```

---

## External Resources

- [Slurm Quick Start Guide](https://slurm.schedmd.com/quickstart.html)
- [Slurm Command Cheat Sheet (PDF)](https://slurm.schedmd.com/pdfs/summary.pdf)
- [Slurm Job Array Guide](https://slurm.schedmd.com/job_array.html)
- [ZestExamples Repository](https://github.com/SyracuseUniversity/ZestExamples)

---

## Getting Help

Questions about Zest specifications or optimal job configuration?

📧 Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
