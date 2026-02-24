---
layout: default
title: Software & Environments
parent: Getting Started
nav_order: 6
---

# Software & Environments

How to install and manage software on the clusters.

{: .warning }
**Critical Information:** You cannot install software directly on the clusters. Instead, use:
- **Conda** or **UV** for Python packages
- **Singularity** containers for complex dependencies

**Acceptable on login nodes:** Creating and setting up these environments (light configuration work).  
**NOT acceptable on login nodes:** Testing or running code after installation. Once your environment is set up, submit a job to test it!

---

## Using Conda Environments

Conda lets you create isolated Python environments with the packages you need.

### On Zest

```bash
# Load the Anaconda module
module load anaconda3

# Create a new environment
conda create -n myenv python=3.11

# Activate it
conda activate myenv

# Install packages
conda install numpy pandas scikit-learn
pip install your-package-here
```

### Using in Job Scripts (Zest)

```bash
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks=1

module load anaconda3
conda activate myenv

python my_script.py
```

### On OrangeGrid

Conda works similarly, but you'll activate it in your job wrapper script since modules aren't available.

**Create wrapper script (`run_with_conda.sh`):**
```bash
#!/bin/bash
source ~/miniconda3/etc/profile.d/conda.sh
conda activate myenv
python my_analysis.py
```

**Submit file:**
```
executable = run_with_conda.sh
request_cpus = 1
request_memory = 4GB
output = job.$(cluster).$(process).out
error = job.$(cluster).$(process).err
log = job.$(cluster).log
queue 1
```

---

## Using UV (Modern Python Packaging)

UV is a fast Python package installer. See examples in the [OrangeGrid UV examples](https://github.com/SyracuseUniversity/OrangeGridExamples/tree/main/uv){:target="_blank"}.

---

## Using Singularity Containers

For complex software stacks or when you need specific system libraries.

### Convert Docker Image to Singularity

```bash
# Pull Docker image and convert
singularity pull docker://tensorflow/tensorflow:latest-gpu

# This creates: tensorflow_latest-gpu.sif
```

### Run Your Code in the Container

```bash
singularity exec tensorflow_latest-gpu.sif python my_script.py
```

### Using Containers in Job Scripts (Zest)

```bash
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --gres=gpu:1

singularity exec my_container.sif python my_ml_training.py
```

### Using Containers in Job Scripts (OrangeGrid)

```
executable = /usr/bin/singularity
arguments = exec my_container.sif python my_script.py
request_gpus = 1
output = job.$(cluster).$(process).out
error = job.$(cluster).$(process).err
log = job.$(cluster).log
queue 1
```

---

## Available Modules on Zest

```bash
# See all available software modules
module avail

# Search for specific module
module spider python

# Load a module
module load cuda/12.3
```

{: .note }
**Popular modules on Zest:**
- `anaconda3/2023.9` - Python environment
- `cuda/12.3` - NVIDIA CUDA libraries
- `openmpi4/4.1.6` - MPI implementation
- `gromacs/2023.2` - Molecular dynamics

For complete up-to-date list, run `module spider` on the cluster.
