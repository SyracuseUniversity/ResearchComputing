# OrangeGrid Cluster Specifications

Technical specifications for the OrangeGrid High-Throughput Computing (HTC) cluster.

---

## Overview

**Scheduler:** HTCondor  
**Type:** High-Throughput Computing (HTC)  
**Best For:** Many independent jobs, parameter sweeps, batch processing, embarrassingly parallel workloads  
**Access:** SSH via `its-og-loginX.syr.edu` (X = your assigned login node number, specified in your welcome email)

---

## Cluster Architecture

OrangeGrid is a heterogeneous pool of compute resources designed for high-throughput workloads. Unlike traditional HPC clusters with uniform nodes, OrangeGrid consists of many different types of machines, allowing the scheduler to match jobs to available resources dynamically.

### Key Characteristics

- **Opportunistic scheduling** - Jobs run when resources become available
- **Fair-share allocation** - Resources distributed equitably among all users
- **Heterogeneous pool** - Variety of CPU and GPU configurations
- **Best for independent jobs** - Each job runs separately without inter-job communication

---

## Requesting Resources

### Basic Job Submission

HTCondor uses submit files to define your job:

```htcondor
executable = my_script.sh

# Request resources
request_cpus = 1
request_memory = 4GB
request_disk = 10GB

# Optional: Request GPU
+request_gpus = 1

# Output files
output = job.$(cluster).$(process).out
error = job.$(cluster).$(process).err
log = job.$(cluster).log

queue 1
```

**Note:** Your home directory (`/home/netid/`) is automatically mounted on compute nodes, so your scripts and data are already accessible - no file transfer needed!

### CPU Requests

```htcondor
# Single CPU (default)
request_cpus = 1

# Multiple CPUs for multi-threaded applications
request_cpus = 4

# Note: Each job runs on a single node
# For truly parallel work across nodes, use Zest with MPI
```

### Memory Requests

```htcondor
# Specify in MB or GB
request_memory = 2GB
request_memory = 2048MB  # Same as 2GB

# Be accurate - jobs killed if they exceed requested memory
# Under-requesting causes job failure
# Over-requesting means longer wait times
```

### Disk Space

```htcondor
# Local disk space needed during job execution
request_disk = 5GB

# This is temporary space on the execution node
# Files transferred back based on transfer settings
```

---

## GPU Resources

### Available GPUs

OrangeGrid has GPU nodes with various models. The scheduler will match your job to an available GPU.

**GPU models in the pool:**
- NVIDIA A100
- NVIDIA L40S
- NVIDIA A6000
- Other models available

### Requesting GPUs

```htcondor
# Request any available GPU
+request_gpus = 1

# Multiple GPUs (if your code supports it)
+request_gpus = 2
```

**Best Practice:** Let HTCondor assign any available GPU unless your code specifically requires a certain model.

---

## Storage

### Home Directory
- **Path:** `/home/netid/`
- **Type:** NetApp storage
- **Accessibility:** Available on submit/login nodes and automatically mounted on compute nodes when your job runs
- **Use for:** Scripts, code, data, conda environments, results

### How Storage Works

Unlike some clusters, OrangeGrid mounts your home directory on compute nodes automatically. This means:
- ✅ Your scripts are already accessible when jobs run
- ✅ Your data files are available without transfer
- ✅ Results are saved directly to your home directory
- ✅ No need to specify file transfer in submit files

**Best Practices:**
- Organize with subdirectories: `~/data/`, `~/scripts/`, `~/results/`
- Output files are automatically saved to the directory where you submit from (or specify paths)
- For very large datasets (multi-TB), contact [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) to discuss optimal storage strategies

## Submitting Multiple Jobs

### Job Arrays

Submit many similar jobs with one command:

```htcondor
executable = process.py
arguments = input_$(Process).dat

request_cpus = 1
request_memory = 2GB

output = job_$(Process).out
error = job_$(Process).err
log = jobs.log

# Submit 100 jobs, numbered 0-99
queue 100
```

### Queue with Variables

Process multiple items:

```htcondor
executable = analyze.py
arguments = $(item)

# Queue one job for each item
queue item from (
  dataset1.csv
  dataset2.csv
  dataset3.csv
)
```

See [Multiple Jobs & Arrays Guide](../clusters/orangegrid/multiple-jobs.md) for more examples.

---

## Checking Cluster Status

```bash
# View your jobs
condor_q netid

# View all jobs in the pool
condor_q

# Detailed job information
condor_q -long <jobid>

# View available machines
condor_status

# View your priority and usage
condor_userprio

# Job history
condor_history netid

# Watch job status (updates every 5 seconds)
watch -n 5 condor_q netid
```

---

## Job States

When you run `condor_q`, you'll see jobs in different states:

| State | Meaning | Description |
|-------|---------|-------------|
| **I** | Idle | Job is waiting in queue for resources |
| **R** | Running | Job is currently executing |
| **H** | Held | Job has a problem requiring manual intervention |
| **C** | Completed | Job finished and ready to be removed from queue |
| **X** | Exiting | Job is cleaning up |

### Dealing with Held Jobs

If a job enters "H" (held) state:

```bash
# Check why job is held
condor_q -hold <jobid>

# Common reasons:
# - Requested more memory than available
# - Executable not found
# - File transfer failed

# Release held job after fixing issue
condor_release <jobid>

# Or remove and resubmit
condor_rm <jobid>
```

---

## Common Job Patterns

### Basic Python Job

```htcondor
executable = /usr/bin/python3
arguments = my_script.py

request_cpus = 1
request_memory = 4GB

output = job.$(cluster).$(process).out
error = job.$(cluster).$(process).err
log = job.$(cluster).log

queue 1
```

### GPU Job

```htcondor
executable = /usr/bin/python3
arguments = train_model.py

request_cpus = 4
request_memory = 16GB
+request_gpus = 1

output = gpu_job.$(cluster).$(process).out
error = gpu_job.$(cluster).$(process).err
log = gpu_job.$(cluster).log

queue 1
```

### Job with Conda Environment

**Create wrapper script (`run_with_conda.sh`):**
```bash
#!/bin/bash
source ~/miniconda3/etc/profile.d/conda.sh
conda activate myenv
python my_analysis.py
```

**Submit file:**
```htcondor
executable = run_with_conda.sh

request_cpus = 1
request_memory = 4GB

output = conda_job.$(cluster).$(process).out
error = conda_job.$(cluster).$(process).err
log = conda_job.$(cluster).log

queue 1
```

### Parameter Sweep

```htcondor
executable = simulation.py
arguments = --param $(Process)

request_cpus = 1
request_memory = 2GB

output = sim_$(Process).out
error = sim_$(Process).err
log = simulations.log

# Run 1000 simulations with different parameters
queue 1000
```

---

## Important Notes

### Interactive Development Prohibited

OrangeGrid is for batch job submission only. Do not run:
- Jupyter notebooks
- IDEs (Spyder, VSCode, etc.)
- Interactive development tools
- Long-running tests on login nodes

For development, use [Google Colab](../resources/google-colab.md) or your local machine.

### Job Duration

- Most jobs complete within hours to days
- No hard runtime limits, but fair-share scheduling applies
- Very long jobs may be preempted during high-demand periods
- For guaranteed long runtimes (weeks), consider Zest's longjobs partition

---

## Monitoring Resource Usage

After jobs complete, check resource usage to optimize future requests:

```bash
# View job statistics
condor_history <jobid> -limit 1 -long | grep -E 'Memory|Disk|Cpu'

# Useful for tuning requests:
# - MemoryUsage: Actual memory used
# - DiskUsage: Actual disk used  
# - RemoteUserCpu: CPU time used
```

Adjust your `request_memory` and `request_cpus` based on actual usage to get jobs scheduled faster.

---

## External Resources

- [HTCondor Quick Start Guide](https://htcondor.readthedocs.io/en/latest/users-manual/quick-start-guide.html)
- [HTCondor User Manual](https://htcondor.readthedocs.io/en/latest/users-manual/)
- [HTCondor Submit File Reference](https://htcondor.readthedocs.io/en/latest/man-pages/condor_submit.html)
- [OrangeGridExamples Repository](https://github.com/SyracuseUniversity/OrangeGridExamples)

---

## Getting Help

Questions about OrangeGrid specifications or optimal job configuration?

📧 Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
