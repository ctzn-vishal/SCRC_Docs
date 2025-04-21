# Running Interactive Jobs with FastX

Using FastX with the Stern Slurm cluster provides fast and efficient remote access to graphical applications such as R-Studio, MATLAB, xStata, SAS, and more. This page explains how to access FastX, connect using the client or browser, and start an interactive session on a compute node.

## Accessing FastX

To access FastX, you need your Stern NetID and password.

**Prerequisites:**

*   You must have an activated Stern account. See [Getting An Account](/computing-resources/getting-an-account) if you need help setting up your account.
*   If you are connecting from off-campus (e.g., home), you **must** first connect to the NYU VPN.

**FastX Session Nodes:**

You can connect to any of the following FastX session nodes:

*   [https://fx1.scrc.nyu.edu:3300](https://fx1.scrc.nyu.edu:3300)
*   [https://fx2.scrc.nyu.edu:3300](https://fx2.scrc.nyu.edu:3300)
*   [https://fx3.scrc.nyu.edu:3300](https://fx3.scrc.nyu.edu:3300)

**Login Process:**

1.  Navigate to one of the FastX session node URLs in your web browser.
2.  Log in using your Stern NetID and password.
3.  Once logged in, you will see the FastX home page. This is where you manage your sessions.
4.  To start a new session, click on the **GNOME Terminal** application icon on the left.
5.  Before the session starts, you will be prompted to choose how you want to connect:
    *   **Connect using Browser client:** Use your session within your web browser tab. See [Using FastX in a Browser](#using-fastx-in-a-browser).
    *   **Connect using the Desktop client:** Use the dedicated FastX desktop application. We recommend using the FastX Client for a smoother experience. See [Connecting with the FastX Client](#connecting-with-the-fastx-client).

**Note:** For potentially better performance, you can log in remotely to a physical machine in your office at NYU first and then connect to one of the FastX session nodes from there.

## Connecting with the FastX Client

There are two main ways to use the FastX Desktop Client. First, ensure you have downloaded and installed the client from [StarNet (FastX Client Download)](https://www.starnet.com/fastx/download).

### Option 1: Launching from the Web Interface

1.  Follow the steps in [Accessing FastX](#accessing-fastx) and click the **GNOME Terminal** application icon.
2.  When prompted, select **Connect using the Desktop client**.
3.  The FastX client application should launch automatically and open a GNOME terminal window connected to the FastX session node (`fx1`, `fx2`, or `fx3`).
4.  Proceed to [Using Modules with FastX](#using-modules-with-fastx) to start an interactive job on a compute node.

### Option 2: Launching the Client Directly

1.  Find and start the installed FastX client program on your local machine. You should see a **Connections** window.
2.  Click the **+** icon to create a new connection.
3.  Enter the connection details:
    *   **Host:** `fx1.scrc.nyu.edu` (or `fx2`, `fx3`)
    *   **User:** `<Your Stern NetID>`
    *   **Port:** `22`
    *   **Name:** (Choose a descriptive name, e.g., "SCRC FastX")
4.  Click **Save**.
5.  Double-click the connection you just created in the **Connections** window.
6.  Enter your Stern password when prompted. The session window will appear.
7.  Click the **+** icon in the session window to show the available applications.
8.  Double-click the **GNOME Terminal** application to start a terminal session on the FastX session node.
9.  Proceed to [Using Modules with FastX](#using-modules-with-fastx) to start an interactive job on a compute node.

## Using FastX in a Browser

1.  Follow the steps in [Accessing FastX](#accessing-fastx) and click the **GNOME Terminal** application icon.
2.  When prompted, select **Connect using Browser client**.
3.  A new browser tab will open, displaying a GNOME terminal session connected to the FastX session node (`fx1`, `fx2`, or `fx3`).
4.  Proceed to the next section [Using Modules with FastX](#using-modules-with-fastx) to start an interactive job on a compute node.

## Using Modules with FastX

Whether you connected via the Desktop Client or the Browser, you will now have a terminal window open. This terminal is connected to one of the FastX **login nodes** (`fx1`, `fx2`, or `fx3`).

**Important:** The FastX login nodes (`fx1`, `fx2`, `fx3`) have limited software installed and are **not intended for computational tasks**. You must request an interactive session on a compute node to run research applications.

You can see the limited modules available on the login node by typing:

```bash
module avail
```

### Logging in to an Interactive Compute Node

To run interactive jobs, use the `srun` command to request resources and start a session on a compute node.

```bash
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
```

**Command Breakdown:**

*   `srun`: The Slurm command to run a job interactively.
*   `--pty`: Allocate a pseudo-terminal for the interactive session.
*   `--mem=8gb`: Request 8 gigabytes of memory for the job. Adjust as needed.
*   `--time=1:00:00`: Set a maximum wall-clock time limit of 1 hour. Adjust as needed (e.g., `--time=4:00:00` for 4 hours).
*   `--cpus-per-task=1`: Request 1 CPU core. Adjust as needed.
*   `--nodes=1`: Request 1 compute node.
*   `/bin/bash`: Execute the Bash shell once the resources are allocated.

**Optional Parameters:**

*   `--partition=gpu`: Request a node with GPUs.
*   `--partition=bigmem`: Request a node with a large amount of RAM.

After running `srun`, your command prompt will change, indicating you are now logged into a compute node (e.g., `compute-0-1`).

### Loading Modules and Running Applications on the Compute Node

Once logged into an interactive compute node via `srun`:

1.  **Check available software:** Use the `module avail` command again to see the full list of software modules available on the compute nodes.

    ```bash
    module avail
    ```

2.  **Load a module:** Use the `module load` command followed by the module name and version (if needed). For example, to load R:

    ```bash
    module load R/4.0.2
    ```
    *(Replace `R/4.0.2` with the desired software and version shown by `module avail`)*

3.  **Run the application:** Launch the graphical application by typing its command name. For example, to start RStudio after loading the R module:

    ```bash
    rstudio &
    ```
    *(Using `&` runs the application in the background, freeing up your terminal.)*

The graphical application (e.g., RStudio) should now open in a new window managed by your FastX session. You can continue using the terminal to load other modules or run commands.

**Terminating Sessions:**

*   To exit the interactive compute node session (`srun`), type `exit` in the terminal.
*   To close the FastX session entirely, close the terminal window(s) and either close the FastX client application or log out from the FastX web interface. You can also manage (terminate) sessions from the FastX home page.