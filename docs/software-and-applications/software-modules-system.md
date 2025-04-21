```markdown
---
title: "Using the Software Modules System"
category: "software-and-applications"
description: "How to use the 'module' command to find, load, and unload available software packages on the SCRC clusters."
---

# Using the Software Modules System

## Introduction

The SCRC clusters provide access to a wide variety of software packages, libraries, and compilers. To manage different versions and prevent conflicts between software, the SCRC uses an environment modules system. The `module` command is the primary tool for interacting with this system.

This page covers how to use the `module` command to find, load, and manage software packages available on the SCRC clusters. Understanding the module system is essential for using pre-installed software in your research workflows, whether in interactive sessions or batch jobs.

As stated in the tutorials:
> The `module` command is used to manage environment modules, which allow users to easily load and unload software and environment settings on systems such as HPC clusters.

## Finding Available Software

Before loading software, you need to know what is available. You can list all the software packages available through the module system using the `module avail` command.

```bash
module avail
```

Alternatively, you can use the shorthand:

```bash
module av
```

This command will display a list of all installed modules. The list can be quite long and often includes multiple versions for a single software package (e.g., `python/3.9.7`, `python/3.10.4`).

**Note:** The list of available modules might differ between login nodes (like the FastX session nodes `fx1`, `fx2`, `fx3`) and the compute nodes accessed via Slurm (`srun` or `sbatch`). Compute nodes typically have a more extensive software collection available. Always check for modules *after* starting an interactive job or within your batch script.

```bash
# Example: Checking modules after starting an interactive job
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
[user@compute-node ~]$ module avail
```

## Loading Software Modules

To use a specific software package, you need to load its corresponding module. Loading a module modifies your environment variables (like `PATH` and `LD_LIBRARY_PATH`) so that the system can find and execute the software.

The command to load a module is `module load`.

**Syntax:**

```bash
module load <module_name>[/<version>]
```

*   `<module_name>`: The name of the software package (e.g., `python`, `R`, `matlab`).
*   `[/<version>]`: Optional, but **highly recommended**. Specifying the version ensures you are using the exact version you need for reproducibility. If you omit the version, a default version (usually the latest or recommended one) will be loaded.

**Examples:**

*   Load a specific version of Python:
    ```bash
    module load python/3.9.7
    ```
*   Load a specific version of R:
    ```bash
    module load R/4.0.2
    ```
    ```bash
    module load R/4.3.2
    ```
*   Load MATLAB:
    ```bash
    module load matlab/2019a
    ```
*   Load Anaconda:
    ```bash
    module load anaconda3/py3.9
    ```
*   Load RStudio (often used in interactive graphical sessions):
    ```bash
    module load rstudio
    ```
*   Load XStata (often used in interactive graphical sessions):
    ```bash
    module load xstata-se/17.0
    ```
*   Load SAS:
    ```bash
    module load sas/9.4
    ```

You can load multiple modules sequentially if your workflow requires several software packages.

## Unloading Software Modules (Purging)

It is often crucial, especially in batch scripts, to start with a clean environment to avoid conflicts from previously loaded modules. The `module purge` command unloads *all* currently loaded modules.

**Syntax:**

```bash
module purge
```

This command is frequently used as the first step in Slurm batch scripts to ensure a predictable environment before loading the specific modules required for the job.

> The `purge` subcommand clears all loaded modules, while the `load` subcommand loads a specific module.

## Using Modules in Slurm Jobs

When submitting jobs to the Slurm scheduler (either batch jobs with `sbatch` or interactive jobs with `srun`), the required software modules must be loaded *within* the job's environment. Modules loaded in your login shell are not automatically inherited by Slurm jobs.

### Batch Jobs (`sbatch`)

Include `module purge` and `module load` commands directly in your `sbatch` script before executing your program.

**Example Structure:**

```bash
#!/bin/bash
#
#SBATCH --job-name=my_job
#SBATCH --output=my_job.%j.out
#SBATCH --time=01:00:00
#SBATCH --mem=4G
#SBATCH --partition=test
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=your_email@stern.nyu.edu

# Start with a clean environment
module purge

# Load necessary software modules
module load python/3.9.7
# module load another_package/version

# Execute your program
echo "Running Python script..."
python my_script.py
echo "Job finished."
```

### Interactive Jobs (`srun`)

After starting an interactive session using `srun`, use the `module load` command directly in the interactive shell before running your software.

**Example Flow:**

1.  Start an interactive session:
    ```bash
    srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
    ```
2.  Once on the compute node, load the required module:
    ```bash
    [user@compute-node ~]$ module load R/4.3.2
    ```
3.  Run your application:
    ```bash
    [user@compute-node ~]$ R
    ```
    or for graphical applications started via FastX/X11 forwarding:
    ```bash
    [user@compute-node ~]$ module load rstudio
    [user@compute-node ~]$ rstudio &
    ```

By managing your software environment with the `module` command, you can ensure access to the correct tools and versions for your research on the SCRC clusters.
```