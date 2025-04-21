```markdown
---
title: "Linux Introduction and Basic Navigation"
category: "linux-tutorials"
description: "Introduction to the Linux command line, shell prompt, basic commands like pwd, ls, cd, and understanding the directory structure."
---

# Linux Introduction and Basic Navigation

This tutorial introduces the basic Linux commands needed to use and run programs on the SCRC Linux computers, focusing on navigating the file system.

## The Command Line Interface (Shell)

The Linux machines use a command line interface called a Shell. The Shell is the interface where you enter Linux commands. There are many types of shells; by default, SCRC Linux machines use the BASH shell.

When you log in, the first thing you see is the shell's **command prompt**. This indicates the shell is ready to accept your commands. The prompt might look something like this:

```text
[your_netid@hostname ~ ]$
```

## Your Home Directory

When you log in, you start in your **home directory**. Every user has a unique home directory, which is the primary location for storing your personal files and data.

## Basic Navigation Commands

Here are some fundamental commands for navigating the Linux file system:

### Show the present working directory (`pwd`)

To see the complete name and path of the directory you are currently in (the "present working directory"), use the `pwd` command:

```bash
pwd
```

**Example Output:**

```text
/homedir/employees/c/ct27
```

This output shows the full path to the current directory. In this example, `ct27` is the user's home directory, located inside `c`, inside `employees`, inside `homedir`.

### Show contents of a directory (`ls`)

To see a list of the files and sub-directories within the current directory, use the `ls` command. Using the `-l` option provides a detailed "long format" listing:

```bash
ls -l
```

**Example Output:**

```text
total 180
drwxr-xr-x 3 ct27 nobody 4096 Apr  5 2023 mywork
drwxr-xr-x 3 ct27 nobody 4096 Apr  3 2023 archived-work
-rw-r--r-- 1 ct27 nobody    0 Mar 18 2023 prog.sas7bdat
-rw-r--r-- 1 ct27 nobody 1421 Mar 18 2023 prog.sas7bdat.log
```

*   `ls` is the command, and `-l` is an option.
*   Lines starting with `d` indicate directories (`mywork`, `archived-work`).
*   Lines starting with `-` indicate regular files (`prog.sas7bdat`, `prog.sas7bdat.log`).
*   The long format shows permissions, owner (`ct27`), size (e.g., `1421` bytes), modification date, and name.
*   Using `ls` without options typically shows only the names of files and directories.

### Create a sub-directory (`mkdir`)

To create a new directory (folder) inside your current directory, use the `mkdir` (make directory) command, followed by the desired directory name:

```bash
mkdir costProject
```

This creates a new sub-directory named `costProject`. You can verify its creation using `ls -l`.

**Note:** Linux file and directory names are case-sensitive. `costProject` is different from `costproject`.

### Change Directory (`cd`)

To move into a different directory, use the `cd` (change directory) command, followed by the name of the directory you want to enter:

```bash
cd costProject
```

After running this command, your present working directory becomes `/homedir/employees/c/ct27/costProject` (in this example). You can verify this using `pwd`.

To move *up* one level in the directory structure (to the parent directory), use `cd ..`:

```bash
cd ..
```

## The Linux File System Structure

Linux uses a **hierarchical file structure**, often visualized as an upside-down tree.

*   The top-level directory is called the **root directory**, represented by a forward slash (`/`).
*   All other files and directories are located within the root directory or its sub-directories.
*   A **file** can hold text, data, or a program.
*   A **directory** (or folder) contains files and other directories (sub-directories).
*   A **sub-directory** is simply a directory located inside another directory.

Understanding this structure is key to navigating using commands like `pwd`, `ls`, and `cd`.

## Useful Tips and Tools

### Auto Completion in the Shell

The BASH shell offers tab completion. Start typing a command or filename, and press the `Tab` key.

*   If the typed portion is unique, the shell will complete the rest of the name.
*   If there are multiple possibilities, pressing `Tab` a second time will often list them.

### Create or Edit a File (`nano`)

`nano` is a simple, beginner-friendly text editor available on the command line. To create a new file or open an existing one for editing:

```bash
nano my_program.py
```

```bash
nano data_notes.txt
```

Inside `nano`, commands are listed at the bottom. The `^` symbol represents the `Ctrl` key.

*   `Ctrl+O`: Write Out (Save the file)
*   `Ctrl+X`: Exit `nano`

### List the Contents of a File (`more`)

To view the contents of a text file one screen at a time, use the `more` command:

```bash
more my_data.txt
```

*   Press the `Spacebar` to advance to the next page.
*   Press `q` to quit viewing the file and return to the command prompt.

### Breaking Out (`Ctrl+C`)

If a command seems stuck, unresponsive, or you want to cancel the current operation, press `Ctrl+C`. This usually interrupts the running process and returns you to the command prompt.
```