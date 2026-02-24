---
layout: default
title: Your First Job
parent: Getting Started
nav_order: 7
---

# Your First Job

Step-by-step walkthrough for submitting your first job on either cluster.

{: .highlight }
**This is how you test your code on the cluster!** You don't run scripts directly on the login node - you submit them as jobs. Even small tests should be submitted to the scheduler. This teaches you the submission process you'll use for all your computational work.

---

## Choose Your Cluster

Select the guide for your assigned cluster:
- [Your First Job on OrangeGrid](#your-first-job-on-orangegrid)
- [Your First Job on Zest](#your-first-job-on-zest)

---

# Your First Job on OrangeGrid

## Step 1: Connect to OrangeGrid

```bash
ssh netid@its-og-login3.syr.edu
```
(Use your assigned login node from your welcome email)

## Step 2: Create Your Script

```bash
nano hello.sh
```

Add this content:

```bash
#!/bin/bash
set -e

echo "Hello from OrangeGrid!"
echo "Host name: $(hostname)"
echo "Date: $(date)"
echo "Kernel: $(uname -r)"

# Do some work
echo "Calculating..."
python3 -c "print('Sum:', sum(range(1000000)))"

echo "Job complete!"
exit 0
```

Make it executable:
```bash
chmod +x hello.sh
```

## Step 3: Create HTCondor Submit File

```bash
nano hello.sub
```

Add this content:

```
# Point to your executable script
executable = hello.sh

# Output files
output = hello.$(cluster).$(process).out
error = hello.$(cluster).$(process).err
log = hello.$(cluster).log

# Submit one job
queue 1
```

## Step 4: Submit the Job

```bash
condor_submit hello.sub
```

You'll see:
```
Submitting job(s).
1 job(s) submitted to cluster 54321.
```

## Step 5: Check Job Status

```bash
# Check your jobs
condor_q

# Check specific user
condor_q netid

# Watch continuously (update every 5 seconds)
watch -n 5 condor_q netid
```

**Understanding Job States:**
- **I** - Idle (waiting in queue)
- **R** - Running
- **H** - Held (problem requiring manual intervention)
- **C** - Completed

## Step 6: View Results

```bash
# View output
cat hello.54321.0.out

# Check for errors
cat hello.54321.0.err
```

{: .note }
**Common HTCondor Commands:**
- `condor_q` - View job queue
- `condor_rm 54321` - Remove job 54321
- `condor_status` - View available machines
- `condor_userprio` - See who's using the pool

---

# Your First Job on Zest

## Step 1: Connect to Zest

```bash
ssh netid@its-zest-login1.syr.edu
```
(Use your assigned login node from your welcome email)

## Step 2: Create Your Python Script

```bash
nano hello_cluster.py
```

Add this content:

```python
#!/usr/bin/env python3
import socket
import datetime

print("Hello from the cluster!")
print(f"Running on: {socket.gethostname()}")
print(f"Time: {datetime.datetime.now()}")

# Do some computation
result = sum(range(1000000))
print(f"Computation result: {result}")

# Save to file
with open('hello_output.txt', 'w') as f:
    f.write(f"Job ran on {socket.gethostname()}\n")
    f.write(f"Result: {result}\n")
```

Save with Ctrl+O, exit with Ctrl+X.

## Step 3: Create Job Submission Script

```bash
nano submit_hello.sh
```

Add this content (replace netid with your actual NetID):

```bash
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --time=00:05:00
#SBATCH --mail-type=ALL
#SBATCH --mail-user=netid@syr.edu

# Load Python environment
module load anaconda3

# Run the script
python hello_cluster.py
```

## Step 4: Submit the Job

```bash
sbatch submit_hello.sh
```

You'll see output like:
```
Submitted batch job 12345
```

## Step 5: Check Job Status

```bash
# Check your jobs
squeue -u netid

# See detailed info
scontrol show job 12345
```

## Step 6: View Results

Once the job completes, check your output:

```bash
# View the Slurm output file
cat slurm-12345.out

# View your custom output
cat hello_output.txt
```

{: .note }
**Common Slurm Commands:**
- `squeue` - View job queue
- `scancel 12345` - Cancel job 12345
- `sinfo` - View node information
- `sacct` - View job accounting info

---

## Next Steps

Now that you've submitted your first job, you can:

1. **Explore examples** - Check the [OrangeGrid](https://github.com/SyracuseUniversity/OrangeGridExamples){:target="_blank"} or [Zest](https://github.com/SyracuseUniversity/ZestExamples){:target="_blank"} repositories
2. **Set up your environment** - See the [Software & Environments]({% link getting-started/software.md %}) guide
3. **Adapt examples** - Modify example scripts for your research
4. **Optimize** - Learn from resource usage and adjust requests

**Need help?** Email [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)
