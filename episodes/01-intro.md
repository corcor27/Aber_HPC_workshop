---
title: Introduction to High-Performance Computing (HPC)
teaching: 30
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand HPC Architecture: Differentiate between login nodes, compute nodes, and specialized accelerator hardware (GPUs).
- Navigate System Hardware & Specs: Identify cluster resources, storage tiers, and system capabilities.
- Comply with Usage Policies: Adhere to fair-share queue rules, storage quotas, and security guidelines.
- Submit & Monitor Jobs: Draft and run job scripts using the Slurm workload manager.

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::: questions

- "Why should you never run heavy Python data analysis or deep learning scripts directly on the login node?"
- "If your job requires 120 GB of memory and 2 GPUs, what happens if you forget to specify --mem in your Slurm script?"
- "What is the difference between /home and /scratch in terms of performance and data security?"


::::::::::::::::::::::::::::::::::::::::::::::::::


## Section 1: What is HPC & How Does It Work?

### 1.1 Desktop vs. Cluster Computing
- Local Machine: Single system where interactive GUI, CPU, memory, and storage share the same bus. Great for development, bad for scale.
- HPC Cluster: A collection of network-connected servers (nodes) operating as a unified system to handle heavy computational loads.

### 1.2 The Anatomy of a Cluster

- Login Head Nodes: The front door of the cluster. Used only for editing code, managing files, and submitting jobs. Never run computational tasks directly on login nodes.
- Compute Nodes: The worker units where actual execution happens in isolated job environments.
- Interconnect: High-speed networks connecting nodes to shared parallel storage.
    
## Section 2: System Specs & Environment Setup 

### HPC Hardware Overview

### Bert (Log-in Node) — TDP 120W
- **CPU:** AMD EPYC 7252 (8-Core, 120W)  
- **Memory:** 48GB  

---

### Ernie (x3) — TDP 200W each | Total 600W
- **CPU:** AMD EPYC 7552 (48-Core, 2.2GHz, 200W)  
- **Memory:** 384GB  

---

### hpc-gn-ampere-01 (AM-01) — TDP 2880W
- **GPU:** 8 × NVIDIA A100 (80GB VRAM each, 300W | 2400W total)  
- **CPU:** 2 × AMD EPYC 7F72 (24-Core, 240W | 480W total)  
- **Memory:** 2TB  

---

### hpc-ci-cascade-lake-01 (CL-01) — TDP 410W
- **CPU:** 2 × Intel Xeon Gold 6248R (3.0GHz, 205W | 410W total)  
- **Memory:** 1.5TB  

---

### hpc-gn-ampere-03 (AM-03) — TDP 2800W
- **GPU:** 8 × NVIDIA A100 (80GB VRAM each, 300W | 2400W total)  
- **CPU:** 2 × AMD EPYC 7702 (64-Core, 200W | 400W total)  
- **Memory:** 2TB  

---

### hpc-gn-ampere-04 (AM-04) — TDP 2800W
- **GPU:** 8 × NVIDIA A100 (80GB VRAM each, 300W | 2400W total)  
- **CPU:** 2 × AMD EPYC 7702 (64-Core, 200W | 400W total)  
- **Memory:** 2TB  

---

### hpc-gn-pascal-01 (PA-01) — TDP 625W
- **GPU:** 2 × NVIDIA Tesla P100 (16GB VRAM each, 250W | 500W total)  
- **CPU:** Intel Xeon Gold 6130 (2.1GHz, 125W)  
- **Memory:** 48GB  
- **Note:** Legacy GPU server  

---

### hpc-gn-hopper-01 (HO-01) — TDP 3520W
- **GPU:** 4 × NVIDIA H100 (94GB VRAM each, 700W | 2800W total, configurable to 400W each)  
- **CPU:** 2 × AMD EPYC Genoa 9654 (96-Core, 2.4GHz, 360W | 720W total)  
- **Memory:** 2TB  

---

### Cascade Lake Cluster (CL-02 to CL-06) — TDP 250W (standard) | 750W (optional)
- **Nodes:** CL-02, CL-03, CL-04, CL-05, CL-06  
- **CPU (each):** 2 × Intel Xeon Gold 6254 (3.1GHz, 125W | 250W total)  
- **Memory (each):** 768GB  

---

### hpc-ca-genoa-01 (GE-01) — TDP 115W
- **CPU:** Intel Xeon E5-2620 v4 (2.1GHz, 115W)  
- **Memory:** 1TB  

---

### hpc-gn-ampere-05 (AM-05) — TDP 455W
- **GPU:** 1 × NVIDIA A100 (40GB VRAM, 300W)  
- **CPU:** AMD EPYC 7452 (155W)  
- **Memory:** 768GB  

!["Are we dealing with supervised or unsupervised
learning?"](fig/hpc_upgrade.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

### 2.1 Hardware Specifications Overview

- Compute Architecture: [Rocky Linux]
- Total Compute Nodes: [INSERT: Total node count]
- CPU Resources: [INSERT: e.g., AMD EPYC / Intel Xeon cores per node]
- GPU Accelerator Resources: [NVIDIA A100 / H100]
- Interconnect: [Ethernet]

### 2.2 Storage Tiers & Quotas

Here's a synopsis of filesystems on the cluster at Aberystwyth:

|Name|Path|Default Quota|Disk Size|Backed Up|Filesystem
|-----------------|---|----|-----|---|-----|------|
|Home|/hpc/user.name|100GB|40TB |Yes|NFS|
|Scratch|/scratch/user.name|N/A|100TB|No|NFS|

**Important!! Ensure that you don't store anything longer than necessary on scratch, this can negatively affect other people’s jobs on the system.**

### 2.3 Software & Environment Management

- Lmod / Environment Modules: Software on HPC systems is loaded dynamically to avoid library conflicts.
- Common Commands:
  - module avail — List available software packages.
  - module load [package_name] — Load a tool into your current session.
  - module list — Display currently active modules.

## Section 3: Usage Policy & System Etiquette (10 mins)
### 3.1 Acceptable Use Rules

- Login Node Etiquette: No high-CPU, high-RAM, or multi-threaded jobs on login nodes. Rogue processes will be terminated automatically.
- Resource Request Accuracy: Request only the CPUs, GPUs, memory, and walltime your job actually needs. Over-requesting leads to longer queue wait times and starves other users.
- Fair-Share Priority: Prioritization is calculated algorithmically based on recent resource consumption.

### 3.2 Specific Cluster Policy Limits

- GPU Allocation Cap: [INSERT: e.g., Maximum 8 GPUs per user across active jobs]
- Job Runtime Limits: [INSERT: e.g., Default queue max walltime 48 hours]
- Account Security & SSH: Shared accounts are strictly prohibited. Multi-factor authentication or SSH key access required.
- Data Cleanup Responsibilities: Users are required to purge /scratch space regularly.

## Section 4: Submitting & Managing Jobs with Slurm (15 mins)

### 4.1 Anatomy of a Slurm Batch Script (submit.sh)

```bash
#!/bin/bash
#SBATCH --job-name=hpc_demo
#SBATCH --output=logs/job_%j.out
#SBATCH --error=logs/job_%j.err
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem=16G
#SBATCH --time=01:00:00
#SBATCH --partition=[INSERT_PARTITION_NAME]
#SBATCH --account=[INSERT_ACCOUNT_NAME]

# 1. Load required environment modules
module load python/3.11

# 2. Print execution metadata
echo "Job started on node: $(hostname) at $(date)"

# 3. Execute computational workload
python my_script.py
```


### 4.2 Essential Slurm Commands

## Section 5: Wrap-Up, Troubleshooting & Q&A (10 mins)

### 5.1 Common Troubleshooting Scenarios

- OUT_OF_MEMORY (OOM) Errors: Job exceeded requested RAM (--mem). Increase memory limit in #SBATCH header.
- TIMEOUT Errors: Job ran longer than requested --time. Increase requested walltime or implement checkpointing.
- Pending Job Reason ReqNodeNotAvailable / QOSResourceLimit: Job requests exceed max policy limits or hardware availability.

### 5.2 Support Channels & Resources

- Cluster Documentation: [INSERT: Link to wiki / docs]
- Helpdesk / Ticketing: [INSERT: Support email / ticket portal]
- System Status & Maintenance: [INSERT: Status page URL]

:::::::::::::::::::::::::::::::::::::::: keypoints

- Login nodes are for navigation and submission; compute nodes are for computation.
- Slurm schedules resources based on your requests—estimate memory and time accurately.
- Respect storage quotas and purge temporary scratch files regularly.
- Check job accounting (sacct) after execution to optimize future resource requests.
::::::::::::::::::::::::::::::::::::::::::::::::::


