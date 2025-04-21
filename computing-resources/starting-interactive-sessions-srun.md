```markdown
---
title: "Starting Interactive Compute Sessions (srun)"
category: "computing-resources"
description: "Using the 'srun' command to allocate resources and start interactive command-line sessions on compute nodes."
---

# Starting Interactive Compute Sessions (srun)

This document describes how to use the `srun` command to request computational resources and start an interactive command-line session directly on a compute node within the SCRC Slurm cluster. Interactive sessions are useful for tasks like debugging code, running short tests, or using applications with graphical interfaces (via FastX).

Unlike batch jobs submitted with `sbatch`, an interactive session provides a real-time command prompt on the allocated compute node.

## Starting an Interactive Session

To start an interactive session, you first need to be logged into one of the SCRC login nodes (`rnd.scrc.nyu.edu` or `vleda.scrc.nyu.edu`) or a FastX node (`fx1`, `fx2`, `fx3`).

From the command line, use the `srun` command with the `--pty` option and specify the resources you need. The final argument is the command you want to run, typically `/bin/bash` to get a shell prompt.

**Basic Command Structure:**

```bash
srun [options] /bin/bash
```

**Common Example:**

This command requests 1 CPU core, 8GB of memory, and 1 node for a duration of 1 hour, then starts a Bash shell session on the allocated node.

```bash
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
```

Once the resources are allocated, your command prompt will change, indicating you are now on a compute node (e.g., `[user@compute-node-name ~]$`) rather than a login or FastX node.

## Common Parameters

Here are explanations for the frequently used parameters in the example above:

*   `srun`: The Slurm command to run a job interactively (or as part of a batch job).
*   `--pty`: Allocates a pseudo-terminal, making the session interactive. This is crucial for getting a command prompt.
*   `--mem=<size>`: Specifies the amount of memory required for the job. Use units like `mb` (megabytes) or `gb` (gigabytes). Example: `--mem=8gb`.
*   `--time=<hh:mm:ss>`: Sets the maximum wall-clock time limit for the job. Your session will be terminated after this time. Example: `--time=1:00:00` for 1 hour. Be mindful of partition limits.
*   `--cpus-per-task=<number>`: Requests a specific number of CPU cores for your task. Example: `--cpus-per-task=1`.
*   `--nodes=<number>`: Requests a specific number of compute nodes. For most interactive sessions, this will be `--nodes=1`.
*   `/bin/bash`: The command to execute once the resources are allocated. `/bin/bash` starts an interactive Bash shell.

## Requesting Specific Resources (Partitions)

You can request nodes with specific characteristics (like GPUs or large amounts of memory) by specifying a partition using the `--partition` option.

*   **Requesting a GPU Node:**

    ```bash
    srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 --partition=gpu /bin/bash
    ```

*   **Requesting a High-Memory Node:**

    ```bash
    srun --pty --mem=64gb --time=2:00:00 --cpus-per-task=4 --nodes=1 --partition=bigmem /bin/bash
    ```

You can view available nodes and partitions using the `sinfo` command.

## Example Workflow

A common workflow for using an interactive session involves:

1.  Logging into an SCRC login node or FastX node.
2.  Using `srun` to allocate resources and get a shell on a compute node.
3.  Loading necessary software modules using the `module` command.
4.  Running your application or commands.
5.  Exiting the shell (typing `exit` or `Ctrl+D`) when finished, which releases the allocated resources.

**Example:** Running RStudio interactively via FastX

```bash
# 1. Log in to a FastX node (e.g., fx1.scrc.nyu.edu) and open a GNOME Terminal

# 2. Request an interactive session on a compute node
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash

# ---> Wait for resource allocation. Prompt changes to compute node prompt. <---
# Example prompt: [yourNetID@compute-node-XX ~]$

# 3. Load the RStudio module
module load rstudio

# 4. Launch RStudio
rstudio

# ---> RStudio GUI opens <---

# 5. When finished with RStudio, close its window.
#    Then, exit the interactive shell on the compute node:
exit
# ---> Returns you to the FastX node prompt. <---
```

## Notes

*   **Do not run computationally intensive tasks directly on login nodes (`rnd`, `vleda`) or FastX nodes (`fx1`, `fx2`, `fx3`).** These nodes are shared resources for accessing the cluster, editing files, and submitting jobs. Use `srun` or `sbatch` to run computations on the compute nodes.
*   Be realistic with resource requests (`--time`, `--mem`, `--cpus-per-task`). Requesting excessive resources may increase your wait time in the queue.
*   Your interactive session will be terminated automatically when the requested `--time` limit is reached. Save your work frequently.
```