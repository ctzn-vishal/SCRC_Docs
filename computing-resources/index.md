```markdown
---
title: "Computing Resources"
category: "computing-resources"
description: "Documentation about Slurm, batch jobs, interactive sessions, resource management, and hardware specifications at SCRC."
---

# Computing Resources

Welcome to the Computing Resources documentation for the SCRC cluster. This section provides essential information on how to effectively utilize the computational power available to you. Understanding these concepts is key to running your analyses, simulations, and other computational tasks efficiently and respectfully of shared resources.

Here, you'll learn about **Slurm**, the workload manager that schedules and manages jobs on the cluster. We cover two primary ways of running jobs:

*   **Batch Jobs:** Ideal for non-interactive tasks that can run independently. You'll submit these using script files (`.sbatch`).
*   **Interactive Sessions:** Necessary when you need to interact directly with software or visualize results in real-time. This can be done via command-line (`srun`) or graphical interfaces (FastX).

Effectively managing resources means understanding how to request processors (CPUs), memory (RAM), time, and potentially specialized hardware like GPUs. This ensures your jobs run correctly and the cluster remains available for all users.

## Topics in this Category

Explore the following pages to learn more about specific aspects of using SCRC's computing resources:

*   **[Slurm Overview and Common Commands](slurm-overview-commands.md)**
    *   Introduction to the Slurm workload manager and descriptions of essential commands like `sbatch`, `squeue`, `sinfo`, `srun`, and `scancel`.
*   **[Submitting Batch Jobs](submitting-batch-jobs.md)**
    *   Detailed guide on creating Slurm batch scripts (`.sbatch` files) and submitting non-interactive jobs to the cluster. Includes examples for Python, SAS, and MATLAB.
*   **[Running Interactive Jobs with FastX](running-interactive-jobs-fastx.md)**
    *   How to use FastX to start interactive graphical sessions on the cluster, connect via browser or client, and launch applications.
*   **[Starting Interactive Compute Sessions (srun)](starting-interactive-sessions-srun.md)**
    *   Using the `srun` command to allocate resources and start interactive command-line sessions on compute nodes.
*   **[Slurm Array Jobs](slurm-array-jobs.md)**
    *   Explanation and examples of using Slurm array jobs to run multiple similar tasks efficiently. Includes Python and R examples.
*   **[Hardware Specifications](hardware-specifications.md)**
    *   Details about the computing hardware available at SCRC, including cloud server specifications and network infrastructure.
```