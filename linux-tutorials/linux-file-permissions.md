```markdown
---
title: "Linux File Permissions"
category: "linux-tutorials"
description: "Understanding and modifying file and directory permissions using 'ls -l' and 'chmod'."
---

# Linux File Permissions

This document explains how to view and modify file and directory permissions in the Linux environment using the `ls -l` and `chmod` commands. Understanding permissions is crucial for controlling access to your files and ensuring proper security and collaboration on shared systems like the SCRC clusters.

## Viewing File Permissions

Since Linux is designed for multiple users to share files, you have options to allow or deny access to your files and directories for others on the system. Permissions determine who can access a file or directory and what actions they can perform (read, write, execute).

To view the permissions associated with files and directories, use the `ls` command with the `-l` (long format) option:

```bash
ls -l
```

This command lists the contents of the current directory in a detailed format. The permissions are shown at the beginning of each line.

**Example Output:**

```
total 180
drwxr-xr-x 3 ct27 nobody 4096 Apr 5 2023 mywork
drwxr-xr-x 3 ct27 nobody 4096 Apr 3 2023 archived-work
-rw-r--r-- 1 ct27 nobody    0 Mar 18 2023 prog.sas7bdat
-rw-r--r-- 1 ct27 nobody 1421 Mar 18 2023 prog.sas7bdat.log
-rw------- 1 ct27 devel Aug 20 10:15 logon
-rwx------ 1 ct27 devel Aug 19 15:23 a.out
-r-xr-xr-x 1 ct27 devel Aug 28 09:48 ls-list
drwx------ 1 ct27 resch Aug 27 15:45 sas-one/
drw------- 1 ct27 resch Aug 27 15:45 tex/
```

### Understanding the Permission String

The first 10 characters on each line represent the file type and its permissions (e.g., `drwxr-xr-x`, `-rw-r--r--`).

1.  **Position 1: File Type**
    *   `d`: Indicates a directory.
    *   `-`: Indicates a regular file.
    *   Other characters exist (e.g., `l` for symbolic link) but `d` and `-` are the most common.

2.  **Positions 2-10: Access Permissions**
    These nine characters are divided into three sets of three, representing permissions for different user classes:
    *   **Positions 2, 3, 4:** Owner permissions (the user who created the file/directory).
    *   **Positions 5, 6, 7:** Group permissions (the group associated with the file/directory).
    *   **Positions 8, 9, 10:** Other permissions (all other users on the system).

### Permission Characters

Within each set of three, the characters represent specific permissions:

*   **`r` (Read):**
    *   *Files:* Allows viewing or copying the file's contents.
    *   *Directories:* Allows listing the contents of the directory (e.g., using `ls`).
*   **`w` (Write):**
    *   *Files:* Allows modifying, renaming, or deleting the file.
    *   *Directories:* Allows creating, deleting, or renaming files *within* the directory. (Requires `x` permission as well).
*   **`x` (Execute):**
    *   *Files:* Allows running the file as a program or script.
    *   *Directories:* Allows entering (changing into) the directory (e.g., using `cd`) and accessing files/subdirectories within it.
*   **`-` (Hyphen):** Indicates that the specific permission is *not* granted.

### Permission Examples

*   `-rw-r--r--`: A regular file (`-`). The owner has read and write (`rw-`) permissions. The group (`r--`) and others (`r--`) have only read permission.
*   `drwxr-x--x`: A directory (`d`). The owner has read, write, and execute (`rwx`) permissions. The group has read and execute (`r-x`) permissions. Others have only execute (`--x`) permission (meaning they can enter the directory if they know the path, but cannot list its contents).
*   `-rwx------`: A regular file (`-`). The owner has read, write, and execute (`rwx`) permissions. The group (`---`) and others (`---`) have no permissions.
*   `drwx------`: A directory (`d`). The owner has read, write, and execute (`rwx`) permissions. The group (`---`) and others (`---`) have no permissions.

## Changing File and Directory Permissions

The `chmod` (change mode) command is used to modify the permission levels of files and directories. You must be the owner of the file/directory or the system administrator to change its permissions.

`chmod` can use symbolic notation to specify permission changes.

### Symbolic Notation

This method uses characters to represent user classes, operators, and permissions.

*   **User Classes:**
    *   `u`: User (owner)
    *   `g`: Group
    *   `o`: Others
    *   `a`: All (equivalent to `ugo`)
*   **Operators:**
    *   `+`: Add permission
    *   `-`: Remove permission
    *   `=`: Set exact permissions (overwriting existing ones)
*   **Permissions:**
    *   `r`: Read
    *   `w`: Write
    *   `x`: Execute

**Syntax:**

```bash
chmod <user_class(es)><operator><permission(s)> <filename/directory>
```

**Examples:**

1.  **Add read, write, and execute permissions for everyone (all users) to `my.dat`:**
    Assume `my.dat` starts with `-rw-r--r--`.

    ```bash
    chmod a+rwx my.dat
    ```

    Resulting permissions: `-rwxrwxrwx`

2.  **Make `my.dat` readable and writable only by the owner:**
    Assume `my.dat` currently has `-rwxrwxrwx`. This requires multiple steps or a combined command.

    *   Remove execute permission for the owner (`u`):
        ```bash
        chmod u-x my.dat
        ```
        Result: `-rw-rwxrwx`
    *   Remove all permissions for the group (`g`):
        ```bash
        chmod g-rwx my.dat
        ```
        Result: `-rw----rwx`
    *   Remove all permissions for others (`o`):
        ```bash
        chmod o-rwx my.dat
        ```
        Result: `-rw-------`

    *Alternatively, set the exact permissions:*
    ```bash
    chmod u=rw,g=,o= my.dat
    ```
    Result: `-rw-------`

3.  **Add execute permission for the owner:**
    ```bash
    chmod u+x script.sh
    ```

4.  **Remove write permission for the group and others:**
    ```bash
    chmod go-w shared_file.txt
    ```
```