```markdown
---
title: "Transferring Files"
category: "storage-solutions"
description: "Instructions for transferring files between your local computer and SCRC servers using FileZilla."
---

# Transferring Files

This document provides instructions on how to transfer files between your local computer (Windows, Linux, or Mac) and the NYU Stern Center for Research Computing (SCRC) Linux servers using the FileZilla graphical SFTP client.

## FileZilla Overview

FileZilla is a free and open-source file transfer program that supports FTP, FTPS, and SFTP. It provides a graphical user interface for transferring files between a local machine and a remote server, simplifying the process compared to command-line tools.

*   [FileZilla website](https://filezilla-project.org/)

## Using FileZilla (Windows, Linux, and Mac)

Follow these steps to connect to SCRC servers and transfer files using FileZilla:

1.  **Download and Install:** Download the FileZilla client suitable for your operating system from the [FileZilla website](https://filezilla-project.org/), install it, and then launch the application.

2.  **Connect to NYU VPN (If Off-Campus):** If you are connecting from a location outside the NYU network (e.g., your home), you must first connect to the [NYU VPN](https://www.nyu.edu/life/information-technology/getting-connected/vpn.html). If you are already on the NYU network, you can skip this step.

3.  **Enter Connection Details:** In the FileZilla interface, locate the "Quickconnect" bar, typically found at the top of the window. Enter the following details:
    *   **Host:** `sftp://rnd.scrc.nyu.edu` (or `sftp://vleda.scrc.nyu.edu`). Using the `sftp://` prefix ensures you are using the secure SFTP protocol.
    *   **Username:** Your Stern NetID (e.g., `xy12`)
    *   **Password:** Your Stern password
    *   **Port:** `22` (This is the standard port for SFTP)

4.  **Connect:** Click the "Quickconnect" button.

5.  **Trust Host Key (First Connection):** If this is your first time connecting to the server from FileZilla, you may see a warning message about an unknown host key (e.g., `The server's host key is unknown...`). Verify the host key if possible, and then check the box to trust the host and click "OK" or "Yes" to proceed.

6.  **Transfer Files:** Once connected, you will see two main panes:
    *   **Local site (Left pane):** Shows the files and directories on your local computer.
    *   **Remote site (Right pane):** Shows the files and directories in your home directory (`/homedir/employees/<initial>/<netid>`) on the SCRC server (`rnd` or `vleda`).
    *   Navigate to the desired directories in both panes.
    *   To transfer files, simply drag and drop them from one pane to the other.
        *   Drag from Left to Right to upload files from your local computer to the server.
        *   Drag from Right to Left to download files from the server to your local computer.

7.  **Disconnect:** Once you have finished transferring files, you can disconnect from the server by clicking the disconnect icon (often looks like a computer with a red 'X') in the toolbar or by closing FileZilla.
```