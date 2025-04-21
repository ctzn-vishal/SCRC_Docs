```markdown
---
title: "Running GUI Applications (RStudio, XStata, Jupyter)"
category: "software-and-applications"
description: "Guides for running graphical applications like RStudio, XStata, and Anaconda/Jupyter notebooks within interactive sessions on SLURM."
---

# Running GUI Applications (RStudio, XStata, Jupyter)

This guide provides instructions on how to run graphical user interface (GUI) applications such as RStudio, XStata, and Jupyter Notebooks on the SCRC Slurm cluster. These applications require an interactive session initiated through FastX.

## Prerequisites

Before you begin, ensure you have the following:

1.  **SCRC Account:** You need an active Stern NetID and password. Refer to the [Getting an Account documentation](../getting-started/account-access.md#getting-an-account) if you need access.
2.  **NYU VPN:** If you are connecting from off-campus, you must first connect to the [NYU VPN](https://www.nyu.edu/life/information-technology/getting-connected/vpn.html).
3.  **FastX Access:** You will need to connect to the SCRC environment using FastX, either through a web browser or the desktop client.

## General Workflow

Running GUI applications on the Slurm cluster generally involves these steps:

1.  **Connect via FastX:** Establish a session to one of the FastX nodes.
2.  **Start a Terminal:** Launch a GNOME Terminal within your FastX session.
3.  **Start an Interactive Slurm Job:** Use the `srun` command to request resources and start an interactive session on a compute node.
4.  **Load the Software Module:** Use the `module load` command to make the desired application available in your environment.
5.  **Launch the Application:** Run the command to start the GUI application.

## Connecting with FastX

FastX provides remote access to graphical applications.

**Available FastX Nodes:**

*   `https://fx1.scrc.nyu.edu:3300`
*   `https://fx2.scrc.nyu.edu:3300`
*   `https://fx3.scrc.nyu.edu:3300`

Log in using your Stern NetID and password.

**Option 1: Using the Browser Client**

1.  Access one of the FastX URLs above in your web browser.
2.  Log in with your Stern credentials.
3.  From the FastX home page, click the **GNOME Terminal** application icon on the left.
4.  Choose "Connect using Browser client". A terminal session will open in a new browser tab.

**Option 2: Using the Desktop Client (Recommended)**

1.  Download and install the [FastX Desktop Client](https://starnet.doit.wisc.edu/software/fastx/).
2.  Start the client and click the **+** icon to create a new connection.
3.  Enter the following details:
    *   Host: `fx1.scrc.nyu.edu` (or `fx2` or `fx3`)
    *   User: `<Your Stern NetID>`
    *   Port: `22`
    *   Name: (e.g., "SCRC FastX")
4.  Double-click the newly created connection and enter your Stern password when prompted.
5.  Click the **+** icon within the active connection window to show available applications.
6.  Double-click the **GNOME Terminal** application to start a terminal session.

## Starting an Interactive SLURM Session

Once you have a terminal open within your FastX session, you need to start an interactive job on a compute node using the `srun` command. This allocates resources like CPU, memory, and time for your graphical application.

**Example `srun` Command:**

```bash
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
```

**Command Parameters:**

*   `srun`: The command to submit an interactive job.
*   `--pty`: Allocates a pseudo-terminal, necessary for interactive sessions.
*   `--mem=8gb`: Requests 8 gigabytes of memory for the job. Adjust as needed.
*   `--time=1:00:00`: Sets the maximum wall-clock time limit for the job (e.g., 1 hour). Your session will end when this time expires.
*   `--cpus-per-task=1`: Requests 1 CPU core. Adjust as needed.
*   `--nodes=1`: Requests 1 compute node.
*   `/bin/bash`: Specifies that a Bash shell should be started on the allocated node.

**Optional Partitions:**

*   To request a node with GPUs (e.g., for specific computations within Jupyter): add `--partition=gpu`
*   To request a node with high memory: add `--partition=bigmem`

After running `srun`, your command prompt will change, indicating you are now logged into a compute node.

## Running Specific Applications

Once inside your interactive Slurm session, you can load the required software module and launch the application.

### RStudio

1.  **Load the RStudio module:**
    ```bash
    module load rstudio
    ```
    *Note: Depending on the configuration, you might need to load a specific R version first (e.g., `module load R/4.3.2`) before loading `rstudio`.*

2.  **Launch RStudio:**
    ```bash
    rstudio
    ```
    RStudio will open in a new window within your FastX session. You can open scripts, run code in the console, and manage your R environment.

### XStata

1.  **Load the XStata module:** (Replace `17.0` with the desired version if different)
    ```bash
    module load xstata-se/17.0
    ```

2.  **Launch XStata:**
    ```bash
    xstata
    ```
    The XStata graphical interface will open. You can enter commands in the command window or run `.do` files.

### Anaconda / Jupyter Notebook

1.  **Load the Anaconda module:** (Replace `py3.9` with the desired version if different)
    ```bash
    module load anaconda3/py3.9
    ```

2.  **Launch Jupyter Notebook:**
    ```bash
    jupyter-notebook
    ```
    Jupyter Notebook will typically launch in a Chromium browser window within your FastX session. You can navigate directories, create new notebooks (Python 3, R, etc., depending on installed kernels), or open existing ones.

## Important Notes

*   **Check Available Modules:** Before loading, you can see all available software modules on the compute node by running:
    ```bash
    module avail
    ```
    Or search for a specific module:
    ```bash
    module avail <software_name>
    ```
*   **Time Limits:** Remember that your interactive session runs within the time limit specified in the `srun` command (`--time`). The application and your session will terminate when the time expires. Save your work frequently.
*   **Resource Allocation:** Ensure you request sufficient memory (`--mem`) and CPUs (`--cpus-per-task`) for your application to run effectively.
```