```markdown
# Accessing SCRC Clusters

## Log in to a Terminal Command Line Interface

The most common way to access the SCRC servers is to use a Command Line Interface (CLI) from a terminal application. A CLI is a text-based interface that allows users to interact with a host by entering text commands at the prompt of a terminal application. The SCRC hosts that you connect to are running Linux.

You will use your Stern NetID and password to authenticate to either one of SCRCs remote login hosts:
* `rnd.scrc.nyu.edu`
* `vleda.scrc.nyu.edu`

## If Off Campus, First Connect to the NYU VPN

If you are connecting from a remote location that is not on the NYU network (your home for example), you need to set up your computer to use the NYU VPN. Once you've created a VPN connection, you can proceed as if you were connected to the NYU network. If you're on the NYU network already, you can proceed directly with your connection.

## Log in From Mac/Linux

Open the terminal application and use the `ssh` command to make a secure connection to one of SCRCs remote login hosts. E.g., if your Stern NetID is `xy12`:

```bash
ssh xy12@rnd.scrc.nyu.edu
```

OR

```bash
ssh xy12@vleda.scrc.nyu.edu
```

## Log in From Windows

Windows users have several options:

*   **Command Line:** Open the `cmd` program on an updated Windows 10 or later machine. Type the `ssh` command the same as shown above for Mac/Linux.
*   **WSL2:** If you run Windows 10 or later, you can install Windows Subsystem for Linux (WSL), and then install Ubuntu or other Linux distributions on your machine. You will get a fully functional Ubuntu distribution with a terminal application. Type the `ssh` command the same as shown above for Mac/Linux.
*   **PuTTY:** PuTTY is a free and open-source terminal emulator and network file transfer application that supports logging in with the `ssh` command.

    *   Note: If you are using WSL2, you may not be able to access the internet when Cisco AnyConnect VPN, installed from the .exe file, is activated. A potential solution is to uninstall Cisco AnyConnect and install AnyConnect using Microsoft Store and then set up a new VPN connection using the settings described onthe IT webpage .

### Getting and using PuTTy

PuTTY is free and can be downloaded from [PuTTY Download](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

1.  Download and run the latest installer file from the website.
2.  Follow the on-screen install instructions.
3.  Once installed, start PuTTY, then type `rnd.stern.nyu.edu` or `vleda.stern.nyu.edu` in the Host Name field and click Open.
4.  Note: The first time you log in a dialog may appear which starts with `The server's host key is not cached`. Click Yes in this dialog.
5.  Type your Stern NetID and password at the `login as` and `password` prompts, respectively.

You should now be logged in and see a command line prompt from which you can enter Linux commands or run programs.

# Common SLURM Commands

| Command  | Usage                  | Description                                   | Example                    |
| -------- | ---------------------- | --------------------------------------------- | -------------------------- |
| `sbatch` | `sbatch [options] script` | Submits a batch job to the Slurm scheduler  | `sbatch myScript.sbatch`   |
| `squeue` | `squeue [options]`       | Displays the status of jobs in the queue      | `squeue`                   |
| `sinfo`  | `sinfo [options]`        | Provides information about Slurm nodes and queues | `sinfo`                    |
| `srun`   | `srun [options] executable [arguments]` | Runs a parallel job interactively            | `srun pty mem=8gb time=1:00:00 cpus-per-task=1 nodes=1 /bin/bash` |
| `scancel`| `scancel [options] job_id`| Cancels a pending or running job            | `scancel 1203`            |

# Python Virtual Environment

A Python virtual environment is a personal isolated Python installation. The virtual environment consists of a directory that contains all the necessary executables for a Python project. You can customize this environment by installing additional Python packages.

## General Steps

1.  Creating or Configuring On a login node, create python virtual environment in your bigdata directory. First time only.
2.  Activate
3.  Install packages
4.  Deactivate

## Running as Slurm batch job

In `sbatch` script, include module load and virtual environment activation, e.g.,

```bash
#!/bin/bash
#
# [hello-world.sbatch]
#
#SBATCH --job-name=hello         # Job name
#SBATCH --output=hello.out        # Output file name
#SBATCH --export=ALL             # Export all environment variables
#SBATCH --time=00:01:00          # Set max runtime of job = 1 minute
#SBATCH --mem=4G                 # Request 4 gigabytes of memory
#SBATCH --mail-type=BEGIN,END,FAIL # Send email notifications
#SBATCH --mail-user=you@stern.nyu.edu # email TO
#SBATCH --partition=test       # Specify the partition to submit the job to

module purge                   # Start with a clean environment
module load python/3.9.7       # Load python module

source ~/bigdata/05-virtenvs/py3.9/bin/activate  # activate virt env
python hello-world.py          # Run python
```

Submit job:

```bash
sbatch hello-world.sbatch
```

## How to Create a Python virtual environment

Note: Always create virtual environments in your `bigdata` directory. If you do not have a `bigdata` directory, email `scrc-list@stern.nyu.edu` to request one.

1.  Load the Python module.

    ```bash
    module load python/3.9.7
    ```

2.  Create the virtual environment and specify the location. For example

    ```bash
    virtualenv ~/bigdata/05-virtenvs/py3.9
    ```

    You only need to create the virtual environment once but you can create multiple virtual environments with different versions and flavors of Python.
3.  Activate

    ```bash
    source ~/bigdata/05-virtenvs/py3.9/bin/activate
    ```

    Notice the name of the active virtual environment is prepended to your prompt
4.  Install Python modules with `pip`

    *   See modules currently installed

        ```bash
        pip list
        ```

    *   Install a new module

        ```bash
        pip install requests
        ```
5.  Deactivate

    ```bash
    deactivate
    ```

# Getting an Account

## Stern users

For those in the Stern School of Business, you can use your existing activated Stern account, i.e., Stern NetID and password, to access SCRC services and resources. If you haven't already, activate your Stern account.

## Non-Stern NYU users

Those already at NYU but not in Stern (and not enrolled in a Stern course) must have a full-time Stern employee make a request on their behalf by contacting the Stern IT Help Desk at `helpdesk@stern.nyu.edu` or 212-998-0180 and provide the following information:

*   Full Name
*   NYU NetID
*   NYU UniversityID (N#)
*   Date of birth
*   Sponsor's name (Stern faculty or employee)
*   Sponsoring department
*   Expiration date (max 1 year; extensions may be requested yearly)

Activate your Stern account to use SCRC services.

## Non-NYU users

Non-NYU affiliated users must first obtain an NYU account by having an authorized sponsor request an NYU NetID on their behalf by filling out the [IT Onboarding Form](https://identity.it.nyu.edu/).  It is accessed by logging into the [NYU VPN](https://www.nyu.edu/life/information-technology/getting-connected/vpn.html), then logging into identity.it.nyu.edu , clicking the hamburger menu, selecting Request Affiliate, and then Request Affiliate User. For additional help contact NYU IT support at AskIT@nyu.edu or 212-998-3333.

# Getting Started with Slurm Interactive Jobs

Using FastX with the Stern Slurm cluster provides fast and efficient remote access to graphical applications such as R-Studio, MATLAB, xStata, SAS, and more.

## Accessing FastX

You will login with your Stern account. If you are not on campus, make sure you are logged in to the NYU VPN and then you have two options.

*   Login directly into one of the FastX session nodes.
*   Login remotely to a physical machine in your office at NYU and then into one of the FastX session nodes (better performance)

These are the available FastX session nodes.

*   [https://fx1.scrc.nyu.edu:3300](https://fx1.scrc.nyu.edu:3300)
*   [https://fx2.scrc.nyu.edu:3300](https://fx2.scrc.nyu.edu:3300)
*   [https://fx3.scrc.nyu.edu:3300](https://fx3.scrc.nyu.edu:3300)

Log in using your Stern credentials. Visit [Getting An Account](#getting-an-account) if you need help with setting up your account.

Once logged in, you will see the FastX home page. This is where you will start, terminate and manage your sessions. To start a New Session, click on the GNOME Terminal application on the left. This will launch a new Terminal session. Before you are taken to the session, you will have the option to choose how you want to connect to the session:

You have two options:

*   Connect using Browser client: Use your session in a browser window. See the section [Using FastX in a Browser](#using-fastx-in-a-browser) below.
*   Connect using the Desktop client: To use the client, download and install it from [Download the FastX Client](https://starnet.doit.wisc.edu/software/fastx/). We recommend using FastX Client for a smoother experience.

## Connecting with the FastX Client: Option 1

If you select the Desktop Client, a Gnome terminal window opens. Next, see [Using Modules with FastX](#using-modules-with-fastx). For a specific program example see [Run XStata on SLURM](link-to-xstata).

## Connecting with the FastX Client: Option 2

You can start the FastX client directly.

1.  Find and start the installed FastX client program on your local machine. You should see a Connections window.
2.  Next, to create a new connection click the + icon and login to one of the fx session nodes, e.g.,
    *   Host: `fx1.scrc.nyu.edu` (or `fx2` or `fx3`)
    *   User: `<Your Stern NetID>`
    *   Port: `22`
    *   Name: (can be anything you want)

3. Next, you see a window with the connection to the fx node. The connection is not active until you double-click it and enter your Stern password. Once active the session window looks similar to...
4.  Click the + icon to show the application window.
5.  Double-click the GNOME Terminal application to start a terminal session.

Next, see [Using Modules with FastX](#using-modules-with-fastx). For a specific program example see [Run XStata on SLURM](link-to-xstata).

## Using FastX in a Browser

If you chose to connect to a session with the Browser Client, a terminal session will open in a new tab in your browser.

1.  Double-click the GNOME Terminal application to start a terminal session.

Next, see the next section [Using Modules with FastX](#using-modules-with-fastx). For a specific program example see [Run XStata on SLURM](link-to-xstata).

## Using Modules with FastX

Once you have the Terminal open on one of the FastX nodes, to list the available software, type:

```bash
module avail
```

This brings up a list of all installed modules on the fx login node

Note that on the fx login node, you are limited to a few basic applications. This node is not intended for computational tasks.

## Logging in to an interactive node

To run interactive jobs, we have to use the `srun` command to log in to an interactive job node. You can see what nodes are available using `sinfo`:

```bash
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
```

*   `srun`: Command to submit a job to the Slurm scheduler.
*   `--pty`: Allocate a pseudo-terminal for interactive job execution.
*   `--mem=8gb`: Request 8 gigabytes of memory for the job.
*   `--time=1:00:00`: Set a time limit of 1 hour for the job's execution.
*   `--cpus-per-task=1`: Request 1 CPU core per task.
*   `--nodes=1`: Request 1 compute node for the job.
*   `--partition=gpu`: Request a node with gpus. (optional)
*   `--partition=bigmem`: Request a node with a lot of RAM. (optional)
*   `/bin/bash`: Execute the Bash shell as the job's command.

You will see that you are logged in to one of the interactive nodes. Use `module avail` here to see available software packages:

## Loading a module

To load RStudio, type in the following command:

```bash
module load R/4.0.2
```

Now run the following command to open RStudio:

```bash
rstudio
```

You should see an RStudio window open up.

# Install Local R Packages

In this tutorial, you will install R packages to your RStudio environment. R packages increase the power of R by improving existing base R functionalities, or by adding new ones.

## Repositories

Repositories are where packages are located so you can install them from it. Three popular repositories are:

*   **CRAN:** The official repository maintained by R community.
*   **Bioconductor:** Topic-specific repository, intended for open-source software for bioinformatics
*   **Github:** Popular repository site for open-source projects

## Installing packages

Make sure you are in an interactive node, and have R loaded and RStudio opened. For specific instructions, see [Getting Started with Slurm Interactive Jobs](#getting-started-with-slurm-interactive-jobs). Make sure to have the Console open in RStudio. We will be typing in commands here.

### Installing from CRAN

CRAN packages can be installed directly using the following command:

```R
install.packages("package")
```

For example, to install `vioplot` package, we will use:

```R
install.packages("vioplot")
```

To install more than one package at a time, use a character vector as follows:

```R
install.packages(c("vioplot", "MASS"))
```

Often, packages have different mirrors. Here is a [list of available mirrors](https://cran.r-project.org/mirrors.html). To use a specific mirror, use the `repo` parameter:

```R
install.packages("vioplot", repo = "https://lib.ugent.be/CRAN/")
```

### Installing Bioconductor packages

Detailed instructions can be found at the [official site](https://www.bioconductor.org/install/).

1.  First, we install basic functions needed to install Bioconductor packages. Execute the following script:

    ```R
    install.packages("BiocManager")
    ```

2.  Get a [list of available software packages](https://www.bioconductor.org/packages/release/BiocViews.html#___Software).

3.  To check available packages programmatically, use the following command:

    ```R
    BiocManager::available()
    ```

4.  Install specific packages, e.g., `GenomicFeatures` and `AnnotationDbi`, with:

    ```R
    BiocManager::install(c("GenomicFeatures", "AnnotationDbi"))
    ```

### Installing GitHub (and other) packages via `devtools`

You can install `devtools`, an R package that makes installation easier using the following command:

```R
install.packages("devtools")
```

After `devtools` is installed, you will be able to use the utility functions to install another packages. Here is more [documentation on devtools](https://cran.r-project.org/web/packages/devtools/devtools.pdf).

The basic options are:

*   `install_bioc()` from Bioconductor
*   `install_bitbucket()` from Bitbucket
*   `install_cran()` from CRAN
*   `install_git()` from a git repository
*   `install_github()` from GitHub
*   `install_local()` from a local file
*   `install_svn()` from a SVN repository
*   `install_url()` from a URL
*   `install_version()` from a specific version of a CRAN package.

For example, to install `babynames` package from GitHub, run the following command:

```R
devtools::install_github("hadley/babynames")
```

## Removing packages

You can remove packages using the following command:

```R
remove.packages("vioplot")
```

## Updating Packages

To check what packages need update, type:

```R
old.packages()
```

To update a specific package, run the install command again:

```R
install.packages("vioplot")
```

To update all packages, use:

```R
old.packages()
```

## Using GUI to install packages

While we recommend using Console since it's faster, RStudio has a GUI option for installing packages. You can find it under `Tools > Install Package`, and there you have a pop-up window to type the package you want to install.

# Linux Tutorial

For an in-depth tutorial, you can navigate to this [Linux guide](http://linuxcommand.org/tlcl.php): [Learning the Shell](http://linuxcommand.org/tlcl.php).

This tutorial demonstrates the basic Linux commands a user would need to use and run programs on the SCRC Linux computers. The Linux machines use a command line interface called a Shell. The Shell is the interface where you enter Linux commands. There are many types of shells. By default, SCRC Linux machines use the BASH shell.

The first thing you see after logging in is the shell's command prompt. For example, Christine Thomass' prompt might look something like this:

```
[ct27@rnd ~ ]$
```

## Your Home Directory

Once logged in, you are deposited into your home directory. Every user has a home directory. Your home directory is where you will store most of your files.

### Show the present working directory

To see the complete name and path of the current working directory, use the command

```bash
pwd
```

Example output:

```
/homedir/employees/c/ct27
```

This prints the full directory path. Here, Christine's home directory name is `ct27` which is contained within a directory called `c` which is inside the directory `employees` inside the directory `homedir`. The Linux directory structure is a hierarchical tree structure.

### Show contents of a directory

To see a list of the files and directories in the current directory type `ls -l` (list directory contents using long format), e.g.,

```bash
ls -l
```

Example output:

```
total 180
drwxr-xr-x 3 ct27 nobody 4096 Apr 5 2023 mywork
drwxr-xr-x 3 ct27 nobody 4096 Apr 3 2023 archived-work
-rw-r--r-- 1 ct27 nobody 0 Mar 18 2023 prog.sas7bdat
-rw-r--r-- 1 ct27 nobody 1421 Mar 18 2023 prog.sas7bdat.log
```

`ls` is the command and `-l` is, in this example, the option for the command. The `-l` option formats the results into long format. Long format lists more than just the names of the files which is what `ls` alone would show.

In this example, the output shows two directories `mywork` and `archived-work` (notice the `d` at the beginning of the line), and two files `prog.sas7bdat` and `prog.sas7bdat.log`. Some other information we see, e.g., the size of the log file is `1421` bytes, its owner is `ct27`, its last modification date is `Apr 5 2023`.

### Auto Completion in the Shell

Press the `Tab` key after enough of the word you are trying to complete has been typed in. If when hitting tab the word is not completed there are probably multiple possibilities for the completion. Press tab again and it will list the possibilities.

### Create a sub-directory

Say you would like to work on a project. It is probably convenient to create a sub-directory to hold the projects files, i.e., program, data and results. To create a directory use the `mkdir` (make directory) command, e.g.,

```bash
mkdir costProject
```

This command creates a new directory called `costProject` inside the current directory. Verify this by typing `ls -l`.

**Note:** Linux is case sensitive, so for example `costproject` is not the same as `costProject`.

### Change to a subdirectory

To change into the `costProject` directory, i.e., make it the current directory, use the `cd` (change directory) command, e.g.,

```bash
cd costProject
```

Verify that we are in the `costProject` directory using `pwd`.

```bash
pwd
```

Example output:

```
/homedir/employees/c/ct27/costProject
```

### Create or edit a file

`nano` is a simple text editor used to create or edit a data or program file, etc. For example, to edit a file called `costdata.dat` type,

```bash
nano costdata.dat
```

Along the bottom of the `nano` editor are the editor's commands. The character `^` is the `ctrl` key. To save the file you type `ctrl-o` and then to exit `nano` type `ctrl-x`.

### List the contents of a file

The `more` command displays the contents of a file, one screen-full at a time. Press the space bar to move forward screen by screen until the end of the file is reached or press the letter `q`, for quit., E.g.,

```bash
more costdata.dat
```

If the file contents are larger than can be shown in one page, the `more` command shows you the first page and halts. To see the next page press the space bar and to quit type `q`.

### Breaking out

If you get stuck or hung after typing a command, etc., then use `ctrl-c` to break out or cancel your current command. `ctrl-c` returns you to the command prompt.

## Linux Tutorial Continued Commands

Most Linux commands are short, typically an abbreviation or mnemonic for what the command does. For example, the command to delete a file is `rm` which is short for remove.

**Recall:** Linux is case-sensitive, i.e., it distinguishes between lowercase and uppercase (recognizing commands in lowercase only).

Most commands follow a common syntax:

```bash
command -options arguments
```

Here are some examples of basic Linux commands and command syntax.

*   To list all of the files in your current directory, type

    ```bash
    ls
    ```

*   To get a long listing of the files in your current working directory including information on size, date of modification and permissions, type

    ```bash
    ls -l
    ```

*   To make a copy of a file and give it a new name, type

    ```bash
    cp costdata.dat costdata.dat.bak
    ```

*   To remove (delete) a file, type

    ```bash
    rm costdata.dat
    ```

    **Note:** There is no undo in Linux therefore once a file has been deleted there is no easy way to recover it.

*   To rename (move) a file, type

    ```bash
    mv costdata.dat.bak newcostdata.dat
    ```

*   To create a sub-directory, type

    ```bash
    mkdir study1
    ```

*   To change (move down) into the new directory, type

    ```bash
    cd study1
    ```

*   To change (move up) to the previous directory, type

    ```bash
    cd ..
    ```

*   To remove a directory, type

    ```bash
    rmdir study1
    ```

*   To remove ALL files in the current directory whose name begins with `costdata`, type

    ```bash
    rm costdata *
    ```

    The asterisk (`*`) is a wildcard character that matches one or more characters. Be VERY careful with removing files and using the `*` wildcard character. You might end up permanently deleting more than you intended. Always do a list first, e.g., `ls costdata*` to show the files that would be deleted with the `rm costdata*` command.

## Redirecting Input and Output

Commands usually display their results to the screen. Also, commands normally operate on data as you type it in from the keyboard. A right angle-bracket `>` (called an "into") on the command line indicates that the next word is the name of a file or device in which to place, or redirect the output of a command, e.g.,

```bash
ls > list
```

will place the output of the `ls` command in a file named `list`. If a file named `list` existed before you entered this command, any previous contents will be over written.

You can append to the end of a file using a double right angle-bracket `>>` (called an "onto"). For example, if the next command entered was:

```bash
date >> list
```

The output of the `date` command would be added to the bottom of the file called `list`.

## Pipes

The output of one command can be fed as input into to another command. The symbol for the input/output (I/O) connection is a vertical bar `|` called a pipe.

For example, a directory containing many files will scroll off the screen if just `ls` is used. If a pipe is used to direct the output of `ls` to be the input of `more`, then the directory listing will be shown one screen-full at a time and will not scroll off the screen.

```bash
ls | more
```

## Online Help

To get on-line help in Linux, use the `man` command. It provides access to a comprehensive online Linux manual. Type `man` followed by a command or topic on which you want help.
```


```markdown
# Linux Command Line and Slurm Tutorials

## Online Manual

To make the online manual more helpful, an index is provided. The index is accessed with the `-k` option of the `man` command.

Example:

```bash
man -k directory
```

This will display a one-line synopsis of all manual pages having to do with directories.

## The Linux File System

Linux uses a hierarchical file structure, which is made up of files, directories, and sub-directories.

*   A file can hold text, data, or a program.
*   Directories contain files and sub-directories.
*   A sub-directory is a directory that has been created within another directory.

You can also use the `--help` option to get a description of the commands usage. Simply type your command whose usage you to know in the terminal with `--help` after a space and press enter. And youll get the complete usage of that command as shown below.

An example below:

```bash
cat --help
```

## File Permissions

Since Linux is set up to let users share files, you have the option of allowing or denying access to others on the system. Permissions determine who may access your files and directories or what may be done with a file or a directory.

Use `ls -l` to see what permissions your files and directories have.

Example output:

```
-rw------- 1 ct27 devel Aug 20 10:15 logon
-rwx------ 1 ct27 devel Aug 19 15:23 a.out
-r-xr-xr-x 1 ct27 devel Aug 28 09:48 ls-list
drwx------ 1 ct27 resch Aug 27 15:45 sas-one/
drw------- 1 ct27 resch Aug 27 15:45 tex/
```

The characters `d`, `r`, `w`, `x`, and `-` at the far left indicate the permission of each file and directory. There are 10 positions.

*   **Position 1:** The directory indicator.
*   **Positions 2,3,4:** Apply to the owner (creator).
*   **Positions 5,6,7:** Apply to the group.
*   **Positions 8, 9,10:** Apply to all users.

The meaning of the letters are:

*   **d (directory):** If the first letter is a `d`, the file is a directory. If the first character is a hyphen (`-`), then it is a regular file.
*   **r (readable):** A file must be readable to be looked at or copied. A directory must be readable for you to list its contents.
*   **w (writable):** A file must be writable in order for you to modify it, remove it, or rename it. A directory must be writable in order for you to add or delete files in it.
*   **x (executable):** A file with executable permissions is one you can run, such as a program or a shell script. A directory must be executable in order for you to move into it (using the `cd` command), list its contents, or create or delete files there.
*   **- (hyphen):** Appears when the permission is switched off.

### Examples

*   The file is read/write for owner, read only for others: `-rw-r--r--`
*   The directory is read/write/search for owner, read/search for group, searchable only for others: `drwxr-x--x`

### Changing File and Directory Permissions

The file and directory permission levels in Linux can be changed to allow or deny access to other users. The `chmod` command is used to set the protection level.

You can add or remove protection levels by using either `+` (add) or `-` (remove) with `chmod` and a letter signifying a class of users:

*   `u`: for the file owner
*   `g`: for a system defined group
*   `o`: for users in neither `u` or `g`
*   `a`: for all users

and the desired access settings:

*   `r`: for read access
*   `w`: for write access
*   `x`: for execute access

Example:

To change the file called `my.dat` with the permissions `-rw-r--r--` to read/write/execute for all users (owner, group, and other) type the command:

```bash
chmod a+rwx my.dat
```

The resultant permissions would be: `-rwxrwxrwx`

Now, change the permissions of `my.dat` so that only the owner can read, modify or delete it:

```bash
chmod u-x my.dat
chmod g-rwx my.dat
chmod o-rwx my.dat
```

The resulting permissions are: `-rw-------`

## Command History

The most recent commands typed at the command line interface are saved and can be viewed or retrieved for re-use. Access the history by pressing the up arrow.

To search for a command in the history type `ctrl-r`, type the search text, then press enter to re-execute or `ctrl-c` to abort.

## Basic Cursor Movement, Cut, Paste and Undo

*   `ctrl-a`: move cursor to beginning of line
*   `ctrl-e`: move cursor to end of line
*   `ctrl-k`: cut everything after the cursor
*   `ctrl-y`: paste the last thing cut
*   `ctrl-_`: undo

## Command Summary

*   `cat`: display contents of a file
*   `cd dir`: moves you to directory called `dir`
*   `pwd`: diplay the current working directory
*   `chmod permissions`: sets permissions on a file
*   `clear`: clear screen
*   `cp file1 file2`: copies a file
*   `diff file1 file2`: compare two files
*   `exit`: exit Linux shell
*   `file`: lists file type of given file
*   `find name filename`: search for file called `filename`
*   `grep search-string`: search for files containing search-string
*   `cat file | grep searchstring`: search file for the text searchstring
*   `head`: displays top lines of a file
*   `history`: displays recently entered commands
*   `ls`: lists the contents of a directory
*   `ls -l`: like `ls`, but in long format
*   `man cmd`: displays manual pages about `cmd`
*   `mkdir dir`: creates a directory
*   `more`: displays the contents of a file
*   `mv`: moves or renames a file
*   `nano filename`: launches a baskic text editor to edit filename
*   `pwd`: tells you which directory youre in
*   `rm filename`: removes a file
*   `rmdir dirname`: removes a directory
*   `sort`: sort content of files
*   `tail`: displays the last lines of a file

## MATLAB GPU Tutorial

Run a MATLAB script that performs a regression test comparing the computation time of a non-GPU-based computation with that of a GPU-based computation.

### MATLAB Script (`gpu-bench.m`)

```matlab
% gpu-bench.m
for i = 300 : 100 : 700
    fprintf(' i = %d\n ', i);

    % Generates a random matrix X of size 1000i by 800 and a vector Y of size 1000i by 1
    X = random('unif', 0, 1, 1000*i, 800);
    Beta = [1:801]';
    allones = ones(1000*i, 1);

    % Add a constant term
    X = [allones, X];
    Y = X * Beta + random('norm', 0, 1, 1000*i, 1);

    % Non-GPU computation
    disp(' Time for non-GPU: ');
    tic;
    Bestimate = inv(X' * X) * (X' * Y);
    Bestimate = inv(X' * X) * (X' * Y);
    Bestimate = inv(X' * X) * (X' * Y);
    Bestimate = inv(X' * X) * (X' * Y);
    toc;

    % Now do it on the GPU
    % Copy the data to the GPU and create gX and gY in the GPU
    disp(' Load time for GPU: ');
    tic;
    gX = gpuArray(X);
    gY = gpuArray(Y);
    gBestimate = gpuArray(zeros(801, 1));
    toc;

    % GPU computation
    disp(' Time for GPU compute: ');
    tic;
    gBestimate = inv(gX' * gX) * (gX' * gY);
    gBestimate = inv(gX' * gX) * (gX' * gY);
    gBestimate = inv(gX' * gX) * (gX' * gY);
    gBestimate = inv(gX' * gX) * (gX' * gY);
    toc;

    % Copy estimates back
    disp(' Copy estimates back: ');
    tic;
    Bestimate = gather(gBestimate);
    toc;
end
```

The script generates a random matrix `X` of size 1000i by 800 and a vector `Y` of size 1000i by 1. It then adds a column of ones to `X` to account for the intercept term in the regression model. Next, it computes the regression coefficients (`Bestimate`) using the ordinary least squares (OLS) method for the non-GPU-based computation, and it computes the regression coefficients (`gBestimate`) using the OLS method on the GPU.

### Slurm Script (`gpu-bench.sbatch`)

```bash
#!/bin/bash
#
# [ gpu-bench.sbatch ]
#SBATCH --job-name=gpu-bench
#SBATCH --output=gpu-bench.%j.out
#SBATCH --export=ALL
#SBATCH --gpu-bind=closest
#SBATCH --time=00:9:00
#SBATCH --mem=32G
#SBATCH --mail-type=END,FAIL
#SBATCH --partition=gpu
#
# `--partition=gpu` specifies that we want to run it on the GPU node
#
# This script runs a MATLAB program saving the output into a files called:
# gpu-bench_#.out, where the # represents the jobID. See below.
#
#
# You SUBMIT this 'gpu-bench.sbatch' script to the grid with the sbatch command:
#
#
# sbatch gpu-bench.sbatch
#
# Specify the software and version to use, and run the MATLAB program:
echo "Running on node: `hostname`"
echo ""
module purge
module load matlab/2019a
matlab -nojvm < gpu-bench.m
```

You can run the following command to execute the script:

```bash
sbatch gpu-bench.sbatch
```

## Python Array Job Tutorial

Run `getSlurmExamples` at the command line of `rnd` or `vleda` to have all the tutorials copied to your home directory. This tutorial will teach you how to pass multiple parameters to Slurm. The Python script, `realVol.py`, calculates the real volatility for 5 different price series, with each price series saved as a file named `series<#>.txt`.

### Python Script (`realVol.py`)

```python
#------------------------------------
# realVol.py
# Calculate Real Volitility
#------------------------------------
import sys
import math

def main():
    sumsq = 0
    n = 0
    # read first price in file
    price_previous = sys.stdin.readline()
    # read each subsequent price in file
    for price_current in sys.stdin:
        # calculate the daily return
        daily_return = math.log(float(price_current) / float(price_previous))
        # compute the sum of squares
        sumsq = sumsq + daily_return ** 2
        price_previous = price_current
        n = n + 1
    # compute and output realized volatility
    real_vol = 100 * math.sqrt((252.0 / n) * sumsq)
    print("realized volatility = %.2f" % (real_vol))

if __name__ == '__main__':
    main()
```

### Slurm Script (`realVol.sbatch`)

```bash
#!/bin/bash
##------------------------------------
# realVol.sbatch
# Slurm job script
#------------------------------------
#SBATCH --job-name=realVol                 # set the name of the job
#SBATCH --array=1-5                        # create an array job with task IDs ranging from 1 to 5
#SBATCH --export=ALL                       # export env variables to the compute nodes
#SBATCH --mem=512m                         # set the amount of memory required for each task to 512 megabytes
#SBATCH --mail-type=BEGIN,END,FAIL        # send email notifications when the job starts, ends or fails
#SBATCH --output=realVol.%A-%a.out       # set the output file name for each task. The %A is replaced by the job ID and %a is replaced by the task ID.
#SBATCH --partition=test                   # specify the partition to run the job in. In this case, it is "test".
#SBATCH --time=00:10:00                   # set the maximum time limit for each task to 10 minutes. If a task exceeds this time limit, it will be terminated.

# The --array directive in Slurm allows a single job script to be executed multiple times, each with a different input parameter.
# When a job is submitted with --array, Slurm automatically creates an array of tasks, with each task corresponding to a specific value or range of values for the input parameter.
# The tasks can be executed in parallel on different nodes, and each task can be identified using its task ID, which is automatically assigned by Slurm.
# This feature is particularly useful when running a large number of similar tasks, such as parameter sweeps or simulations with different initial conditions.
# For our use case, we are using it to pass in files dynamically.

echo python realVol.py < `bash -c "unset noglob; ls series${SLURM_ARRAY_TASK_ID}*.txt"`
python realVol.py < `bash -c "unset noglob; ls series${SLURM_ARRAY_TASK_ID}*.txt"`
```

You can run the Slurm script by typing in the following command:

```bash
sbatch realVol.sbatch
```

## Python Simple Job Tutorial

### Introduction

This tutorial is intended to familiarize you with the process of running and scheduling jobs on the SCRC Slurm cluster. You will use the Simple Python Job to run a basic Python script that outputs the text `Hello World!`. Make sure you are logged in to a Linux terminal with SSH. Instructions can be found at Accessing the SCRC Systems.

### Writing Python Code

Using a text editing program such as `nano`, `vim`, `code`, or `emacs`, create a python script `hello-world.py`.

```python
'''
hello-world.py
Print string "Hello World!" to output
'''
# --------------------------------
# main
# --------------------------------
def main():
    print("Hello World!")

if __name__ == '__main__':
    main()
```

### Creating the Slurm Script

To run a Python script use a Slurm `sbatch` file to allocate the necessary compute resources. It contains directives for Slurm to interpret as well as programs for it to execute. Here is an example `sbatch` file, `hello-world.sbatch`, that submits the python job to the Slurm cluster.

```bash
#!/bin/bash
#
# [hello-world.sbatch]
#
#SBATCH --job-name=hello            # Job name
#SBATCH --output=hello.out          # Output file name
#SBATCH --export=ALL               # Export all environment variables
#SBATCH --time=00:01:00             # Set max runtime of job = 1 minute
#SBATCH --mem=4G                    # Request 4 gigabytes of memory
#SBATCH --mail-type=BEGIN,END,FAIL    # Send email notifications
#SBATCH --mail-user=you@stern.nyu.edu # email TO
#SBATCH --partition=test            # Specify the partition to submit the job to

module purge                         # Start with a clean environment
module load python/3.9.7           # Load python module
python hello-world.py               # Run the script using the loaded Python module
```

Lines beginning with `#SBATCH` are Slurm directives that specify job options, resource requests, and scheduling parameters for a job submitted to a Slurm cluster.

The `module` command is used to manage environment modules, which allow users to easily load and unload software and environment settings on systems such as HPC clusters. The `purge` subcommand clears all loaded modules, while the `load` subcommand loads a specific module.

The `python hello-world.py` command executes the Python script named `hello-world.py` using the Python interpreter. The script is run with the version of Python that was loaded via the environment module.

### Executing the Slurm Script

Submit the job with the command:

```bash
sbatch hello-world.sbatch
```

The job is now queued and as soon as the requested resources are available, Slurm schedules the job onto one of the Slurm compute nodes. If the requested resources cannot be met, the job waits in the queue.

To check the status of your submitted jobs:

```bash
squeue -u $USER
```

To check all jobs in the queue and running on the cluster:

```bash
squeue
```

## R Fitspline Tutorial

In this tutorial, you will run an R script. This script generates simulated data points with random noise, fits a cubic smoothing spline to the data, and plots the data points, original model, and smoothing spline.

### R Script (`fitspline.R`)

```R
# fitspline.R

# Set the initial seed for the random number generator.
set.seed(sample(1:1000, 1))

# Create n = 100 random data points.
# x is n equally spaced values from 0 to 1.
n <- 100
x <- (1:n) / n

# The model in this simulation (no random error)
mval <- ((exp(x / 3) - 2 * exp(-7 * x) + sin(9 * x)) + 1) / 3

# Generate n independent normal random variates with mean 0
# and variance derived from the task id
tid <- as.integer(Sys.getenv("SLURM_ARRAY_TASK_ID"))
v <- tid / 100
noise <- rnorm(n, 0, v)

# Simulated observed values (model value + noise)
y <- mval + noise

# Alternatively, you can read data from a file:
# dat <- read.table("dataset.dat", header = TRUE)
# attach(dat)

# Fit a cubic smoothing spline to the data
# Use GCV score and all basis functions
fit <- smooth.spline(x, y, cv = FALSE, all.knots = TRUE)

# Create a graph that shows the data, the smoothing spline,
# and the original model
r <- paste("result_", tid, ".ps", sep = "")
postscript(r, height = 8, width = 10, horizo = FALSE)

# Plot data points
plot(x, y, xlab = "x", ylab = "y", cex = 0.5)

# Plot original model values without noise
lines(x, mval, lty = 2)

# Plot smooth spline fit
lines(fit$x, fit$y)

# Save the graph to a PS file
graphics.off()

# To view with Ghostscript, at the
# command line type: gs result_X.ps
# where X is the corresponding task id
```

### Slurm Script (`fitspline.sbatch`)

```bash
#!/bin/bash
#
# [ fitspline.sbatch ]
#
# This script demonstrates how to run an R job, specifically,
# how to fit a smooth spline model. It uses a range of SLURM_ARRAY_TASK_ID's
# as a noise parameter for the model.
# --------------------------------------------------------------------
#
#
# Use environment modules to specify software and version. Run the
# "module av" command to get list of installed software versions,
# then replace the <X.Y.Z> with actual software version as shown below.
#
# module purge
# module load R/<X.Y.Z>
#
# For example:
#
# rnd> module avail R
# ---------------- /gridapps/modules -----------------
#   R/4.0.2   R/4.3.2
#
# rnd>
# rnd> module purge
# rnd> module load R/4.3.2
# rnd>
# --------------------------------------------------------------------
# Submit this job via 'sbatch' which accepts these command line options:
#SBATCH --job-name=fitsplineJob        # Define the name of the current job.
#SBATCH --output=fitsplineJob.Rout     # Define the stdout (the terminal output)
# file name.
#SBATCH --error=fitsplineJob.err      # Define the stderr (the terminal error output)
# file name. If '--error=' is not specified,
# both stdout and stderr are output to the
# same output file (in this case to file:
# fitspline.out).
#SBATCH --export=ALL                  # Export ALL environment variables of the
# submitting process to the submitted job
# including the current working directory.
#SBATCH --mail-type=END,FAIL           # Tell Slurm's sbatch to send email when the
# job ENDs or when the job FAILs. Options
# that may be specified with '--mail=' are
# NONE or any combination of:
# BEGIN,END,FAIL,REQUEUE,STAGE_OUT. There
# is no default for '--mail-type='.
#SBATCH --mail-user=your-stern-netid@stern.nyu.edu  # Specify your Stern email address to notify.
#SBATCH --mem=512m                    # Specifies the maximum memory this program will
# be allocated. The 512M specifies 512
# Megabytes. Memory units may be: k|m|g|t
# for kilo/mega/giga/tera-bytes. The default
# units are Megabytes.
#SBATCH --time=00:10:00               # The wall-clock time limit for this job, here 10 min.
#SBATCH --partition=test               # Specify to which partition to submit the job.
# A partition is group of compute servers
# which may potentially run this job.
# The 'test' partition is the default partition.
# The maximum time you
# may request for the 'test' partition is
# 100-hours (--time=100:00:00).
# --------------------------------------------------------------------
# How to submit an array job to Stern Slurm cluster.
# Pass array variable values 5, 10, 15 to the R script.
#
# sbatch --array=5-15:5 fitspline.sbatch
# --------------------------------------------------------------------

# Select stat package and version to use
module purge
module load R/4.3.2

R CMD BATCH --no-save --no-restore fitspline.R fitspline.$SLURM_ARRAY_TASK_ID.Rout
```

To run the SLURM script, execute this command:

```bash
sbatch --array=5-15:5 fitspline.sbatch
```

## R Monte Carlo Simulation Tutorial

In this tutorial, we will run an R script. The R script runs a Monte Carlo simulation to estimate the path of a stock price using the Geometric Brownian stochastic process.

### R Script (`stock-price.R`)

```R
# [stock-price.R]
GeometricBrownian <-function() {
    paths <- 10
    count <- 5000
    interval <- 5 / count
    mean <- 0.06
    sigma <- 0.3
    sample <- matrix(0, nrow = (count + 1), ncol = paths)
    for (i in 1:paths) {
        sample[1,i] <- 100
        for (j in 2:(count + 1)) {
            #Expression for Geometric Brownian Motion
            sample[j,i] <- sample[j - 1,i] * exp(interval * (mean - ((sigma) ^ 2) / 2) + ((interval) ^ .5) * rnorm(1) * sigma)
        }
    }
    cat("E[W(2)] = ", mean(sample[2001,]), "\n")
    cat("E[W(5)] = ", mean(sample[5001,]), "\n")
    #pdf <- paste("result_", tid, ".pdf", sep = "")
    #pdf(file="out.pdf")
    hist(sample)
    matplot(sample, main = "Geometric Brownian", xlab = "Time", ylab = "Path", type = "l")
    dev.off()
}

GeometricBrownian()
```

### SLURM Script (`stock-price.sbatch`)

```bash
#!/bin/bash
#
# [ stock-price.sbatch ]
#
# This slurm submission script runs a Monte Carlo simulation to
# estimate the path of a stock price using the geometric
# Brownian motion stochastic process.
#
# -----------------------------------------------------------------------------
#
# slurm job scheduler directives begin with "#SBATCH"
#
#SBATCH --job-name=spJob                # Job name
#SBATCH --time=00:10:00               # Wall-clock time limit for this job
#SBATCH --mem=4G                      # Request 4G RAM
#SBATCH --mail-type=END,FAIL           # email user when job ENDs or FAILs
#SBATCH --mail-user=you@stern.nyu.edu  # email TO
#SBATCH --output=helloJob%j.out        # write output; "%j" = job ID
#SBATCH --partition=test                # test partition max time 1hr
#
#
# **** Note: It is always advantages to specify conservative values
# for run time and memory. Jobs requesting fewer resources are more
# likely to be scheduled before jobs requesting more resources.
#
# --------------------
# How to submit job to Stern grid
#
# sbatch --array=5-15:5 fitspline.embedded-sbatch.sh
# --------------------------------------------------------------------
# Select stat package and version to use
module purge
module load R/4.0.2
#R CMD BATCH --slave fitspline.R fitspline.$SLURM_JOBID.Rout
#R CMD BATCH --slave fitspline.R fitspline.$SLURM_TASK_PID.Rout
R CMD BATCH stock-price.R
```

To execute this script, run the following command:

```bash
sbatch stock-price.sbatch
```

## Run Anaconda/Jupyter Environment on SLURM

In this tutorial, you will run an interactive Anaconda Jupyter notebook environment within on SLURM. Make sure you have opened a FastX terminal and are logged in to the `fx1` node. To run interactive jobs, we have use the `srun` command to log in to an interactive job node. You can see what nodes are available using `sinfo`.

To request a GPU, add the Slurm directive `--partition=gpu` parameter in `srun`.

```bash
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
```

Where:

*   `srun`: Command to submit a job to the Slurm scheduler.
*   `--pty`: Allocate a pseudo-terminal for interactive job execution.
*   `--mem=8gb`: Request 8 gigabytes of memory for the job.
*   `--time=1:00:00`: Set a time limit of 1 hour for the jobs execution.
*   `--cpus-per-task=1`: Request 1 CPU core per task.
*   `--nodes=1`: Request 1 compute node for the job.
*   `/bin/bash`: Execute the Bash shell as the jobs command.

You will see that you are logged in to one of the interactive nodes. Check what modules are installed:

```bash
module av
# OR
module avail
```

To load the Anaconda environment, type in the following command:

```bash
module load anaconda3/py3.9
```

Now run the following command to load the Jupyter Notebook:

```bash
jupyter-notebook
```

You will see a Jupyter notebook open up in Chromium Browser. Navigate to your Jupyter notebook that you created previously or create a new one using the New button and then clicking on Python 3 (ipykernel). Once inside the Jupyter notebook, type Python code in the cells and click the Run button to execute the code.
```


```markdown
# Knowledge Base

This document consolidates information from various tutorials and guides.

## Run RStudio on SLURM

This tutorial explains how to run an interactive RStudio session and execute R code on SLURM.

**Prerequisites:**

*   A FastX session logged in to one of the `fx` nodes. See [Getting Started with Slurm Interactive Jobs](link-to-getting-started).

**Procedure:**

1.  Run an interactive job using the `srun` command:

    ```bash
    srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
    ```

    *   `srun`: Command to submit a job to the Slurm scheduler.
    *   `--pty`: Allocate a pseudo-terminal for interactive job execution.
    *   `--mem=8gb`: Request 8 gigabytes of memory for the job.
    *   `--time=1:00:00`: Set a time limit of 1 hour for the job's execution.
    *   `--cpus-per-task=1`: Request 1 CPU core per task.
    *   `--nodes=1`: Request 1 compute node for the job.
    *   `/bin/bash`: Execute the Bash shell as the job's command.

2.  After the command executes, you'll be logged into an interactive node.

3.  Check available modules:

    ```bash
    module av
    # OR
    module avail
    ```

4.  Load the RStudio module:

    ```bash
    module load rstudio
    ```

5.  Run RStudio:

    ```bash
    rstudio
    ```

    RStudio will open in a new window. Open an R script using the directory navigation window (bottom right). To run the R script, click the green "Run" icon. The output will be displayed in the Console below.

## Run XStata on SLURM

This tutorial explains how to run XStata on SLURM.

**Prerequisites:**

*   A FastX session logged in to one of the `fx` nodes. See [Getting Started with Slurm Interactive Jobs](link-to-getting-started).

**Procedure:**

1.  Run an interactive job using the `srun` command:

    ```bash
    srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
    ```

    *   `srun`: Command to submit a job to the Slurm scheduler.
    *   `--pty`: Allocate a pseudo-terminal for interactive job execution.
    *   `--mem=8gb`: Request 8 gigabytes of memory for the job.
    *   `--time=1:00:00`: Set a time limit of 1 hour for the job's execution.
    *   `--cpus-per-task=1`: Request 1 CPU core per task.
    *   `--nodes=1`: Request 1 compute node for the job.
    *   `/bin/bash`: Execute the Bash shell as the job's command.

2.  After the command executes, you'll be logged into an interactive node.

3.  Check available modules:

    ```bash
    module av
    # OR
    module avail
    ```

4.  Load the XStata module:

    ```bash
    module load xstata-se/17.0
    ```

5.  Run XStata:

    ```bash
    xstata
    ```

**Running Stata code:**

You can type code in the command line at the bottom of the window and press Enter to execute. For larger programs, create a `.do` script and import it into XStata.

## SAS Tutorial

This tutorial provides a SAS script example.

**Note:** Run `getSlurmExamples` at the command line of `rnd` or `vleda` to have all tutorials copied to your home directory.

**Example SAS Script (`crosstab.sas`):**

```sas
/* crosstab.sas */
DATA Hand;
INPUT gender $ handed $ ;
DATALINES;
Female Right
Male Left
Male Right
Female Right
Female Right
Male Right
Male Left
Male Right
Female Right
Female Left
Male Right
Female Right
PROC FREQ DATA=Hand;
TABLES gender*handed;
RUN;
```

**Example SLURM Script (`crosstab.sbatch`):**

```bash
#!/bin/bash
# [ crosstab.sbatch ]
#SBATCH --job-name=crosstab
#SBATCH --output=crosstab.out
#SBATCH --export=ALL
#SBATCH --time=00:10:00
#SBATCH --mem=512m
# This script demonstrates how to run a SAS program on the Stern grid.
# The SAS program creates a cross tabulation between gender and
# left- and right-handedness. It creates TWO files:
#
# crosstab.log
# the execution log
#
#
# and crosstab.lst
# a table of gender handedness
# ---------------------------------------------------------------------
# You may submit this 'crosstab.sh' script for:
# IMMEDIATE execution, to the grid using the 'srun' command, or
# LATER execution, to the grid using the 'sbatch' command.
#
#
# Example submissions:
# --------------------
# Submit crosstab.sh via sbatch to the grid for LATER execution with command:
# sbatch crosstab.sbatch
#
#
# Specify the software and version to use, and run the sas program:
module purge
module load sas/ 9.4
sas -nodms crosstab.sas
```

**Running the script:**

```bash
sbatch crosstab.sbatch
```

## Transferring Files from Local to Remote Linux Server

This guide explains how to transfer files between your local computer and a remote Linux server.

**Using FileZilla (Windows, Linux, and Mac):**

1.  Download, install, and start [FileZilla](https://filezilla-project.org/).

2.  If off-campus, first log in to the NYU VPN.

3.  Enter the following connection details:

    *   Host: `rnd.scrc.nyu.edu`
    *   Username: `<your Stern ID>`
    *   Password: `<your password>`
    *   Port: `22`

4.  Click "Quickconnect."

5.  On the left side of FileZilla, you should see your local computer. On the right side, you should see your Linux home directory.

6.  Drag and drop files to transfer between your local computer and the Linux server.
```