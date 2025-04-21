# Connecting to SCRC Clusters

This guide explains how to connect to the NYU Stern Center for Research Computing (SCRC) cluster login nodes using a Secure Shell (SSH) connection from various operating systems (Mac, Linux, Windows). It also covers the requirement for using the NYU VPN when connecting from off-campus.

## Overview: Command Line Interface (CLI)

The primary method for accessing SCRC servers is through a Command Line Interface (CLI) using a terminal application. The CLI is a text-based interface where you interact with the remote Linux host by typing commands.

You will use your Stern NetID and password to authenticate.

## SCRC Login Hosts

You can connect to either of the following SCRC remote login hosts:

*   `rnd.scrc.nyu.edu`
*   `vleda.scrc.nyu.edu`

## VPN Requirement for Off-Campus Access

If you are connecting from a location outside the NYU network (e.g., your home), you **must first connect to the NYU VPN**. Once the VPN connection is established, you can proceed with the SSH connection steps as if you were on the NYU network.

If you are already connected to the NYU network (e.g., on campus), you do not need the VPN and can connect directly.

## Connecting from Mac/Linux

1.  Open your Terminal application (e.g., Terminal on Mac, or any terminal emulator on Linux).
2.  Use the `ssh` command followed by your Stern NetID, the `@` symbol, and the hostname of one of the login nodes.

    Replace `your_netid` with your actual Stern NetID (e.g., `xy12`).

    ```bash
    ssh your_netid@rnd.scrc.nyu.edu
    ```

    Alternatively, you can connect to the `vleda` node:

    ```bash
    ssh your_netid@vleda.scrc.nyu.edu
    ```

3.  When prompted, enter your Stern password. Note that the password will not be displayed on the screen as you type.

## Connecting from Windows

Windows users have several options for connecting via SSH:

*   **Windows Command Prompt (`cmd`) / PowerShell:** Modern versions of Windows 10 and 11 include a built-in SSH client.
    1.  Open Command Prompt or PowerShell.
    2.  Use the `ssh` command exactly as shown in the [Connecting from Mac/Linux](#connecting-from-maclinux) section.
        ```bash
        ssh your_netid@rnd.scrc.nyu.edu
        ```
    3.  Enter your Stern password when prompted.

*   **Windows Subsystem for Linux (WSL2):** If you have WSL2 installed (available on Windows 10 and later), you can install a Linux distribution (like Ubuntu) and use its native terminal and `ssh` client.
    1.  Open your WSL terminal (e.g., Ubuntu).
    2.  Use the `ssh` command as shown in the [Connecting from Mac/Linux](#connecting-from-maclinux) section.
        ```bash
        ssh your_netid@rnd.scrc.nyu.edu
        ```
    3.  Enter your Stern password when prompted.
    *   **Note:** If using WSL2, you might encounter issues accessing the internet when the Cisco AnyConnect VPN (installed via `.exe`) is active. A possible solution is to uninstall the standard Cisco AnyConnect client and install the [AnyConnect app from the Microsoft Store](https://apps.microsoft.com/store/detail/anyconnect/9WZDNCRDFJ3D), then configure the VPN connection using NYU IT's provided settings.

*   **PuTTY:** PuTTY is a popular free and open-source SSH and telnet client for Windows.

### Using PuTTY

1.  **Download PuTTY:** Download the latest installer from the official [PuTTY Download Page](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
2.  **Install PuTTY:** Run the downloaded installer and follow the on-screen instructions.
3.  **Launch PuTTY:** Open the installed PuTTY application.
4.  **Configure Session:**
    *   In the **Host Name (or IP address)** field, enter one of the SCRC login hostnames:
        *   `rnd.scrc.nyu.edu`
        *   or `vleda.scrc.nyu.edu`
    *   Ensure the **Port** is set to `22`.
    *   Ensure the **Connection type** is set to `SSH`.
    *   *(Optional)* You can save these settings for future use by typing a name in the **Saved Sessions** field (e.g., "SCRC RND") and clicking **Save**.
5.  **Connect:** Click the **Open** button.
6.  **Security Alert (First Connection):** The first time you connect to a host, PuTTY will display a security alert dialog box starting with "The server's host key is not cached...". This is normal. Click **Yes** (or **Accept**) to trust the host and cache its key.
7.  **Login:** A terminal window will open. You will be prompted to log in:
    *   At the `login as:` prompt, type your Stern NetID and press Enter.
    *   At the `password:` prompt, type your Stern password and press Enter. (The password will not be shown as you type).

You should now be logged into the SCRC cluster and see a command line prompt (e.g., `[your_netid@rnd ~]$`). You can now enter Linux commands.