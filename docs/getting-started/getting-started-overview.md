# Getting Started Overview

This guide outlines the essential first steps for new users after obtaining an SCRC account and logging into the SCRC environment for the first time via SSH. It covers the initial environment setup and basic commands to verify your access.

## Your First Login

Once your Stern account is activated and you have successfully logged into one of the SCRC login nodes (`rnd.scrc.nyu.edu` or `vleda.scrc.nyu.edu`) using your Stern NetID and password via SSH:

1.  **Automatic Home Directory Creation:** Upon your first login, your personal home directory will be automatically created on the SCRC file system. This directory serves as your primary storage space for files and projects.

2.  **The Command Prompt:** After logging in, you will be presented with a command prompt in the Linux BASH shell. This is the interface where you will enter commands. The prompt typically looks similar to this (where `xy12` is the NetID and `rnd` is the login node):

    ```text
    [xy12@rnd ~ ]$
    ```

## Initial Steps and Verification

After logging in for the first time, you can perform these basic steps to familiarize yourself with the environment:

1.  **Verify Your Location (Present Working Directory):**
    To confirm you are in your home directory, use the `pwd` (print working directory) command:

    ```bash
    pwd
    ```

    The output will show the full path to your home directory, for example:

    ```text
    /homedir/employees/x/xy12
    ```
    *(Note: The exact path structure might vary)*

2.  **List Directory Contents:**
    Your newly created home directory will initially be empty or contain only default configuration files. You can view its contents using the `ls -l` command (list directory contents in long format):

    ```bash
    ls -l
    ```

    If the directory is empty, the command will return immediately without listing any files. If there are hidden configuration files, it might look something like this:

    ```text
    total 0
    # Or potentially some hidden files starting with '.'
    ```

## Environment Notes

*   **Operating System:** The SCRC systems run Linux.
*   **Shell:** The default command-line interface (shell) is BASH (Bourne-Again SHell).
*   **Linux Familiarity:** Basic familiarity with Linux/Unix commands is expected for using SCRC resources effectively.

## Next Steps

Now that you have successfully logged in and verified your home directory, you can proceed to:

*   Learn more essential commands in the [Linux Tutorial](./linux-tutorial.md).
*   Understand how to [Transfer Files](./transferring-files.md) between your local machine and SCRC.
*   Learn about submitting jobs using the [Slurm Workload Manager](./slurm-overview.md).