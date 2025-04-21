```markdown
---
title: "Python Virtual Environments"
category: "software-and-applications"
description: "Creating, activating, and managing isolated Python environments to install and use specific package versions."
---

# Python Virtual Environments

This document describes how to create, activate, and manage Python virtual environments on the SCRC (Stern Center for Research Computing) systems. Using virtual environments allows you to create isolated Python setups for your projects, ensuring that package dependencies and versions do not conflict between different projects.

## What is a Python Virtual Environment?

A Python virtual environment is a personal, isolated Python installation located within a specific directory. It contains all the necessary executables and libraries for a Python project, independent of the system-wide Python installation or other virtual environments. This isolation allows you to customize the environment by installing specific versions of Python packages required for your project without affecting others.

## Why Use Virtual Environments?

*   **Dependency Management:** Different projects might require different versions of the same library. Virtual environments prevent version conflicts.
*   **Reproducibility:** Ensures that your project uses the exact package versions it was developed with, making it easier to share and reproduce your work.
*   **Cleanliness:** Keeps your global site-packages directory clean and manageable.

## General Steps

1.  **Create:** Set up the virtual environment directory (typically done once per project/environment).
2.  **Activate:** Activate the environment before working on your project or installing packages.
3.  **Install:** Use `pip` to install necessary packages within the activated environment.
4.  **Work:** Run your Python scripts or applications.
5.  **Deactivate:** Deactivate the environment when you are finished.

## Creating a Python Virtual Environment

Follow these steps to create a new virtual environment:

**Note:** Always create virtual environments within your `bigdata` directory. If you do not have a `bigdata` directory, please email `scrc-list@stern.nyu.edu` to request one. Storing environments elsewhere may lead to quota issues.

1.  **Load the Python Module:** Load the specific version of Python you want to use for your environment. Available Python versions can be listed using `module avail python`.

    ```bash
    module load python/3.9.7
    ```

2.  **Create the Environment:** Use the `virtualenv` command followed by the desired path for your environment directory. It's good practice to include the Python version in the directory name for clarity.

    ```bash
    # Example: Create an environment named 'py3.9' inside a '05-virtenvs' directory in your bigdata space
    virtualenv ~/bigdata/05-virtenvs/py3.9
    ```

    *   You only need to create a specific virtual environment once.
    *   You can create multiple virtual environments, potentially using different Python versions by loading different modules before running `virtualenv`.

## Activating and Deactivating an Environment

Before installing packages or running Python code within the environment, you must activate it.

1.  **Activate the Environment:** Use the `source` command to run the activation script located within the environment's `bin` directory.

    ```bash
    source ~/bigdata/05-virtenvs/py3.9/bin/activate
    ```

    *   **Indicator:** Once activated, the name of the virtual environment (e.g., `(py3.9)`) will be prepended to your shell prompt, indicating that the environment is active.
    *   Example prompt after activation: `(py3.9) [username@rnd ~]$`

2.  **Deactivate the Environment:** When you are finished working within the virtual environment, simply run the `deactivate` command.

    ```bash
    deactivate
    ```

    *   Your shell prompt will return to its normal state.

## Managing Packages with pip

Once an environment is activated, you can manage Python packages using `pip`. Packages installed in an active virtual environment are isolated to that environment.

*   **List Installed Packages:** See the packages currently installed in the active environment.

    ```bash
    pip list
    ```

*   **Install a New Package:** Install packages from the Python Package Index (PyPI).

    ```bash
    # Example: Install the 'requests' library
    pip install requests

    # Example: Install a specific version
    pip install requests==2.25.1

    # Example: Install from a requirements file
    pip install -r requirements.txt
    ```

*   **Uninstall a Package:** Remove a package from the environment.

    ```bash
    pip uninstall requests
    ```

*   **Freeze Requirements:** Generate a list of installed packages and their versions, typically saved to a `requirements.txt` file. This is useful for replicating the environment elsewhere.

    ```bash
    pip freeze > requirements.txt
    ```

## Using Virtual Environments in Slurm Batch Jobs

To use a specific Python virtual environment within a Slurm batch job, you need to include the `module load` command for the correct Python version and the `source ... activate` command for your environment within your `sbatch` script *before* executing your Python code.

**Example `sbatch` Script:**

```bash
#!/bin/bash
#
# [my-python-job.sbatch]
#
#SBATCH --job-name=py-job          # Job name
#SBATCH --output=py-job.%j.out     # Standard output file (%j expands to jobID)
#SBATCH --error=py-job.%j.err      # Standard error file (%j expands to jobID)
#SBATCH --export=ALL              # Export all environment variables
#SBATCH --time=00:10:00           # Max runtime D-HH:MM:SS
#SBATCH --mem=4G                  # Memory requested
#SBATCH --partition=test          # Partition to run in (e.g., test, cpu)
#SBATCH --mail-type=END,FAIL      # Send email on job END or FAIL
#SBATCH --mail-user=your_netid@stern.nyu.edu # Email address for notifications

# --- Job Steps ---
echo "Starting job on node: $(hostname)"
echo "Job started at: $(date)"

# 1. Purge existing modules to start fresh
module purge

# 2. Load the same Python module used to create the virtual environment
module load python/3.9.7

# 3. Activate the virtual environment
source ~/bigdata/05-virtenvs/py3.9/bin/activate

# 4. Run your Python script
echo "Running Python script..."
python my_script.py

# Environment will be deactivated automatically when the script finishes
echo "Job finished at: $(date)"

```

**Submit the Job:**

```bash
sbatch my-python-job.sbatch
```

Remember to replace `python/3.9.7`, `~/bigdata/05-virtenvs/py3.9`, `my_script.py`, and `your_netid@stern.nyu.edu` with your specific details.
```