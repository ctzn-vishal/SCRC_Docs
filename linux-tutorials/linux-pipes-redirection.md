```markdown
---
title: "Linux Pipes and Redirection"
category: "linux-tutorials"
description: "Using redirection symbols (>, >>) to control command output and pipes (|) to chain commands together."
---

# Linux Pipes and Redirection

This tutorial explains how to use redirection symbols (`>` and `>>`) to control where the output of Linux commands goes, and how to use pipes (`|`) to connect the output of one command to the input of another.

## Redirecting Input and Output

By default, Linux commands display their results (standard output) to the screen and take input from the keyboard (standard input). Redirection allows you to change these defaults, often sending output to a file instead of the screen.

### Overwriting Output with `>`

A right angle-bracket `>` (called an "into") on the command line indicates that the output of the command should be placed into the file specified after the symbol, instead of being displayed on the screen.

**Syntax:**

```bash
command > filename
```

**Example:**

```bash
ls > list
```

This command will execute `ls` (list directory contents) and place its output into a file named `list` in the current directory.

**Warning:** If a file named `list` already exists, its previous contents will be **overwritten** without warning.

### Appending Output with `>>`

You can append output to the end of an existing file using a double right angle-bracket `>>` (called an "onto"). If the file does not exist, it will be created.

**Syntax:**

```bash
command >> filename
```

**Example:**

Following the previous example, if the next command entered was:

```bash
date >> list
```

The output of the `date` command (the current date and time) would be **added to the end** of the file called `list`, preserving the original content from the `ls` command.

## Pipes (`|`)

Pipes allow you to connect multiple commands together. The standard output of the command to the left of the pipe symbol is "piped" into the standard input of the command to the right of the pipe. The symbol for this connection is a vertical bar `|` called a pipe.

**Syntax:**

```bash
command1 | command2
```

This takes the output of `command1` and uses it as the input for `command2`.

**Example 1: Paging through long output**

If a directory contains many files, the output of `ls` might scroll off the screen too quickly to read. You can pipe the output of `ls` to the `more` command, which displays output one screen-full at a time.

```bash
ls | more
```

In this case, `ls` generates the directory listing, which is then passed as input to `more`. `more` displays the first page and waits for user input (space bar for next page, `q` to quit).

**Example 2: Searching within a file**

You can use pipes to filter the contents of a file. For instance, use `cat` to display a file's content and pipe it to `grep` to search for specific text within that content.

```bash
cat filename | grep searchstring
```

This command displays the content of `filename` using `cat`, and then `grep` filters that output, showing only the lines containing `searchstring`.
```