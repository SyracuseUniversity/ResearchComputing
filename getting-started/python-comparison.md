---
layout: default
title: Python - Local vs. Cluster
parent: Getting Started
nav_order: 2
---

# Python: Local vs. Cluster

Understanding how Python workflows change when moving from your laptop to a cluster.

---

## Running Python Locally (Interactive)

On your laptop, you might work like this in Jupyter or VSCode:
```python
# You run this cell and see output immediately
import numpy as np
data = np.random.rand(1000, 1000)
result = np.mean(data)
print(f"Mean: {result}")
# Output appears right away: Mean: 0.4998234...
```

---

## Running Python on the Cluster (Batch)

Instead, you create files and submit them as a job.

{: .warning }
**CRITICAL: Login Nodes vs. Compute Nodes**  
The login node is NOT where your work runs. When you SSH in, you're on a shared login node used by all researchers to submit jobs. Login nodes are ONLY for: light text editing, creating conda/UV environments, testing singularity containers load, submitting jobs, and checking job status. Do NOT run computational code, install software outside conda/UV/singularity, use IDEs, leave tmux sessions running, or keep unused SSH connections open. Your work runs on dedicated compute nodes after you submit it as a job. Need a development environment? Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

### Step 1: Create your Python script

**File:** `my_analysis.py`
```python
#!/usr/bin/env python3
import numpy as np

# Your computation here
data = np.random.rand(1000, 1000)
result = np.mean(data)

# Save results to file instead of printing to screen
with open('results.txt', 'w') as f:
    f.write(f"Mean: {result}\n")

print("Analysis complete!")
```

### Step 2: Create a job submission script

**For Zest (Slurm):**

File: `submit_job.sh`
```bash
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --time=00:10:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=netid@syr.edu

# Load Python environment
module load anaconda3

# Run your script
python my_analysis.py
```

**For OrangeGrid (HTCondor):**

File: `job.sub`
```
executable = /usr/bin/python3
arguments = my_analysis.py
output = job.$(cluster).$(process).out
error = job.$(cluster).$(process).err
log = job.$(cluster).log
queue 1
```

{: .note }
**OrangeGrid Note:** Your home directory is mounted on compute nodes, so no file transfer is needed!

### Step 3: Submit the job

**On Zest:**
```bash
sbatch submit_job.sh
```

**On OrangeGrid:**
```bash
condor_submit job.sub
```

### Step 4: Check status and retrieve results

**On Zest:**
```bash
squeue                 # Check job status
cat results.txt        # View your results
```

**On OrangeGrid:**
```bash
condor_q               # Check job status
cat results.txt        # View your results
```

{: .highlight }
**Key Difference:** Instead of seeing output immediately in a notebook, you submit the job, it runs when resources are available, and you retrieve results from output files later.
