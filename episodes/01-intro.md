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

Session Breakdown & Content
Session 1: What is HPC & How Does It Work? (10 mins)
1.1 Desktop vs. Cluster Computing

    Local Machine: Single system where interactive GUI, CPU, memory, and storage share the same bus. Great for development, bad for scale.

    HPC Cluster: A collection of network-connected servers (nodes) operating as a unified system to handle heavy computational loads.

1.2 The Anatomy of a Cluster

    Login Head Nodes: The front door of the cluster. Used only for editing code, managing files, and submitting jobs. Never run computational tasks directly on login nodes.

    Compute Nodes: The worker units where actual execution happens in isolated job environments.

    Interconnect: High-speed networks connecting nodes to shared parallel storage.
    

Session 2: System Specs & Environment Setup (15 mins)

(Fill in the bracketed placeholders below with your cluster details.)
2.1 Hardware Specifications Overview

    Compute Architecture: [INSERT: e.g., x86_64 / Rocky Linux / Ubuntu]

    Total Compute Nodes: [INSERT: Total node count]

    CPU Resources: [INSERT: e.g., AMD EPYC / Intel Xeon cores per node]

    GPU Accelerator Resources: [INSERT: e.g., NVIDIA A100 / H100 / L40S specs]

    Interconnect: [INSERT: e.g., InfiniBand 100Gbps / Ethernet]
    
2.2 Storage Tiers & Quotas

2.3 Software & Environment Management

    Lmod / Environment Modules: Software on HPC systems is loaded dynamically to avoid library conflicts.

    Common Commands:

        module avail — List available software packages.

        module load [package_name] — Load a tool into your current session.

        module list — Display currently active modules.

Session 3: Usage Policy & System Etiquette (10 mins)
3.1 Acceptable Use Rules

    Login Node Etiquette: No high-CPU, high-RAM, or multi-threaded jobs on login nodes. Rogue processes will be terminated automatically.

    Resource Request Accuracy: Request only the CPUs, GPUs, memory, and walltime your job actually needs. Over-requesting leads to longer queue wait times and starves other users.

    Fair-Share Priority: Prioritization is calculated algorithmically based on recent resource consumption.

3.2 Specific Cluster Policy Limits

    GPU Allocation Cap: [INSERT: e.g., Maximum 8 GPUs per user across active jobs]

    Job Runtime Limits: [INSERT: e.g., Default queue max walltime 48 hours]

    Account Security & SSH: Shared accounts are strictly prohibited. Multi-factor authentication or SSH key access required.

    Data Cleanup Responsibilities: Users are required to purge /scratch space regularly.

Session 4: Submitting & Managing Jobs with Slurm (15 mins)
4.1 Anatomy of a Slurm Batch Script (submit.sh)
:::::::::::::::::::::::::::::::::::::::: bash
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
python3 my_script.py

::::::::::::::::::::::::::::::::::::::::::::::::::

4.2 Essential Slurm Commands

Session 5: Wrap-Up, Troubleshooting & Q&A (10 mins)
5.1 Common Troubleshooting Scenarios

    OUT_OF_MEMORY (OOM) Errors: Job exceeded requested RAM (--mem). Increase memory limit in #SBATCH header.

    TIMEOUT Errors: Job ran longer than requested --time. Increase requested walltime or implement checkpointing.

    Pending Job Reason ReqNodeNotAvailable / QOSResourceLimit: Job requests exceed max policy limits or hardware availability.

5.2 Support Channels & Resources

    Cluster Documentation: [INSERT: Link to wiki / docs]

    Helpdesk / Ticketing: [INSERT: Support email / ticket portal]

    System Status & Maintenance: [INSERT: Status page URL]

:::::::::::::::::::::::::::::::::::::::: keypoints

- Login nodes are for navigation and submission; compute nodes are for computation.
- Slurm schedules resources based on your requests—estimate memory and time accurately.
- Respect storage quotas and purge temporary scratch files regularly.
- Check job accounting (sacct) after execution to optimize future resource requests.
::::::::::::::::::::::::::::::::::::::::::::::::::


