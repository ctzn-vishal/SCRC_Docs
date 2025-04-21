# Computing Resources

Welcome to the Computing Resources documentation for the SCRC cluster. This section provides essential information about Slurm, batch jobs, interactive sessions, resource management, and hardware specifications.

Here, you'll learn about **Slurm**, the workload manager that schedules and manages jobs on the cluster. We cover:

* **Batch Jobs:** Ideal for non-interactive tasks that can run independently. You'll submit these using scripts.
* **Interactive Sessions:** Necessary when you need to interact directly with software or visualize results in real time.

Effectively managing resources means understanding how to request processors (CPUs), memory (RAM), time, and potential access to GPUs.

## Topics in this Category

Explore the following pages to learn more about specific aspects of using SCRC's computing resources:

* **[Slurm Overview and Common Commands](slurm-overview-commands.md)**
    * Introduction to the Slurm workload manager and descriptions of essential commands like `sbatch`, `squeue`, and `scancel`.
* **[Submitting Batch Jobs](submitting-batch-jobs.md)**
    * Detailed guide on creating Slurm batch scripts (`.sbatch` files) and submitting non-interactive jobs to the cluster.
* **[Running Interactive Jobs with FastX](running-interactive-jobs-fastx.md)**
    * How to use FastX to start interactive graphical sessions on the cluster, connect via browser or client, and manage resources.
* **[Starting Interactive Sessions (srun)](starting-interactive-sessions-srun.md)**
    * Using `srun` for interactive command-line sessions on compute nodes.
* **[Slurm Array Jobs](slurm-array-jobs.md)**
    * Submitting and managing job arrays for high-throughput computing.
* **[Hardware Specifications](hardware-specifications.md)**
    * Overview of available hardware, including CPUs, memory, GPUs, and networking.