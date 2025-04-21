```markdown
---
title: "Home and Bigdata Directories"
category: "storage-solutions"
description: "Information about user home directories and the 'bigdata' storage space for large datasets, including how to request it."
---

# Home and Bigdata Directories

This document provides information about your standard home directory and the separate `bigdata` storage space available on the SCRC Linux systems. Understanding the purpose and usage of each is crucial for managing your files and data effectively.

## User Home Directory

### Overview

Upon your first login to the SCRC systems (`rnd.scrc.nyu.edu` or `vleda.scrc.nyu.edu`), your personal home directory is automatically created. This directory serves as your primary storage space for configuration files, scripts, source code, and smaller datasets.

When you log in using SSH or other methods, you are automatically placed in your home directory.

### Finding Your Home Directory Path

You can display the full path to your current directory (which is your home directory immediately after login) using the `pwd` (print working directory) command:

```bash
pwd
```

**Example Output:**

The output will show a path structure similar to this example for a user with NetID `ct27`:

```
/homedir/employees/c/ct27
```

*   `/homedir`: The base directory containing user home directories.
*   `/employees`: A subdirectory (this might vary based on user type, e.g., students).
*   `/c`: A subdirectory based on the first letter of the user's NetID.
*   `/ct27`: The user's specific home directory, named after their NetID.

### Managing Files in Your Home Directory

You can view and manage files and directories within your home directory using standard Linux commands:

*   **List contents:** Use `ls -l` to see files and directories in long format, showing permissions, owner, size, and modification date.

    ```bash
    ls -l
    ```

    **Example Output:**
    ```
    total 180
    drwxr-xr-x 3 ct27 nobody 4096 Apr  5 2023 mywork
    drwxr-xr-x 3 ct27 nobody 4096 Apr  3 2023 archived-work
    -rw-r--r-- 1 ct27 nobody    0 Mar 18 2023 prog.sas7bdat
    -rw-r--r-- 1 ct27 nobody 1421 Mar 18 2023 prog.sas7bdat.log
    ```

*   **Change directory:** Use `cd` to navigate into subdirectories (e.g., `cd mywork`) or `cd ..` to move up one level.
*   **Create directory:** Use `mkdir` to create new subdirectories (e.g., `mkdir project_data`).

For more details on basic Linux commands, refer to the [Linux Tutorial](#linux-tutorial).

## Bigdata Directory (`bighome`)

### Purpose and Need

While your home directory is suitable for general use, it may have storage quotas or performance characteristics not ideal for very large datasets or computationally intensive I/O operations. For storing and managing large datasets, SCRC provides a separate, designated space often referred to as `bigdata` or `bighome`.

This space is specifically designed for:

*   Storing large research datasets.
*   Housing data used in computationally intensive jobs.
*   Creating Python virtual environments or other software environments that might consume significant disk space.

### Requesting Access

The `bigdata` directory is **not created automatically**. You must request it if you need space for large datasets.

*   **How to Request:** Send an email to `scrc-list@stern.nyu.edu` to request a `bigdata` (or `bighome`) directory.
*   **Location:** Once created, it typically resides within your home directory structure, often accessible via a path like `~/bigdata`. You can confirm the exact path after it has been set up for you.

### Usage Recommendations

*   **Large Datasets:** Store all substantial files and datasets (e.g., multi-gigabyte files, extensive simulation outputs) in your `bigdata` directory.
*   **Python Virtual Environments:** It is **strongly recommended** to create your Python virtual environments within your `bigdata` directory. This prevents filling up your home directory quota and can leverage storage optimized for larger files.

    **Example (Creating a virtual environment in `bigdata`):**
    ```bash
    # First, ensure the target directory exists (adjust path as needed based on setup)
    # This example assumes your bigdata directory is ~/bigdata
    mkdir -p ~/bigdata/my_virtual_envs

    # Load a Python module (use 'module avail python' to see options)
    module load python/3.9.7

    # Create the virtual environment inside the bigdata directory
    virtualenv ~/bigdata/my_virtual_envs/my_project_env

    # Activate the environment
    source ~/bigdata/my_virtual_envs/my_project_env/bin/activate

    # Your prompt should now indicate the active environment
    # (my_project_env) [ct27@rnd ~]$

    # Install packages as needed
    pip install pandas numpy

    # Deactivate when finished
    deactivate
    ```

### Storage and Backups

*   **Quota:** There is generally no predefined quota limit for `bigdata`/`bighome`, but please inform SCRC via email (`scrc-list@stern.nyu.edu`) if you anticipate needing more than 1TB of storage so they can plan accordingly.
*   **Backups:** The `bigdata`/`bighome` space is backed up (typically weekly) for data protection and disaster recovery purposes.

**Note:** The terms `bigdata` and `bighome` may be used interchangeably in different SCRC communications or by different staff members. They both refer to the same dedicated large-scale storage space available to users upon request. If unsure about the specific path or name for your account, please contact SCRC support.
```