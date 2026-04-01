---
layout: default
title: Connecting
parent: Getting Started
nav_order: 1
---

# Connecting to the Cluster

How to connect to your assigned cluster and transfer files.

---

## SSH Connection

You'll connect using SSH (Secure Shell). Your welcome email contains your specific login node.

### From Windows (Command Prompt or PowerShell)
```bash
ssh netid@its-zest-login1.syr.edu
```

### From Mac/Linux (Terminal)
```bash
ssh netid@its-zest-login1.syr.edu
```

### Using PuTTY (Windows)
1. Download and install PuTTY
2. Enter hostname: `its-zest-login1.syr.edu` (or your assigned node)
3. Click "Open" and enter your credentials

---

## Off-Campus or Campus Wi-Fi?

{: .warning }
You cannot connect directly from off-campus or while on campus Wi-Fi. ITS recommends to connecting through [SU Remote Desktop (RDS)](https://answers.atlassian.syr.edu/wiki/x/noOICQ), which provides a Windows environment with SSH and SCP tools pre-installed (e.g., Putty/WinSCP). Once on RDS, you can connect as if you are on campus as detailed above.  

### Alternative Remote Access Options  
If RDS presents disruption to your workflow, please let us know and specify the operating system you are using (e.g. Windows 11, MacOS, Linux) as we have other off-campus connection options. Note that access is regulated and users do not have alternative access by default.    

**Alternative Access Instructions:**
For those who have or have been provided access. 
- [Azure VPN Instructions](https://answers.atlassian.syr.edu/wiki/x/cYGICQ) (Windows 11 and MacOS)
- Bastion Host Instructions (Linux)
**Need help with remote access?** Contact [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu) for additional connection options.

---

## Once Connected: What to Do

{: .note }
**Acceptable Activities on Login Nodes:**
- Edit scripts with nano or vim (keep it brief)
- Create conda environments: `conda create -n myenv python=3.11`
- Check singularity: `singularity exec container.sif echo "works"`
- Submit jobs: `sbatch script.sh` or `condor_submit job.sub`
- Check status: `squeue` or `condor_q`
- Quick file operations: `ls`, `cp`, `mv`

{: .warning }
**Do NOT Do These Things:**
- Run: `python my_analysis.py` (submit as a job instead!)
- Test code by running it directly
- Install software outside of conda/UV/singularity
- Start tmux and leave it running indefinitely
- Keep connections open in your IDE when not actively editing

**Remember:** The login node is a gateway, not your workspace. Your code runs on compute nodes after you submit it as a job.

{: .note }
**Connection Best Practices:**
- Close connections when done - Don't leave SSH sessions or IDE connections open unnecessarily
- Avoid stale tmux/screen sessions - Don't create persistent sessions and leave them running indefinitely
- Why this matters: Each open connection consumes resources on the shared login node
- Good practice: Connect → submit jobs/check status/light editing → disconnect

---

## Transferring Files

You have several options for moving files to/from the cluster.

### SCP (Command Line) - Quick Transfers

**Good for:** Small to medium files, one-time transfers

```bash
# Upload to cluster
scp myfile.py netid@its-zest-login1.syr.edu:~/my_project/

# Download from cluster
scp netid@its-zest-login1.syr.edu:~/results.txt ./
```

### WinSCP (Windows GUI) - User-Friendly

**Good for:** Windows users who prefer graphical interface, browsing files

1. Download and install WinSCP
2. Enter hostname and credentials
3. Drag and drop files between local and remote

**Ideal if you're developing primarily on Windows** and want an easy way to sync files.

### rsync - Large Data Transfers

**Good for:** Large datasets, resumable transfers, synchronizing directories

```bash
# Sync local directory to cluster
rsync -avz --progress /local/data/ netid@cluster:~/data/

# Download from cluster
rsync -avz --progress netid@cluster:~/results/ ./local_results/
```

**Why rsync for large data?**
- ✅ Can resume interrupted transfers (critical for multi-hour transfers)
- ✅ Only transfers changed files (efficient for updates)
- ✅ Shows progress and transfer speed
- ✅ Handles connection timeouts better than SCP

### Large Data Transfers (TBs)

{: .note }
**Planning to move terabytes of data?**  
Contact us first: [researchcomputing@syr.edu](mailto:researchcomputing@syr.edu)

**Why reach out?**
- Azure VPN connections may timeout during multi-day transfers
- We can explore alternative remote-connection options for more reliable transfers
- We can help optimize the transfer for your specific situation

**Tip for large rsync transfers:** Run rsync in `tmux` or `screen` so it continues if your SSH connection drops. You can then disconnect from the session while letting rsync keep running (this is an acceptable use of these tools).
