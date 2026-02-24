---
layout: default
title: Interactive vs. Batch Computing
parent: Getting Started
nav_order: 1
---

# Interactive vs. Batch Computing

Understanding the fundamental difference between how you've worked before and how clusters work.

---

## What You're Used To: Interactive Computing

On your laptop or desktop:
- You click "Run" in your IDE (Jupyter, Spyder, RStudio, VSCode)
- Your code executes immediately
- You see results right away in the console or plots
- You can interact with your program while it runs

**Interactive Computing Flow:**
```
👨‍💻 Write Code → ▶️ Click Run → ⚡ Immediate Execution → 📊 See Results
```

---

## What's Different: Batch Computing

On a cluster:
- You write a script describing your job
- You submit the job to a queue
- The scheduler assigns resources when available
- Your job runs without interaction
- You retrieve results later from output files

**Batch Computing Flow:**
```
📝 Write Script → 📤 Submit to Queue → ⏳ Wait for Resources → 🖥️ Job Runs → 📁 Check Output Files
```

{: .warning }
**Important:** IDEs like Jupyter, Spyder, and VSCode are **prohibited** on the clusters. They interfere with other users and can impact the entire system. Use batch job submission instead.

{: .note }
**You're Sharing the Login Node**  
When you SSH in, you land on a **login node** - a shared server that all users use to submit jobs. It's like a lobby or reception desk, not your actual workspace. If it takes more than a few minutes or uses significant CPU/memory, it belongs in a job submission, not on the login node.

---

## Why Batch Computing?

- **Resource Sharing:** Hundreds of researchers share the same hardware
- **Fair Scheduling:** Everyone gets their turn based on priority
- **Efficiency:** Resources are allocated optimally
- **Scale:** Run jobs too large for any single desktop
