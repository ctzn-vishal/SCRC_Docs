```markdown
# NYU Stern Center for Research Computing Documentation

This documentation provides information about the NYU Stern Center for Research Computing (SCRC), its services, and how to get started.

## About

The NYU Stern Center for Research Computing is committed to supporting and advancing the research endeavors of the NYU Stern community. Through their comprehensive services, they enable researchers to leverage computational resources effectively, accelerate discoveries, and drive innovation in their respective fields.

## Services

The SCRC offers a range of services to support research computing needs:

*   **High-Performance Computing (HPC):** Access to a moderately sized HPC cluster for complex simulations, data analysis, and modeling. See [Compute Services](#compute).
*   **Data Acquisition, Storage, and Management:** Robust data storage solutions including high-capacity shared file systems, network-attached storage (NAS), and backups. See [Storage](#storage).
*   **Datasets and Services:** Access to a wide variety of datasets and syndicated data services. See [Research Datasets](#research-datasets).
*   **Software and Application Support:** A range of software packages and tools, along with assistance in selecting and optimizing software. Training is also provided. See [Research Software](#research-software).
*   **Cloud Computing:** Access to cloud resources for on-demand computing power and storage. See [Cloud Computing](#cloud-computing).
*   **Research Computing Consultation:** Personalized support services to help researchers identify the best computational approaches and resources for their projects, optimize code, and troubleshoot technical issues. Assistance with finding qualified student assistants is also available. See [FAQ](#faq).

### Hardware Specifications

#### Cloud Servers

Cloud servers are available for GPU processing and computation:

*   **tiffany:** 766GB RAM, 96 CPU x 2.1 GHz Intel Xeon Platinum 8160 @ 2.1 GHz
*   **einstein:** 1.5TB RAM, 96 CPU x 2.1 GHz Intel Xeon Platinum 8160 @ 2.1 GHz
*   **hawking:** 768GB RAM, 56 CPU x 2.59 GHz Intel Xeon Gold 6132 @ 2.59 GHz
*   **nobel:** 384GB RAM, 64 CPU x 2.59 GHz Intel Xeon GPU E5-2697A v4 @ 2.59 GHz

#### Other Hardware

*   **Switches:** NetGear 10GB switches for high-speed intra- and inter-communication.
*   **Storage:** NAS and SAN Storage devices totaling over 120TB of storage.

### Our Team

*   **Razi Ahmad:** Associate CIO, Security, Infrastructure, and Research Computing - <razi@stern.nyu.edu>
*   **Vishal Singh:** Faculty Director - <vsingh@stern.nyu.edu>
*   **Robin Wurl:** Manager of Research Computing - <rw74@stern.nyu.edu> | (212) 998-0814
*   **David Frederick:** Manager of Research Databases and Windows Applications - <research@stern.nyu.edu> | (212) 998-0163

## Compute

The SCRC Slurm cluster is a collection of moderate-sized compute nodes that supports a wide range of computational tasks such as data analysis, simulations, and modeling. The Slurm workload manager provides a flexible way to manage job scheduling and resource allocation. Researchers can run programs on the SCRC Slurm cluster interactively or in batch mode.

*   [Slurm Batch Jobs](#slurm-batch-jobs)
    *   [Python Simple Job Tutorial](#python-simple-job-tutorial)
    *   [Python Array Job Tutorial](#python-array-job-tutorial)
    *   [SAS Tutorial](#sas-tutorial)
    *   [MATLAB GPU Tutorial](#matlab-gpu-tutorial)
    *   [Common SLURM commands](#common-slurm-commands)
    *   [R Fitspline Tutorial](#r-fitspline-tutorial)
    *   [R Monte Carlo Simulation Tutorial](#r-monte-carlo-simulation-tutorial)
    *   [Python Virtual Environment](#python-virtual-environment)
*   [Slurm Interactive Jobs](#slurm-interactive-jobs)
    *   [Getting Started with Slurm Interactive Jobs](#getting-started-with-slurm-interactive-jobs)
    *   [Common SLURM commands](#common-slurm-commands)
    *   [Run Anaconda/Jupyter Environment on SLURM](#run-anacondajupyter-environment-on-slurm)
    *   [Install Local R Packages](#install-local-r-packages)
    *   [Python Virtual Environment](#python-virtual-environment)
    *   [Run XStata on SLURM](#run-xstata-on-slurm)
    *   [Run RStudio on SLURM](#run-rstudio-on-slurm)
*   [Cloud Computing](#cloud-computing)
    *   [Getting started with Cloud Computing](#getting-started-with-cloud-computing)

## Contact Us

Contact one of us directly or send questions to our groups email at <scrc-list@stern.nyu.edu>.

SCRC also offers help through personal consultations such as:

*   Finding the right software, datasets, or computational services that best fit your research needs.
*   Using or understanding our compute services such as batch or interactive processing.
*   Purchasing, transferring, or storing data.
*   Getting and using a virtual machine for specialized computational or secure data requirements.

For general non-research support questions contact the [Stern IT helpdesk](link-to-helpdesk).

## FAQ

### Frequently Asked Questions (FAQ)

On this page, you will find a list of frequent questions that users of our computing services may have. If there's a question you have that isn't answered here, you can always check out the [Support](#contact-us) page to get personalized support.

**How do I request a dedicated virtual machine?**

SCRC has a small VMWARE cloud that we use to support researchers with specialized needs. The cloud supports a wide variety of both Windows and Linux machines. If you send an email to <scrc-list@stern.nyu.edu> with a description of your needs, we can schedule a meeting and usually provide a machine in a day or so. We currently support Windows and Linux virtual machines. Typically, a machine is 6 cores and 32GB of RAM. You can learn more on our [Cloud Computing](#cloud-computing) page.

**Who signs contracts for purchasing data?**

All data purchases at Stern should be handled by David Frederick (<research@stern.nyu.edu>). All purchases are charged to the SCRC and a transfer is made from the appropriate budget to cover the amount. This allows the budget office to see ALL of the data purchases at the school and allows us to make sure no one else already has purchased the data, or if there is a chance for bundling this purchase with an existing license. Also, the contract often needs to be reviewed by NYU legal, as well as risk management and purchasing.

**Should I use SCRC or NYU HPC?**

As a starting point, we recommend using the Stern HPC facilities, especially if you are new to high-performance computing (HPC) or have relatively modest computational requirements. Our team is available to provide personalized assistance to help you get started. In terms of processing time, the Stern HPC typically offers a faster response compared to the NYU HPC, although this may fluctuate. The NYU HPC facility serves the entire university and boasts extensive capabilities, including a wider range of software options compared to the Stern HPC. In fact, the NYU HPC is recognized as one of the most powerful academic HPC clusters. Our knowledgeable staff can guide you in determining the most suitable facility for your computational needs. If you would like to use Hadoop or Big Data services, we recommend using HPC as they have a Peel cluster for specific big data needs.

**How do I get started with SCRC?**

To get started with the SCRC (Stern Center for Research Computing) services, you can follow these steps:

*   As a Stern user, you can access the SCRC facilities using your Stern NetID and password. If you haven't already activated your Stern account, you'll need to do so by visiting the following website: <http://start.stern.nyu.edu>
*   Once your account is activated, you can log in via SSH to either `rnd.stern.nyu.edu` or `vleda.stern.nyu.edu` using your Stern netid and password.
*   Upon your first login, your home directory will be automatically created for you.
*   You are now able to use the SCRC facilities, which include both interactive and grid computing services.

Please be aware that these services operate on Linux, so it is expected that you have some familiarity with Linux or Unix. If you are collaborating with someone from another institution, your departmental coordinator can assist them in obtaining an NYU netid and a sternid for access to SCRC services. More detailed instructions can be found on the [Get Started](#get-started) page.

**I have a large dataset, where should I put it?**

For optimal storage and management of your large datasets, we have a designated space called `bighome` in your home directory. Each user can request a `bighome` by emailing us at <scrc-list@stern.nyu.edu>. This directory is specifically designed to house all your substantial files, such as extensive data sets. It provides a centralized location for efficient organization and easy access to your data. To ensure the safety of your data, we perform weekly backups of your `bighome`, offering an added layer of protection. While there is no predefined quota limit for your `bighome`, please inform us if you require more than 1TB of storage. We are here to support your data needs and will gladly accommodate any additional requirements you may have.

**How do I request consulting help?**

Contact one of us directly or send questions to our groups email at <scrc-list@stern.nyu.edu>. SCRC also offers help through personal consultations such as finding the right software, datasets, or computational services that best fit your research needs, using or understanding our compute services such as batch or interactive processing, purchasing, transferring, or storing data, getting and using a virtual machine for specialized computational or secure data requirements. For general non-research support questions contact the Stern IT helpdesk.

**What services are available through the NYU Library?**

NYU library has access to a vast collection of resources, research materials, and digital databases for students, faculty, and researchers. You can get more information on the [NYU Library](link-to-nyu-library) and [NYU Business Library Data Services](link-to-nyu-business-library-data-services) pages.

**How do I get a WRDS account?**

Wharton Research Database Services is an internet based research business data service from the Wharton School. WRDS data consists of historical financial information for banks, government bonds, stock exchanges, and major companies. It is intended solely for research and instructional purposes. For detailed information, visit our [WRDS page](link-to-wrds-page).

The following steps will guide you in obtaining your WRDS account:

1.  Visit Wharton Research Database Services with your Web browser.
2.  Click on the Register button at the top of the login page.
3.  Complete the form, read the WRDS Terms of Use Statement, and submit.
4.  The NYU Representative for WRDS will receive a message from WRDS regarding your account application.
5.  The NYU Representative will check your NYU affiliation.
6.  Once your account request is approved, WRDS will send you an e-mail with instructions for setting your password.

If you have suggestions, comments, questions or problems using this service, please contact: <research@stern.nyu.edu>. If you have problems, questions, or suggestions concerning WRDS database access or data querying, or programming on the WRDS server, go to [WRDS Support](link-to-wrds-support).

**What is Apps@Stern?**

Apps@Stern provides NYU Stern's students and faculty with virtual access to academically relevant software applications. You can access Apps@Stern by navigating to their website [here](link-to-apps-at-stern). To access additional applications NYU offers, please navigate to the [NYU Virtual Computer Lab (VCL)](link-to-nyu-vcl). Use of Apps@Stern and the Virtual Computer Lab (VCL) are for academic purposes only. For more information, please see the [Apps@Stern service documentation](link-to-apps-at-stern-documentation). If you need help, contact the Stern helpdesk: <helpdesk@stern.nyu.edu> | (212) 998-0180 | Tisch L-100

**How do I learn Linux?**

We have a simple Linux tutorial to get you started with SCRC services: [Linux Tutorial](#linux-tutorial) For an in-depth tutorial, you can navigate to this Linux guide: [Learning the Shell](link-to-learning-the-shell).

## Get Started

### Getting an Account

#### Stern users

For those in the Stern School of Business, you can use your existing activated Stern account, i.e., Stern NetID and password, to access SCRC services and resources. If you haven't already, [activate your Stern account](link-to-stern-account-activation).

#### Non-Stern NYU users

Those already at NYU but not in Stern (and not enrolled in a Stern course) must have a full-time Stern employee make a request on their behalf by contacting the Stern IT Help Desk at <helpdesk@stern.nyu.edu> or 212-998-0180 and provide the following information:

*   Full Name
*   NYU NetID
*   NYU UniversityID (N#)
*   Date of birth
*   Sponsor's name (Stern faculty or employee)
*   Sponsoring department
*   Expiration date (max 1 year; extensions may be requested yearly)

[Activate your Stern account](link-to-stern-account-activation) to use SCRC services.

#### Non-NYU users

Non-NYU affiliated users must first obtain an NYU account by having an authorized sponsor request an NYU NetID on their behalf by filling out the [IT Onboarding Form](link-to-it-onboarding-form). It is accessed by logging into the [NYU VPN](link-to-nyu-vpn), then logging into [identity.it.nyu.edu](link-to-nyu-identity-management), clicking the hamburger menu, selecting Request Affiliate, and then Request Affiliate User. For additional help contact NYU IT support at <AskIT@nyu.edu> or 212-998-3333.

### Accessing the SCRC Systems

#### Log in to a Terminal Command Line Interface

The most common way to access the SCRC servers is to use a Command Line Interface (CLI) from a terminal application. A CLI is a text-based interface that allows users to interact with a host by entering text commands at the prompt of a terminal application. The SCRC hosts that you connect to are running Linux. You will use your Stern NetID and password to authenticate to either one of SCRC's remote login hosts: `rnd.scrc.nyu.edu` or `vleda.scrc.nyu.edu`.

#### If Off Campus, First Connect to the NYU VPN

If you are connecting from a remote location that is not on the NYU network (your home for example), you need to set up your computer to use the [NYU VPN](link-to-nyu-vpn). Once you've created a VPN connection, you can proceed as if you were connected to the NYU network. If you're on the NYU network already, you can proceed directly with your connection.

#### Log in From Mac/Linux

Open the terminal application and use the `ssh` command to make a secure connection to one of SCRC's remote login hosts. E.g., if your Stern NetID is `xy12`,

```bash
ssh xy12@rnd.scrc.nyu.edu
```

OR

```bash
ssh xy12@vleda.scrc.nyu.edu
```

#### Log in From Windows

Windows users have several options:

*   **Command Line:** Open the `cmd` program on an updated Windows 10 or later machine. Type the `ssh` command the same as shown above for Mac/Linux.
*   **WSL2:** If you run Windows 10 or later, you can install [Windows Subsystem for Linux (WSL)](link-to-wsl), and then install Ubuntu or other Linux distributions on your machine. You will get a fully functional Ubuntu distribution with a terminal application. Type the `ssh` command the same as shown above for Mac/Linux.
*   **PuTTY:** PuTTY is a free and open-source terminal emulator and network file transfer application that supports logging in with the `ssh` command.
    *   Note: If you are using WSL2, you may not be able to access the internet when Cisco AnyConnect VPN, installed from the `.exe` file, is activated. A potential solution is to uninstall Cisco AnyConnect and install AnyConnect using Microsoft Store and then set up a new VPN connection using the settings described onthe [IT webpage](link-to-it-webpage).

##### Getting and using PuTTy

PuTTY is free and can be downloaded from [PuTTY Download](link-to-putty-download).

1.  Download and run the latest installer file from the website.
2.  Follow the on-screen install instructions.
3.  Once installed, start PuTTY, then type `rnd.stern.nyu.edu` or `vleda.stern.nyu.edu` in the Host Name field and click Open.

    Note: The first time you log in a dialog may appear which starts with "The server's host key is not cached." Click Yes in this dialog.
4.  Type your Stern NetID and password at the `login as` and `password` prompts, respectively.
5.  You should now be logged in and see a command line prompt from which you can enter Linux commands or run programs.

### Transferring files from local to remote Linux server

#### On Windows, Linux and Mac (using FileZilla)

1.  Download, install, and start [FileZilla](link-to-filezilla).
2.  If off-campus, first log in to the [NYU VPN](link-to-nyu-vpn).
3.  Enter the following for a new connection:
    *   Host: `rnd.scrc.nyu.edu`
    *   Username: `<your Stern ID>`
    *   Password: `<your password>`
    *   Port: `22`
4.  Click Quickconnect.
5.  On the left, you should see your local computer, while on the right, your Linux homedir.
6.  Drag-and-drop files to transfer between the local and the Linux server.

### Linux Tutorial

For an in-depth tutorial, you can navigate to this Linux guide: [Learning the Shell](link-to-learning-the-shell). This tutorial demonstrates the basic Linux commands a user would need to use and run programs on the SCRC Linux computers.

The Linux machines use a command line interface called a Shell. The Shell is the interface where you enter Linux commands. There are many types of shells. By default, SCRC Linux machines use the BASH shell. The first thing you see after logging in is the shell's command prompt. For example, Christine Thomas's prompt might look something like this:

```text
[ct27@rnd ~ ]$
```

#### Your Home Directory

Once logged in, you are deposited into your home directory. Every user has a home directory. Your home directory is where you will store most of your files.

#### Show the present working directory

To see the complete name and path of the current working directory, use the command

```bash
pwd
```

Example output:

```text
/homedir/employees/c/ct27
```

This prints the full directory path. Here, Christine's home directory name is `ct27` which is contained within a directory called `c` which is inside the directory `employees` inside the directory `homedir`. The Linux directory structure is a hierarchical tree structure.

#### Show contents of a directory

To see a list of the files and directories in the current directory type `ls -l` (list directory contents using long format), e.g.,

```bash
ls -l
```

Example output:

```text
total 180
drwxr-xr-x 3 ct27 nobody 4096 Apr  5 2023 mywork
drwxr-xr-x 3 ct27 nobody 4096 Apr  3 2023 archived-work
-rw-r--r-- 1 ct27 nobody    0 Mar 18 2023 prog.sas7bdat
-rw-r--r-- 1 ct27 nobody 1421 Mar 18 2023 prog.sas7bdat.log
```

`ls` is the command and `-l` is, in this example, the option for the command. The `-l` option formats the results into long format. Long format lists more than just the names of the files which is what `ls` alone would show. In this example, the output shows two directories `mywork` and `archived-work` (notice the `d` at the beginning of the line), and two files `prog.sas7bdat` and `prog.sas7bdat.log`. Some other information we see, e.g., the size of the log file is 1421 bytes, its owner is `ct27`, its last modification date is Apr 5 2023.

#### Auto Completion in the Shell

Press the `Tab` key after enough of the word you are trying to complete has been typed in. If when hitting tab the word is not completed there are probably multiple possibilities for the completion. Press tab again and it will list the possibilities.

#### Create a sub-directory

Say you would like to work on a project. It is probably convenient to create a sub-directory to hold the project's files, i.e., program, data and results. To create a directory use the `mkdir` (make directory) command, e.g.,

```bash
mkdir costProject
```

This command creates a new directory called `costProject` inside the current directory. Verify this by typing `ls -l`.

**Note**: Linux is case sensitive, so for example `costproject` is not the same as `costProject`.

#### Change to a subdirectory

To change into the `costProject` directory, i.e., make it the current directory, use the `cd` (change directory) command, e.g.,

```bash
cd costProject
```

Verify that we are in the `costProject` directory using `pwd`.

```bash
pwd
```

Example output:

```text
/homedir/employees/c/ct27/costProject
```

#### Create or edit a file

`nano` is a simple text editor used to create or edit a data or program file, etc. For example, to edit a file called `costdata.dat` type,

```bash
nano costdata.dat
```

[**NOTE**: Insert picture of nano editor here]

This picture shows the nano editor editing the file `costdata.dat`. Along the bottom of the nano editor are the editor's commands. The character `^` is the `ctrl` key. To save the file you type `ctrl-o` and then to exit `nano` type `ctrl-x`.

#### List the contents of a file

The `more` command displays the contents of a file, one screen-full at a time. Press the space bar to move forward screen by screen until the end of the file is reached or press the letter `q`, for quit., E.g.,

```bash
more costdata.dat
```

If the file contents are larger than can be shown in one page, the `more` command shows you the first page and halts. To see the next page press the space bar and to quit type `q`.

#### Breaking out

If you get stuck or hung after typing a command, etc., then use `ctrl-c` to break out or cancel your current command. `ctrl-c` returns you to the command prompt.

### Linux Tutorial Continued

Commands Most Linux commands are short, typically an abbreviation or mnemonic for what the command does. For example, the command to delete a file is `rm` which is short for remove. Recall: Linux is case-sensitive, i.e., it distinguishes between lowercase and uppercase (recognizing commands in lowercase only).

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

    **Note**: There is no undo in Linux therefore once a file has been deleted there is no easy way to recover it.
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

#### Redirecting Input and Output

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

#### Pipes

The output of one command can be fed as input into to another command. The symbol for the input/output (I/O) connection is a vertical bar `|` called a pipe. For example, a directory containing many files will scroll off the screen if just `ls` is used. If a pipe is used to direct the output of `ls` to be the input of `more`, then the directory listing will be shown one screen-full at a time and will not scroll off the screen.

```bash
ls | more
```

#### Online Help

To get on-line help in Linux, use the `man` command. It provides access to a comprehensive online Linux manual. Type `man` followed by a command or topic on which you want information:

```bash
man < command >
```

To make the online manual more helpful, an index is provided. The index is accessed with the `-k` option of the `man` command. For example:

```bash
man -k directory
```

will display a one-line synopsis of all manual pages having to do with directories.

#### The Linux File System

Linux uses a hierarchical file structure, which is made up of files, directories and sub-directories. A file can hold text, data, or a program. Directories contain files and sub-directories. A sub-directory is a directory that has been created within another directory.

You can also use the help to get a description of the commands usage. Simply type your command whose usage you to know in the terminal with `h` or `help` after a space and press enter. And you’ll get the complete usage of that command as shown below. An example below:

```bash
cat --help
```

#### Permissions

Since Linux is set up to let users share files, you have the option of allowing or denying access to others on the system. Permissions determine who may access your files and directories or what may be done with a file or a directory. Use `ls -l` to see what permissions your files and directories have.

Example output:

```text
-rw------- 1 ct27 devel Aug 20 10:15 logon
-rwx------ 1 ct27 devel Aug 19 15:23 a.out
-r-xr-xr-x 1 ct27 devel Aug 28 09:48 ls-list
drwx------ 1 ct27 resch Aug 27 15:45 sas-one/
drw------- 1 ct27 resch Aug 27 15:45 tex/
```

The characters `d`, `r`, `w`, `x`, and `-` at the far left indicate the permission of each file and directory. There are 10 positions.

*   Position 1 is the directory indicator.
*   Positions 2,3,4 apply to the owner (creator) in this case `ct27`.
*   Positions 5,6,7 apply to the group. Here, there are two different groups shown, `devel` and `resch`.
*   Positions 8, 9,10 apply to all users.

The meaning of the letters are:

*   **d (directory)** If the first letter is a `d`, the file is a directory. If the first character is a hyphen (`-`), then it is a regular file.
*   **r (readable)** A file must be readable to be looked at or copied. A directory must be readable for you to list its contents.
*   **w (writable)** A file must be writable in order for you to modify it, remove it, or rename it. A directory must be writable in order for you to add or delete files in it.
*   **x (executable)** A file with executable permissions is one you can run, such as a program or a shell script. A directory must be executable in order for you to move into it (using the `cd` command), list its contents, or create or delete files there.
*   The hyphen (`-`) appears when the pe
```

```markdown
# Linux Tutorial

## Changing File and Directory Permissions

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

For example to change the file called `my.dat` with the permissions:

```
-rw-r--r--
```

to read/write/execute for all users (owner, group, and other) type the command:

```bash
$ chmod a+rwx my.dat
```

The resultant permissions would be:

```
-rwxrwxrwx
```

Now, change the permissions of `my.dat` so that only the owner can read, modify or delete it, i.e.:

```bash
$ chmod u-x my.dat
$ chmod g-rwx my.dat
$ chmod o-rwx my.dat
```

The resulting permissions are:

```
-rw-------
```

## History

The most recent commands typed at the command line interface are saved and can be viewed or retrieved for re-use. Access the history by pressing the up arrow. To search for a command in the history type `ctrl-r`, type the search text, then press enter to re-execute or `ctrl-c` to abort

## Basic Cursor Movement, Cut, Paste and Undo

*   `ctrl-a`: move cursor to beginning of line
*   `ctrl-e`: move cursor to end of line
*   `ctrl-k`: cut everything after the cursor
*   `ctrl-y`: paste the last thing cut
*   `ctrl-_`: undo

## Command Summary

*   `cat`: display contents of a file
*   `cd dir`: moves you to directory called dir
*   `pwd`: display the current working directory
*   `chmod permissions`: sets permissions on a file
*   `clear`: clear screen
*   `cp`: copies a file
*   `diff file1 file2`: compare two files
*   `exit`: exit Linux shell
*   `file`: lists file type of given file
*   `find -name filename`: search for file called filename
*   `grep search-string`: search for files containing search-string
*   `cat file | grep searchstring`: search file for the text searchstring
*   `head`: displays top lines of a file
*   `history`: displays recently entered commands
*   `ls`: lists the contents of a directory
*   `ls -l`: like ls, but in long format
*   `man cmd`: displays manual pages about cmd
*   `mkdir dir`: creates a directory
*   `more`: displays the contents of a file
*   `mv`: moves or renames a file
*   `nano filename`: launches a basic text editor to edit filename
*   `pwd`: tells you which directory youre in
*   `rm filename`: removes a file
*   `rmdir dirname`: removes a directory
*   `sort`: sort content of files
*   `tail`: displays the last lines of a file

# Python Simple Job Tutorial

## Introduction

This tutorial is intended to familiarize you with the process of running and scheduling jobs on the SCRC Slurm cluster. You will use the Simple Python Job to run a basic Python script that outputs the text `Hello World!`.

Make sure you're logged in to a Linux terminal with SSH.

## Writing Python code

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
    print(" Hello World! ")

if __name__ == '__main__':
    main()
```

## Creating the Slurm Script

To run a Python script use a Slurm `sbatch` file to allocate the necessary compute resources. It contains directives for Slurm to interpret as well as programs for it to execute.

Here is an example `sbatch` file, `hello-world.sbatch`, that submits the python job to the Slurm cluster.

```bash
#!/bin/bash
#
# [hello-world.sbatch]
#
#SBATCH --job-name=hello        # Job name
#SBATCH --output=hello.out       # Output file name
#SBATCH --export=ALL             # Export all environment variables
#SBATCH --time=00:01:00          # Set max runtime of job = 1 minute
#SBATCH --mem=4G                 # Request 4 gigabytes of memory
#SBATCH --mail-type=BEGIN,END,FAIL  # Send email notifications
#SBATCH --mail-user=you@stern.nyu.edu # email TO
#SBATCH --partition=test          # Specify the partition to submit the job to

module purge                      # Start with a clean environment
module load python/3.9.7        # Load python module

python hello-world.py            # Run the script using the loaded Python module
```

Lines beginning with `#SBATCH` are Slurm directives that specify job options, resource requests, and scheduling parameters for a job submitted to a Slurm cluster.

The `module` command is used to manage environment modules, which allow users to easily load and unload software and environment settings on systems such as HPC clusters. The `purge` subcommand clears all loaded modules, while the `load` subcommand loads a specific module.

The `python hello-world.py` command executes the Python script named `hello-world.py` using the Python interpreter. The script is run with the version of Python that was loaded via the environment module.

## Executing the Slurm Script

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

# Research Datasets

The Stern Center for Research Computing provides access to a wide range of research datasets for academic and research purposes. These datasets cover a variety of topics such as finance, economics, business, and social sciences. The center offers access to both numerical databases and text-based databases.

Numerical databases include data on financial markets, company financials, regulatory filings, and more. Text-based databases include access to academic journals, news articles, and other sources of information.

The datasets are sourced from reputable providers such as Bloomberg, Capital IQ, Compustat, Dow Jones, I/B/E/S, JSTOR, Lexis-Nexis, S&P NetAdvantage, and more. Researchers can access these datasets through various means such as APIs, web-based platforms, and downloadable files. Access to these datasets requires a Stern NetID.

*   [Bank Regulatory (formerly FDIC)](#bank-regulatory-formerly-fdic)
*   [Bloomberg](#bloomberg)
*   [BoardEx](#boardex)
*   [Bobst Library Business Services](#bobst-library-business-services)
*   [Capital IQ Datafeeds](#capital-iq-datafeeds)
*   [Capital IQ Web-Based Platform](#capital-iq-web-based-platform)
*   [Compustat](#compustat)
*   [CRSP](#crsp)
*   [Datastream](#datastream)
*   [Dealscan](#dealscan)
*   [Dow Jones Averages](#dow-jones-averages)
*   [Dow Jones Factiva](#dow-jones-factiva)
*   [EBSCO Business Source Complete](#ebsco-business-source-complete)
*   [Federal Reserve Bank Reports](#federal-reserve-bank-reports)
*   [I/B/E/S](#ibes)
*   [IBES Guidance](#ibes-guidance)
*   [IRI](#iri)
*   [ISS: Institutional Shareholder Services](#iss-institutional-shareholder-services)
*   [JSTOR](#jstor)
*   [Lexis-Nexis](#lexis-nexis)
*   [Mergent-FISD](#mergent-fisd)
*   [NASTRAQ](#nastraq)
*   [NYCRDC](#nycrdc)
*   [NYSE TAQ](#nyse-taq)
*   [SDC](#sdc)
*   [SEC Order Execution](#sec-order-execution)
*   [Standard & Poor's NetAdvantage](#standard-poors-netadvantage)
*   [Thompson/Refinitiv](#thomsonrefinitiv)
*   [WorldScope Fundamentals](#worldscope-fundamentals)
*   [WRDS](#wrds)

## Bank Regulatory (formerly FDIC)

The Federal Deposit Insurance Corporation (FDIC) database contains financial data and history of all entities filing the Report Of Condition and Income (Call Report) and some savings institutions filing the OTS Thrift Financial Report (TFR). These entities include Commercial banks, savings banks, or savings and loans. FDIC files include structure data, financial time series data, complex derived integers data, ratio data, and merger history data.

Further information can be found on the WRDS website (see links below). FDIC data is available to NYU on the WRDS Web query site, with data manuals and users guides. SAS datasets and sample SAS programs are available in the WRDS cloud (wrds.wharton.upenn.edu).

*   [FDIC Government Website](https://www.fdic.gov/)
*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## Bloomberg

Bloomberg is an online financial information service that delivers raw data, news, and analytics through a single platform. The service provides real-time, historical, and descriptive financial data, supplemented by analytic tools such as pricing models and risk assessment models. Stern faculty and PhD students are given exclusive access to a Bloomberg station. For more information, call 212-998-0163 or send email to research@stern.nyu.edu .

Bobst library has three Bloomberg terminals on the 5th floor and two terminals on the Lower Level which are available to all NYU faculty and students.

*   [Bloomberg commercial website](https://www.bloomberg.com/)

## BoardEx

BoardEx offers relationship capital management data, including director profiles, director network, compensation, board summaries, organization analysis, announcements, and more. BoardEx is available to Stern researchers, and is accessible as Excel files via FTP. For more information, please send email to research@stern.nyu.edu.

*   [BoardEx Data (commercial website)](https://www.boardex.com/)

## Bobst Library Business Services

Bobst Library has a very large collection of online business databases. Most of them are text based (scholarly journals, news, analysis, etc.), and are accessible via Web browser through the NYU Virtual Business Library . Some databases are on dedicated terminals at the library only.

*   [Bobst Library Main Page](https://library.nyu.edu/)
*   [Ask a Librarian](https://library.nyu.edu/ask/)

## Capital IQ Datafeeds

Capital IQ Datafeeds are in three categories. Capital Structure provides extensive debt capital structure and equity capital structure information on tens of thousands of companies worldwide. Key Developments provide structured summaries of material news and events that may affect the market value of securities. People Intelligence covers over 4.5 million professionals and over 2.4 million people including private and public company executives, board members, and investment professionals.

The Capital IQ datafeeds are available on WRDS through query pages, along with documentation. The data is available in the WRDS cloud (wrds.wharton.upenn.edu) in the form of SAS datasets.

*   [Capital IQ Datafeeds (commercial website)](https://www.spglobal.com/marketintelligence/en/solutions/capital-iq-platform)
*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (via Stern wireless, and on public terminals at Stern and Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## Capital IQ Web-Based Platform

The Capital IQ web-based research platform combines deep information on companies, markets, and people worldwide. It includes tools for fundamental analysis, financial modeling, market analysis, screening, targeting, and relationship and workflow management. Stern faculty and PhD students should call the Stern Helpdesk at 212-998-0180 for information about obtaining access to the Capital IQ web-based platform.

## Compustat

COMPUSTAT is a bank of financial, statistical and marketing data on publicly traded American and Canadian companies. The database includes information from annual and quarterly company income statements, balance sheets, and statements of cash flows. It also provides data on aggregates and industry segments, banks, market prices, dividends, and earnings. Other products include executive compensation, Global Vantage, and the Capital IQ Datafeeds .

Further information can be found on the WRDS website (see links below). Compustat data is accessible through query pages on the WRDS website, as sequential datasets and SAS datasets in the WRDS cloud.

The CRSP/COMPUSTAT Merged Database combines COMPUSTAT company financial data with CRSP stock data, facilitating seamless time series examinations. This data is accessible through WRDS under CRSP.

*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (via Stern wireless, and on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## CRSP

The Center for Research in Security Prices (CRSP) maintains the most comprehensive collection of standard and derived security data available for the NYSE, AMEX and Nasdaq Stock Markets. CRSP is a research center at the University of Chicago Graduate School of Business, and maintains historical data spanning from December 1925 to the present. CRSPs trademark of unique issue identifiers tracks a continuous history of securities, providing a seamless time-series examination of the issues history.

Sterns CRSP subscription includes databases on Stocks, Indices, Treasuries, and Mutual Funds. Further information can be found on the WRDS website (see links below).

CRSP data is accessible through query pages on the WRDS website, and as sequential datasets and SAS datasets in the WRDS cloud (wrds.wharton.upenn.edu).

The CRSP/COMPUSTAT Merged Database combines COMPUSTAT company financial data with CRSP stock data, facilitating seamless time series examinations. The data is accessible through WRDS under CRSP.

In May of 2013, CRSP began delivering data files via the CRSP Cloud. Downloads can be arranged. For further information, send email to research@stern.nyu.edu.

*   [CRSP Website at University of Chicago](https://www.crsp.org/)
*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (via Stern wireless, and on public terminals at Stern and Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## Datastream

Datastream is an online historical financial database providing data on financial instruments, equity and fixed-income securities and indicators for over 175 countries and 60 markets worldwide. Datastream Equities, Economics, Commodities, and Futures modules are available via WRDS. Access to Datastream via Refinitiv Workspace can be requested through the Bobst Library Datastream Guide .

*   [Datastream Overview (commercial website)](https://www.lseg.com/en/products-services/market-data/datastream)

## Dealscan

DealScan is global commercial loan market data, including detailed terms and conditions on loan transactions. Further information can be found on the WRDS website (see links below).

WRDS-Reuters DealScan via WRDS includes Company, Facility, and Package data. It is accessible to NYU through the WRDS website, listed under Thomson Reuters. The WRDS cloud (wrds.wharton.upenn.edu) has SAS datasets in /wrds/tfn/sasdata/dealscan. For more information, visit the WRDS website.

*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (only via public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## Dow Jones Averages

The Dow Jones Averages are comprised of The Dow Jones Industrial Average (DJIA), The Dow Jones Transportation Average (DJTA) and The Dow Jones Utility Average (DJUA). Further information can be found on the WRDS website (see links below).

The Dow Jones data are available to NYU on the WRDS Web query site, with documentation of the variables. The WRDS cloud (wrds.wharton.upenn.edu) has sequential data, a SAS dataset, and a sample SAS program. The data are provided by Dow Jones Indexes.

In addition, Dow Jones Factiva (formerly Dow Jones Interactive) is available on the NYU Virtual Business Library website (see link below).

*   [Dow Jones Commercial Website](https://www.dowjones.com/)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (only on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)
*   [NYU Virtual Business Library (look for Factiva)](https://library.nyu.edu/research/business/)

## Dow Jones Factiva

This online data source provides a single point of access to a deep archive of news and business information not available on the free Web, allowing users to conduct in-depth research on companies, industries, regional affairs or any news. The database is available to all of NYU via web browser through the NYU Virtual Business Library (see link below).

*   [Dow Jones Factiva commercial website](https://www.dowjones.com/products/factiva/)
*   [NYU Virtual Business Library (Click on the subject tabs for links to Factiva)](https://library.nyu.edu/research/business/)

## EBSCO Business Source Complete

This online data source provides full text for more than 7,400 scholarly business journals and other sources, including full text for nearly 1,100 peer-reviewed business publications. Coverage includes virtually all subject areas related to business. This database provides full text (PDF) for more than 350 of the top scholarly journals dating as far back as 1922. The database is available to all of NYU via web browser through the NYU Virtual Business Library (see link below).

*   [EBSCO commercial website](https://www.ebsco.com/)
*   [Business Source Complete on NYU Virtual Business Library (contains Business Source Complete link)](https://library.nyu.edu/research/business/)

## Federal Reserve Bank Reports

The Federal Reserve Bank Reports databases on WRDS contain Foreign Exchange Rates (H.10 Report) and Interest Rates (H.15 Report) from the Federal Reserve Board, and FRB-Philadelphia State Indexes from the Federal Reserve Bank of Philadelphia. Further information can be found on the WRDS website (see links below).

FRB data is available to NYU on the WRDS Web query site. FRB data can also be obtained and manipulated using the WRDS linux programming environment. The environment primarily supports SAS, FORTRAN and C.

*   [Federal Reserve Board Statistics & Historical Data (government website)](https://www.federalreserve.gov/data.htm)
*   [Federal Reserve Bank of Philadelphia (official website)](https://www.philadelphiafed.org/)
*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (via Stern wireless, and on public terminals at Stern and Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## I/B/E/S

I/B/E/S is the Institutional Brokers Estimate System. Data includes Global Summary and Individual forecast information as well as buy-sell-hold recommendations for companies globally, plus cash flow, dividend, and pre-tax profit forecasts. Further information can be found on the WRDS website (see links below).

I/B/E/S data is available through the WRDS website, with documentation and data manuals. The WRDS cloud has SAS datasets and SAS sample programs. See links below.

*   [I/B/E/S Estimates (commercial website)](https://www.lseg.com/en/products-services/market-data/ibes)
*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (on public terminals in Library)](https://wrds-web.wharton.upenn.edu/)

## IBES Guidance

IBES Guidance is a datafeed with numeric company expectations across 14 measures using press releases, transcripts of corporate events, and IBES earnings forecasts. The subscription includes current and historical US data. IBES Guidance is available to NYU Stern academic researchers via FTP. For further information, please send email to research@stern.nyu.edu .

## IRI

Information Resources, Inc. (IRI) data contains point-of-sale marketing data from grocery store purchases. These purchases are continuously tracked across all UPC-coded brand-items in all categories. IRI data is accessible through query pages on the WRDS website, and as SAS datasets in the WRDS cloud.

*   [IRI home page (commercial website)](https://www.iriworldwide.com/)
*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## ISS: Institutional Shareholder Services

ISS data includes Governance data, Directors data, Shareholder Proposals, and Voting Analytics data. Further information can be found on the WRDS website (see links below).

The ISS databases are accessible through query pages on the WRDS website, and as SAS datasets in the WRDS cloud (wrds.wharton.upenn.edu).

*   [ISS Website](https://www.issgovernance.com/)
*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## JSTOR

JSTOR is a digital collection that includes over 2000 Business and Economics titles in the form of scholarly journals, primary sources, and books. JSTOR is accessible through the NYU Virtual Business Library (VBL) website. It can be found listed under Journal/Newspaper Articles under most of the main categories of the VBL.

*   [NYU Virtual Business Library](https://library.nyu.edu/research/business/)

## Lexis-Nexis

Lexis-Nexis is an on-line full-text library of business, company, financial and news information. Nexis Uni is available to all of NYU via web browser through the NYU Virtual Business Library. See link below.

*   [Lexis-Nexis (commercial website)](https://www.lexisnexis.com/)
*   [Nexis Uni (direct link to NYU subscribed service)](https://advance.lexis.com/?crid=a5e21e5e-f89c-4a39-a5a2-277b888f5b11)
*   [NYU Virtual Business Library](https://library.nyu.edu/research/business/)

## Mergent-FISD

Mergent FISD (Fixed Income Securities Database) is a U.S. Bond database covering more than 140,000 securities with over 550 data items. Data includes issuer-specific, issue-specific, and transaction information. Further information can be found on the WRDS website (see links below).

Mergent FISD data is accessible through query pages on the WRDS website, and as SAS datasets in the WRDS cloud, wrds.wharton.upenn.edu.

*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## NASTRAQ

NASTRAQ (The North American Securities Tracking and Quantifying System) displays trades and quotes for securities listed on NASDAQ. The database provides trade data, inside quote data, and dealer quote data according to symbol and desired date range. The service officially ended in 2006. Further information can be found on the WRDS website (see links below).

NASTRAQ legacy data is accessible through query pages on the WRDS website, and as SAS datasets in the WRDS cloud, wrds.wharton.upenn.edu.

*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## NYCRDC

The New York Census Research Data Center (NYCRDC) provides census confidential microdata to academic researchers. It is a consortium of 12 research organizations in the New York area. Access to NYCRDC data is in secure facilities at Cornell University and Baruch College. Suitable research projects must be approved before access is granted. More information can be found on the NYCRDC website.

*   [NYCRDC (home page)](https://www.vrdc.cornell.edu/ny-rdc/)

## NYSE TAQ

The NYSE TAQ (Trades and Quotes) database consists of intraday transactions from the New York Stock Exchange, American Stock Exchange, Nasdaq, and Smallcap. Data queries are by date range and timestamp. WRDS has specialized hardware for handling queries on these enormous datasets.

TAQ through 2014 and Millisecond TAQ from 2012 up to the present are accessible through query pages on the WRDS website, and SAS datasets in the WRDS cloud.

*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## SDC

SDC is a collection of financial transaction databases from Thomson Reuters which includes Mergers & Acquisitions, Global New Issues, Corporate Governance, Corporate Restructurings, Venture Capital, and Global Public Finance. For greater detail, see below.

The SDC Platinum interface for Windows is available to Stern faculty and PhD students for installation at Stern only through December 2023. The SDC data is also now available via Refinitiv Workspace. For more information and assistance, send email to research@stern.nyu.edu.

*   [SDC Platinum Overview (commercial web page)](https://www.lseg.com/en/products-services/market-data/deals-intelligence/sdc-platinum)
*   Stern Access Datasets in SDC
    *   Mergers & Acquisitions
        *   US Targets
        *   Non-US Targets
        *   Joint Ventures / Alliances
        *   Repurchases
    *   Global New Issues Databases
        *   All Equity
        *   Common Stock
        *   Convertible Equity
        *   Pipeline and Registrations
        *   Private Equity
        *   All Bonds
        *   Non-Convertible Bonds
        *   Preferred Stock
        *   Mortgage/Asset Backed Bonds
        *   Pipeline and Registrations
        *   MTN Programs
        *   Private Debt
    *   Corporate Governance
        *   Poison Pills
        *   Proxy Fights
    *   Corporate Restructurings
        *   Full Detail Bankruptcies (1988-present)
        *   Limited Detail Bankruptcies (1980-1990)
        *   Exchange Offers
    *   VentureXpert
        *   Industry Resources
            *   Funds
            *   Firms
            *   Portfolio Companies
            *   Limited Partners
            *   Executives
        *   Industry Statistics (Fund)
            *   Commitments
            *   Performance Statistics
        *   Industrial Statistics (Company)
            *   Investments (Disbursements)
        *   Initial Public Offerings
        *   Mergers & Acquisitions
    *   Global Public Finance
        *   U.S. New Issues
        *   Non-U.S. New Issues
        *   MuniProfiles
        *   Refunding Candidates
        *   Project Finance

## SEC Order Execution

SEC Order Execution is the SEC-mandated disclosure of order execution statistics from market centers that trade national market system securities. Further information can be found on the WRDS website (see links below).

ecurities Exchange Commission-mandated Disclosure of Order Execution Statistics (through 2005 only) are available to NYU via WRDS. The WRDS website has a query page and documentation for each field of the data. The WRDS cloud (wrds.wharton.upenn.edu) has SAS datasets in /wrds/doe/sasdata.

*   [SEC Rule 11Ac1-5](https://www.sec.gov/rules/final/34-43590.htm)
*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (on public terminals in Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## Standard & Poor's NetAdvantage

Standard & Poors NetAdvantage is a search driven database of global industry overviews, company profiles, and mutual funds. NetAdvantage is accessible through the NYU Virtual Business Library (VBL) website. Links to the service appear on the Company & Financial Information and the Industry Information pages of the VBL.

*   [NYU Virtual Business Library](https://library.nyu.edu/research/business/)

## Thompson/Refinitiv

Thomson Reuters is a global provider of data, analysis and information tools. Thomson Financial Securities Data (TFSD) had been created in 1999 by the joining of The Investext Group, Securities Data Company and CDA/Spectrum. Thomson Reuters was formed when Thomson Financial merged with Reuters.

The Thomson Reuters databases on WRDS cover Datastream, Insiders Data, 13f Institutional Holdings, Lipper Hedge Fund Database (TASS), Mutual Funds Holdings, Refinitiv ESG, Worldscope, and WRDS-Reuters DealScan, which has global commercial loan data. Further information can be found on the WRDS website (see links below).

Thomson/Refinitiv data available to NYU through WRDS are presented through web query pages, with documentation also provided on the WRDS website. Direct login to the WRDS linux server (wrds.wharton,upenn.edu) provides SAS datasets and sequential data for these products. The datasets include Mutual Funds, Institutional (13f) holdings, Insiders data, and WRDS-Reuters DealScan.

Also available on WRDS, but under a separate heading, are the I/B/E/S datasets. Other available data products from Thomson Reuters, but not on WRDS include SDC, and IBES Guidance data.

*   [WRDS Introduction (includes how to get an account)](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
*   [WRDS Website (to request an account or to login)](https://wrds-web.wharton.upenn.edu/)
*   [WRDS Without Account (via Stern wireless, and on public terminals at Stern and Bobst Library)](https://wrds-web.wharton.upenn.edu/)

## WorldScope Fundamentals

WorldScope Fundamentals include detailed information on public companies in more than 50 developed and emerging markets worldwide. Worldscope includes up to 20 years of historical data on 31,000 active and 9,000 inactive companies, using more than 1,500 data elements on each company. WorldScope is known by researchers as international Compustat.

WorldScope Fundamentals are available via WRDS, and are incorporated with Datastream via Refinitiv Workspace.

*   [Worldscope Fundamentals Overview (commercial website)](https://www.lseg.com/en/products-services/market-data/worldscope)

## WRDS

Wharton Research Database Services is an internet based research business data service from the Wharton School. WRDS data consists of historical financial information for banks, government bonds, stock exchanges, and major companies. It is intended solely for research and instructional purposes.

*   [Accessing WRDS Without a Password](https://wrds-web.wharton.upenn.edu/wrds/support/access.cfm)
```

```markdown
# NYU Stern Center for Research Computing (SCRC) Documentation

## Accessing WRDS (Wharton Research Data System)

### Access Without an Account

The WRDS website can be accessed without an account at WRDS Connect on public workstations at Bobst Library.

### Access With an Account and Password

Users with a WRDS account can log in at Wharton Research Database Services from on or off campus.

*   Faculty, PhD, and Research Assistant accounts come with:
    *   Personal and shared work space on the WRDS server.
    *   A personal record of queries.
    *   Secure access to the WRDS linux server and data.
*   Faculty may apply for Class accounts which allow their students to use WRDS from off campus.

### New Accounts

New York University faculty, administrators, staff, and students may apply for a WRDS account. Non-PhD students may also request a Research Assistant account for a limited time if they are doing research with a faculty member. Faculty may request accounts for classes.

### Requesting an Account

1.  Visit Wharton Research Database Services with your Web browser.
2.  Click on the **Register** button at the top of the login page.
3.  Complete the form, read the WRDS Terms of Use Statement, and submit.
4.  The NYU Representative for WRDS will receive a message from WRDS regarding your account application.
5.  The NYU Representative will check your NYU affiliation.
6.  Once your account request is approved, WRDS will send you an e-mail with instructions for setting your password.

### Support

*   For suggestions, comments, questions, or problems using this service, contact research@stern.nyu.edu.
*   For problems, questions, or suggestions concerning WRDS database access or data querying, or programming on the WRDS server, click the **Contact** button at the top of the WRDS Login Page or WRDS Home Page and complete the form.

## Research Software

### Anaconda

*   **Availability:** Linux, Windows, Apps@Stern
*   Anaconda is a distribution of the Python and R programming languages for scientific computing, that aims to simplify package management and deployment. The distribution includes data-science packages suitable for Windows, Linux, and macOS. Anaconda is available on the SCRC servers, Apps@Stern, and the Anaconda Community Edition can be installed on your local machine.
*   [Anaconda website](link to Anaconda website)
*   [Anaconda installation guide](link to Anaconda installation guide)
*   [Anaconda tutorials](link to Anaconda tutorials)

### Eviews

*   **Availability:** Apps@Stern
*   EViews is software for general statistical analysis, time series estimation and forecasting, large-scale model simulation, presentation graphics, and simple data management. Eviews is available to Stern Faculty and PhD Students on Apps@Stern.
*   [EViews commercial website](link to EViews commercial website)

### Filezilla

*   **Availability:** Linux, Windows
*   FileZilla is an open-source file transfer program that runs on Windows, Mac, and Linux. Use it to transfer files to and from your local machine and SCRC Linux servers.
*   [FileZilla website](link to FileZilla website)

### Java

*   **Availability:** Linux, Windows
*   Java is a high-level, class-based, object-oriented programming language that is designed to have as few implementation dependencies as possible. A version of Java is available to Stern faculty and PhD students on SCRC servers, both on Windows and Linux machines. You can also install Java on a local machine.
*   [Java website](link to Java website)
*   [Java Installation Guide](link to Java Installation Guide)
*   [Java tutorial](link to Java tutorial)

### Mathematica

*   **Availability:** NYU Virtual Computer Lab
*   Mathematica is a fully integrated technical computing system, combining interactive calculation (both numerical and symbolic), visualization tools, and a complete programming environment. Faculty can purchase Mathematica from ITS. NYU has a campus-wide site license for Mathematica for Windows and Mac. For more information, please see the links below. Stern PhD students who need to install Mathematica on their PC should contact the Stern Doctoral Office. Mathematica is available for use by students via Web browser through the NYU Virtual Computer Lab. It is also installed on all NYU Data Services workstations.
*   [Wolfram Commercial Website](link to Wolfram Commercial Website)
*   [Accessing Wolfram Research Software Suite at NYU](link to documentation)

### MATLAB

*   **Availability:** Linux, Windows, NYU Virtual Computer Lab
*   MATLAB, which stands for MATrix LABoratory, is an interactive system whose basic data element is an array that does not require dimensioning. It is a high-level matrix/array language with control flow statements, functions, data structures, input/output, and object-oriented programming features. Typical uses include math and computation, algorithm development, modeling, simulation, prototyping, and data analysis. MATLAB is available to everyone at NYU through the MATLAB Portal. MATLAB is also available to Stern faculty and PhD students on the research servers at SCRC. MATLAB is available for use by Students through the NYU Virtual Computer Lab.
*   [NYU Virtual Computer Lab](link to NYU Virtual Computer Lab)
*   [MathWorks commercial website](link to MathWorks commercial website)
*   [MathWorks Product Overview](link to MathWorks Product Overview)
*   [MathWorks documentation](link to MathWorks documentation)
*   [NYU Research Software](link to NYU Research Software documentation)

### Minitab

*   **Availability:** Apps@Stern, NYU Virtual Computer Lab, NYU Research Software
*   Minitab is a data analysis software package. Minitab provides users with tools to perform statistical analysis, including hypothesis testing, regression analysis, and ANOVA. It runs on Windows, MacOS, and Linux computers.

### Oracle Crystal Ball

*   **Availability:** Apps@Stern
*   Oracle Crystal Ball is an online predictive model application that runs in conjunction with Microsoft Excel. It is used primarily for teaching purposes. Crystal Ball is available to the Stern School of Business community on Apps @ Stern.

### PuTTY

*   **Availability:** Windows
*   PuTTY is a simple, compact Windows program for logging in to Unix or Linux via Telnet or SSH. PuTTY is available as a free download. It also can be found installed on all Data Service Studio workstations on the 5th floor of Bobst Library.
*   [PuTTY Download Page](link to PuTTY Download Page)

### Python

*   **Availability:** Linux, Windows, Apps@Stern
*   Python is a widely used general-purpose, high-level programming language. Its design philosophy emphasizes code readability, and its syntax allows programmers to express concepts in fewer lines of code than would be possible in languages such as C. The language provides constructs intended to enable clear programs on both a small and large scale. Python is available to all researchers on Linux and Windows, on SCRC. You can also install Python locally on your computer. Python is also available on Apps@Stern.
*   [Python website](link to Python website)
*   [Basics of Python](link to Basics of Python documentation)
*   [Pip documentation](link to Pip documentation)

### Qualtrics

*   **Availability:** SternID, NYUHome
*   Qualtrics is software for creating and administering web-based surveys. Stern faculty and students are entitled to a Qualtrics account. It is also available from the NYU Survey Service through the Research tab in NYUHome. For further information, see NYU Survey Service (Qualtrics).
*   [Qualtrics Commercial Website](link to Qualtrics Commercial Website)

### R

*   **Availability:** Linux, Windows, Apps@Stern, NYU Virtual Computer Lab
*   R, also known as GNU S, is a free statistical and graphics language and environment. It is similar to the S language, and is written for Unix, Windows, and Mac. R is available on Apps@Stern, the Stern Citrix server. It is also available to Students through the NYU Virtual Computer Lab (VCL), the NYU Citrix server. R can be downloaded free and installed locally, as well. See link below.
*   [NYU Virtual Computer Lab](link to NYU Virtual Computer Lab)
*   [The R Project for Statistical Computing](link to The R Project for Statistical Computing)
*   [Learn R](link to resources to learn R)

### SAS and Enterprise Miner

*   **Availability:** Linux, Windows, NYU Virtual Computer Lab
*   SAS (Statistical Analysis System) is an integrated suite of modular products facilitating four data-driven tasks: data access, data management, data analysis, and data presentation. SAS supports SQL (Structured Query Language), and can subset and merge a wide range of data sources. SAS software computes simple descriptive statistics, and complicated and highly specialized statistical and econometric analyses. These include regression, planning, simulation, forecasting, quality improvement, project management, decision support, and more. In addition, SAS software produces reports that range from a simple listing of a data set to customized reports of complex relationships. SAS Enterprise Miner streamlines the data mining process to create highly accurate predictive and descriptive models based on analysis of vast amounts of data. The Linux version of SAS is available to Stern faculty and PhD students on SCRC servers. The Windows version of SAS is available for use by students via web browser through the NYU Virtual Computer Lab. Licenses and software for the installation of Windows versions of SAS are available for purchase by NYU faculty, staff, and matriculated graduate students through nyu.onthehub.com. Stern PhD students should contact the Stern Doctoral Office to obtain a SAS license.
*   [SAS Product Description (NYU)](link to SAS Product Description (NYU))
*   [NYU Data Services supported software packages](link to NYU Data Services supported software packages)
*   [SAS commercial website](link to SAS commercial website)
*   [UCLA SAS Website](link to UCLA SAS Website)

### SPSS

*   **Availability:** Windows
*   SPSS (Statistical Package for Social Sciences) is a program with a wide range of statistical procedures for basic analysis including: aggregate, counts, crosstabs, cluster, descriptives, factor analysis, regression and cluster analysis. SPSS for Windows or Mac is available for purchase by NYU faculty, administrators, and staff at a discounted price from the NYU Computer Store. NYU Students who are not in the Stern Doctoral Program may purchase the student versions of SPSS through the NYU Computer Store.
*   [SPSS Description (NYU)](link to SPSS Description (NYU))
*   [NYU Data Services supported software](link to NYU Data Services supported software)
*   [NYU Computer Store Software](link to NYU Computer Store Software)
*   [SPSS commercial website](link to SPSS commercial website)

### Stat/Transfer

*   **Availability:** Windows
*   Stat/Transfer is a data conversion software utility which transfers data files between different programs. It supports more than 30 different file formats, including SAS and JMP, Matlab, Stata, SPSS, R, Minitab, Excel and Access, and ASCII. Faculty may purchase Stat/Transfer directly from http://www.stattransfer.com. If you are Stern faculty or a PhD student, you can request a local PC installation of Stat/Transfer by emailing us at research@stern.nyu.edu.

### Stata

*   **Availability:** Linux, Windows, Apps@Stern, NYU Virtual Computer Lab
*   Stata is a complete, integrated statistical package that provides tools for data analysis, data management, and graphics. Stata is available for use by Stern faculty and students through Apps@Stern, and by students through the NYU Virtual Computer Lab. Stata runs via Web browser on these systems. Stata is also available to Stern researchers on SCRC servers. Stata for local installation can be purchased at a discount by NYU faculty, staff, and students. See Stata Prof+ Plan to order.
*   [Stata commercial website](link to Stata commercial website)
*   [Stata overview](link to Stata overview)
*   [Resources for Learning Stata](link to resources to learn Stata)

## SCRC Services

The Center is devoted to providing world-class computational facilities and services to researchers at the Stern School of Business at New York University.

These services include:

*   A moderately sized Slurm HPC cluster.
*   Cloud Computing (Virtual Machines).
*   Data acquisition and storage.
*   Research software.
*   Access to WRDS (Wharton Research Data System).

### Research Datasets

Empowering researchers by collaborating with various data repositories, platforms and academic institutions to provide a collection of datasets from diverse disciplines.

### Compute

Supporting faculty and researchers with a wide range of computing services and resources for their projects.

### Storage

Facilitating extensive computational data storage in high-speed, robust and scalable storage systems, supporting researchers diverse needs and requirements.

## News and Announcements

Please check back here for the latest news and maintenance updates.

*   April 17: Scheduled Maintenance
*   March 12: Scheduled Maintenance Cancelled

## Support

Stuck or need help with something? We offer personalized support and guidance.

*   Contact one of us directly or send questions to our groups email at scrc-list@stern.nyu.edu.

SCRC also offers help through personal consultations such as:

*   Finding the right software, datasets, or computational services that best fit your research needs.
*   Using or understanding our compute services such as batch or interactive processing.
*   Purchasing, transferring, or storing data.
*   Getting and using a virtual machine for specialized computational or secure data requirements.

### Stern IT

For general non-research support questions contact the Stern IT Helpdesk. To contact the helpdesk, users can submit a support ticket through the online portal, send an email, or call the helpdesk hotline during operating hours.

## Resources

### Additional Resources

*   [Linux Learning the Shell](link to Linux Learning the Shell)
*   [NYU](link to NYU)
*   [NYU High Performance Computing](link to NYU High Performance Computing)
*   [Stern IT Helpdesk](link to Stern IT Helpdesk)
*   [NYU Data Services](link to NYU Data Services)
*   [NYU Computer Store](link to NYU Computer Store)
*   [NYU Virtual Business Library](link to NYU Virtual Business Library)
*   [Bobst Library](link to Bobst Library)
*   [NYU VPN](link to NYU VPN)

### FastX Resources

*   [FastX Desktop Client Download](link to FastX Desktop Client Download)
*   [FastX Desktop Client Guide](link to FastX Desktop Client Guide)

## Storage Information

When you log in to any of SCRCs systems, you will find yourself in your home directory. A bighome is separate storage from your home directory where you keep your data and larger files.

### Your home directory (homedir)

*   SCRC home directories have a capacity of around 5-10GB.
*   Home directories are backed up every hour.
*   They are designed for storing small files like programs and scripts.
*   To find the full path to your home directory, type the command `pwd`.  For example, `/homedir/employees/X/yourHomedir`.
*   Check your home directory usage with the command `quota -s`.

### Your bighome (bigdata)

*   If you need more space than what is provided in your home directory, email scrc-list@stern.nyu.edu for access to a bighome.
*   Bighome storage is accessed from your home directory by the symlink `bigdata`, i.e., `cd bigdata`.
*   Bighome storage is backed up nightly.
*   There is no formal quota limit, but researchers should contact SCRC if they need more than 1TB of storage.
*   Check your storage usage with the command `du -sh`.
```