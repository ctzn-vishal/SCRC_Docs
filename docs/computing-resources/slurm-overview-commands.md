# Slurm Overview and Common Commands

This document provides an overview of the Slurm Workload Manager used on the NYU Stern Center for Research Computing (SCRC) clusters and details the usage of common Slurm commands essential for managing jobs.

## Slurm Overview

The SCRC Slurm cluster is a collection of moderate-sized compute nodes designed to support a wide range of computational tasks, including data analysis, simulations, and modeling. Slurm (Simple Linux Utility for Resource Management) is the workload manager responsible for accepting, scheduling, and managing computational jobs submitted to the cluster.

Researchers can interact with the Slurm cluster in two primary ways:

1.  **Batch Jobs:** Users submit scripts (using `sbatch`) that define the resources needed and the commands to execute. Slurm runs these jobs non-interactively when the requested resources become available.
2.  **Interactive Jobs:** Users request resources (using `srun`) to get direct, real-time access to compute nodes for tasks like debugging, interactive data analysis, or running graphical applications.

## Common Slurm Commands

The following commands are fundamental for interacting with the Slurm scheduler:

| Command  | Usage                                     | Description                                       | Example                                                            |
| :------- | :---------------------------------------- | :------------------------------------------------ | :----------------------------------------------------------------- |
| `sbatch` | `sbatch [options] <script_file>`          | Submits a batch job script to the Slurm scheduler | `sbatch myScript.sbatch`                                           |
| `squeue` | `squeue [options]`                        | Displays the status of jobs in the queue          | `squeue -u $USER`                                                  |
| `sinfo`  | `sinfo [options]`                         | Provides information about Slurm nodes and queues | `sinfo`                                                            |
| `srun`   | `srun [options] <executable> [arguments]` | Runs a parallel job or starts an interactive session | `srun --pty --mem=8gb --time=1:00:00 /bin/bash`                    |
| `scancel`| `scancel [options] <job_id>`              | Cancels a pending or running job                  | `scancel 1203`                                                     |

### `sbatch`

The `sbatch` command submits a job script for later execution. The script typically contains Slurm directives (lines starting with `#SBATCH`) that specify job options, resource requirements, and the commands to be executed.

**Syntax:**

```bash
sbatch [options] <script_file>
```

**Common `#SBATCH` Directives (within the script file):**

*   `--job-name=<job_name>`: Specifies a name for the job.
*   `--output=<output_file>`: Specifies the file to redirect stdout. `%j` can be used for job ID, `%A` for job array master ID, `%a` for array task ID.
*   `--error=<error_file>`: Specifies the file to redirect stderr.
*   `--export=ALL`: Exports all environment variables from the submission environment to the job environment.
*   `--time=<time_limit>`: Sets the maximum wall-clock time limit (e.g., `01:30:00` for 1 hour 30 minutes, `2-00:00:00` for 2 days).
*   `--mem=<memory>`: Specifies the real memory required per node (e.g., `4G` for 4 Gigabytes, `512m` for 512 Megabytes).
*   `--nodes=<node_count>`: Requests a specific number of nodes.
*   `--cpus-per-task=<cpu_count>`: Requests a specific number of CPU cores per task.
*   `--partition=<partition_name>`: Specifies the partition (queue) to submit the job to (e.g., `test`, `gpu`, `bigmem`).
*   `--mail-type=<event_list>`: Sends email notifications for specified events (e.g., `BEGIN`, `END`, `FAIL`, `ALL`).
*   `--mail-user=<email_address>`: Specifies the email address for notifications.
*   `--array=<task_range>`: Submits a job array (e.g., `1-5`, `5-15:5`).

**Example Usage:**

```bash
sbatch my_analysis_script.sbatch
```

**Example Slurm Script (`hello-world.sbatch`):**

```bash
#!/bin/bash
#
# [hello-world.sbatch]
#
#SBATCH --job-name=hello            # Job name
#SBATCH --output=hello.%j.out       # Output file name (%j expands to jobID)
#SBATCH --export=ALL               # Export all environment variables
#SBATCH --time=00:01:00             # Set max runtime of job = 1 minute
#SBATCH --mem=4G                    # Request 4 gigabytes of memory
#SBATCH --mail-type=END,FAIL        # Send email notifications for job end or failure
#SBATCH --mail-user=your_netid@stern.nyu.edu # Email address for notifications
#SBATCH --partition=test            # Specify the partition to submit the job to

module purge                         # Start with a clean environment
module load python/3.9.7           # Load python module
python hello-world.py               # Run the python script
```

*(Note: `hello-world.py` should contain the Python code to be executed.)*

### `squeue`

The `squeue` command shows the state of jobs in the Slurm scheduling queue.

**Syntax:**

```bash
squeue [options]
```

**Common Options:**

*   `-u <username>`: Displays jobs for a specific user (e.g., `-u $USER` for your jobs).
*   `-p <partition_name>`: Displays jobs in a specific partition.
*   `-t <state>`: Displays jobs in a specific state (e.g., `PENDING`, `RUNNING`). Common states are `PD` (Pending), `R` (Running), `CG` (Completing).

**Example Usage:**

```bash
# Show all jobs in the queue
squeue

# Show only your jobs
squeue -u $USER

# Show jobs for user xy12
squeue -u xy12
```

### `sinfo`

The `sinfo` command reports the state of partitions and nodes managed by Slurm.

**Syntax:**

```bash
sinfo [options]
```

**Example Usage:**

```bash
# Show summary information about partitions and nodes
sinfo
```

This command helps you see available partitions (`gpu`, `bigmem`, `test`, etc.) and the status of nodes within them (idle, allocated, down).

### `srun`

The `srun` command is used to submit jobs for execution in real-time or to allocate resources for an interactive session.

**Syntax:**

```bash
srun [options] <executable> [arguments]
```

**Common Options for Interactive Sessions:**

*   `--pty`: Allocates a pseudo-terminal, necessary for interactive shell sessions.
*   `--mem=<memory>`: Requests a specific amount of memory (e.g., `8gb`, `16G`).
*   `--time=<time_limit>`: Sets a time limit for the interactive session (e.g., `1:00:00`).
*   `--cpus-per-task=<cpu_count>`: Requests a number of CPU cores (e.g., `1`, `4`).
*   `--nodes=<node_count>`: Requests a number of compute nodes (usually `1` for interactive sessions).
*   `--partition=<partition_name>`: Specifies the partition to run on (e.g., `gpu`, `bigmem`). If omitted, uses a default partition.
*   `<executable>`: The program to run, often `/bin/bash` to start an interactive shell.

**Example Usage (Starting an Interactive Shell):**

```bash
# Request an interactive session with 8GB RAM, 1 CPU, for 1 hour
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash

# Request an interactive session on a GPU node
srun --pty --mem=16gb --time=2:00:00 --cpus-per-task=2 --nodes=1 --partition=gpu /bin/bash
```

Once the resources are allocated, your command prompt will change, indicating you are now on a compute node instead of a login node. You can then load modules and run commands directly on the allocated node.

### `scancel`

The `scancel` command is used to cancel pending or running Slurm jobs.

**Syntax:**

```bash
scancel [options] <job_id>[_<task_id>]
```

**Common Options:**

*   `-u <username>`: Cancels jobs belonging to the specified user.
*   `-n <job_name>`: Cancels jobs with the specified name.
*   `-t <state>`: Cancels jobs in the specified state (e.g., `PENDING`).

**Example Usage:**

```bash
# Cancel job with ID 1203
scancel 1203

# Cancel task 5 of job array 1204
scancel 1204_5

# Cancel all pending jobs for the current user
scancel -t PENDING -u $USER

# Cancel all jobs for the current user
scancel -u $USER