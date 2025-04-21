```markdown
---
title: "Available Software Overview"
category: "software-and-applications"
description: "A list of commonly used research software available at SCRC, including statistical packages, programming languages, and data analysis tools."
---

# Available Software Overview

This page provides an overview of the commonly used research software available to the NYU Stern community through the Stern Center for Research Computing (SCRC) and associated NYU resources. This includes statistical packages, programming languages, data analysis tools, and utilities accessible on SCRC Linux servers, Apps@Stern, the NYU Virtual Computer Lab (VCL), or for local installation.

## Accessing Software on SCRC Linux Servers

Many software packages are available on the SCRC Linux servers (`rnd.scrc.nyu.edu` or `vleda.scrc.nyu.edu`) via environment modules.

To see available modules, use the command:

```bash
module avail
```

To load a specific module (e.g., Python 3.9.7), use:

```bash
module load python/3.9.7
```

To run graphical applications like RStudio or XStata, you typically need to:
1.  Connect via [FastX](link-to-fastx-doc) (See [Getting Started with Slurm Interactive Jobs](link-to-interactive-jobs)).
2.  Start an interactive job on a compute node using `srun`.
3.  Load the appropriate module.
4.  Launch the application.

Example `srun` command for an interactive session:

```bash
srun --pty --mem=8gb --time=1:00:00 --cpus-per-task=1 --nodes=1 /bin/bash
```

## Software List

### Anaconda

*   **Description:** Anaconda is a distribution of the Python and R programming languages tailored for scientific computing. It simplifies package management and deployment, including numerous data-science packages.
*   **Availability:**
    *   SCRC Linux Servers (Load via `module load anaconda3/...`)
    *   Apps@Stern
    *   Windows/Mac/Linux (Install Anaconda Community Edition locally)
*   **Usage on SCRC:** Can be used interactively (e.g., with Jupyter Notebooks within an `srun` session) or in batch jobs.
    ```bash
    # Example: Load Anaconda module
    module load anaconda3/py3.9

    # Example: Start Jupyter Notebook in an interactive session
    jupyter-notebook
    ```
*   **Links:**
    *   [Anaconda Website](https://www.anaconda.com/)
    *   [Run Anaconda/Jupyter Environment on SLURM](link-to-anaconda-slurm-tutorial)

### Eviews

*   **Description:** EViews provides tools for general statistical analysis, time series estimation and forecasting, large-scale model simulation, graphics, and data management.
*   **Availability:** Apps@Stern (for Stern Faculty and PhD Students)
*   **Links:**
    *   [EViews Commercial Website](https://www.eviews.com/)

### FileZilla

*   **Description:** FileZilla is a free, open-source graphical FTP, FTPS, and SFTP client for transferring files between your local machine and remote servers.
*   **Availability:** Windows, Mac, Linux (Download locally)
*   **Usage for SCRC:** Used to transfer files to/from SCRC Linux servers (`rnd.scrc.nyu.edu` or `vleda.scrc.nyu.edu`).
    1.  Ensure you are connected to the [NYU VPN](link-to-nyu-vpn) if off-campus.
    2.  Start FileZilla.
    3.  Enter connection details:
        *   Host: `rnd.scrc.nyu.edu` (or `vleda.scrc.nyu.edu`)
        *   Username: `<Your Stern NetID>`
        *   Password: `<Your Stern Password>`
        *   Port: `22`
    4.  Click "Quickconnect".
    5.  Drag and drop files between the local (left) and remote (right) panels.
*   **Links:**
    *   [FileZilla Website](https://filezilla-project.org/)

### Java

*   **Description:** Java is a high-level, class-based, object-oriented programming language designed for platform independence.
*   **Availability:**
    *   SCRC Linux Servers
    *   Windows/Mac/Linux (Install locally)
*   **Links:**
    *   [Java Website](https://www.java.com/)
    *   [Java Tutorial](https://docs.oracle.com/javase/tutorial/)

### Mathematica

*   **Description:** Mathematica is an integrated technical computing system for symbolic and numerical calculation, visualization, and programming.
*   **Availability:**
    *   NYU Virtual Computer Lab (VCL) (Students)
    *   NYU Data Services workstations
    *   Local Installation:
        *   Faculty can purchase via ITS. NYU has a site license.
        *   Stern PhD students: Contact the Stern Doctoral Office.
*   **Links:**
    *   [Wolfram Commercial Website](https://www.wolfram.com/mathematica/)
    *   [Accessing Wolfram Software at NYU](https://www.nyu.edu/life/information-technology/software-hardware/software/mathematica.html)

### MATLAB

*   **Description:** MATLAB (MATrix LABoratory) is a high-level language and interactive environment for numerical computation, visualization, and programming. Widely used for math, computation, algorithm development, modeling, simulation, and data analysis. Supports GPU computation.
*   **Availability:**
    *   SCRC Linux Servers (Load via `module load matlab/...`)
    *   Windows (via SCRC Virtual Machines or local install)
    *   NYU Virtual Computer Lab (VCL)
    *   Local Installation: Available to everyone at NYU through the [MATLAB Portal](https://www.mathworks.com/academia/tah-portal/nyu-591482.html).
*   **Usage on SCRC:** Can run interactively (requires FastX/`srun`) or in batch jobs. Supports GPU nodes (`--partition=gpu`).
    ```bash
    # Example: Load MATLAB module
    module load matlab/2019a

    # Example: Run MATLAB script in batch job (from gpu-bench.sbatch)
    matlab -nojvm < gpu-bench.m

    # Example: Run MATLAB GUI interactively (requires FastX/srun)
    matlab
    ```
*   **Links:**
    *   [MathWorks Commercial Website](https://www.mathworks.com/)
    *   [MathWorks Documentation](https://www.mathworks.com/help/matlab/)
    *   [NYU Research Software](https://www.nyu.edu/life/information-technology/software-hardware/software.html)
    *   [MATLAB GPU Tutorial](link-to-matlab-gpu-tutorial)

### Minitab

*   **Description:** Minitab is a statistical software package for data analysis, hypothesis testing, regression, ANOVA, and more.
*   **Availability:**
    *   Apps@Stern
    *   NYU Virtual Computer Lab (VCL)
    *   NYU Research Software (Installation options may vary)
    *   Windows, MacOS, Linux

### Oracle Crystal Ball

*   **Description:** Oracle Crystal Ball is a predictive modeling application that integrates with Microsoft Excel, primarily used for teaching.
*   **Availability:** Apps@Stern

### PuTTY

*   **Description:** PuTTY is a free, lightweight SSH and Telnet client for Windows, used to connect to remote Linux/Unix servers via a command-line interface.
*   **Availability:** Windows (Download locally)
*   **Usage for SCRC:**
    1.  Download and install PuTTY.
    2.  Start PuTTY.
    3.  Enter Host Name: `rnd.stern.nyu.edu` or `vleda.stern.nyu.edu`.
    4.  Ensure Port is `22` and Connection type is `SSH`.
    5.  Click Open.
    6.  Accept the server's host key if prompted (first time only).
    7.  Log in with your Stern NetID and password.
*   **Links:**
    *   [PuTTY Download Page](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

### Python

*   **Description:** Python is a versatile, high-level programming language widely used in data science, scripting, web development, and more. SCRC supports using Python within virtual environments for managing project dependencies.
*   **Availability:**
    *   SCRC Linux Servers (Multiple versions available via `module load python/...`)
    *   Windows/Mac/Linux (Install locally, often via Anaconda)
    *   Apps@Stern (Typically via Anaconda)
*   **Usage on SCRC:**
    *   Use `module load python/<version>` to access system Python.
    *   Recommended practice: Create project-specific virtual environments in your `/bigdata` directory using `virtualenv` or `conda`.
    *   Run scripts directly (`python your_script.py`) or via Slurm batch jobs.
    ```bash
    # Example: Load Python module
    module load python/3.9.7

    # Example: Create a virtual environment (run once)
    # module load python/3.9.7 # Load desired python version first
    # virtualenv ~/bigdata/my_python_env

    # Example: Activate virtual environment
    # source ~/bigdata/my_python_env/bin/activate

    # Example: Install packages within active environment
    # pip install numpy pandas

    # Example: Deactivate virtual environment
    # deactivate
    ```
*   **Links:**
    *   [Python Website](https://www.python.org/)
    *   [Python Virtual Environment Tutorial](link-to-python-venv-tutorial)
    *   [Python Simple Job Tutorial](link-to-python-simple-job-tutorial)
    *   [Python Array Job Tutorial](link-to-python-array-job-tutorial)

### Qualtrics

*   **Description:** Qualtrics is a web-based platform for creating, distributing, and analyzing surveys.
*   **Availability:**
    *   Stern faculty and students (via Stern Qualtrics account)
    *   NYU Community (via NYU Survey Service in NYUHome)
*   **Links:**
    *   [NYU Survey Service (Qualtrics)](https://www.nyu.edu/life/information-technology/teaching-and-learning-services/instructional-technology-tools-and-services/online-surveys-qualtrics.html)
    *   [Qualtrics Commercial Website](https://www.qualtrics.com/)

### R

*   **Description:** R is a free software environment and language for statistical computing and graphics. It offers a wide variety of statistical and graphical techniques. RStudio provides a popular integrated development environment (IDE) for R.
*   **Availability:**
    *   SCRC Linux Servers (Multiple versions via `module load R/...`; RStudio via `module load rstudio`)
    *   Apps@Stern
    *   NYU Virtual Computer Lab (VCL)
    *   Windows/Mac/Linux (Install locally from CRAN)
*   **Usage on SCRC:**
    *   Run R scripts in batch jobs using `R CMD BATCH`.
    *   Run R interactively in the terminal or via RStudio (requires FastX/`srun`).
    *   Install personal packages locally within your home or `/bigdata` directory.
    ```bash
    # Example: Load R module
    module load R/4.3.2

    # Example: Run R script in batch (from fitspline.sbatch)
    # R CMD BATCH --no-save --no-restore fitspline.R fitspline.$SLURM_ARRAY_TASK_ID.Rout

    # Example: Load RStudio module (requires interactive session)
    module load rstudio

    # Example: Start RStudio (requires interactive session)
    rstudio
    ```
*   **Links:**
    *   [The R Project for Statistical Computing](https://www.r-project.org/)
    *   [CRAN (Comprehensive R Archive Network)](https://cran.r-project.org/)
    *   [Run RStudio on SLURM](link-to-run-rstudio-slurm)
    *   [Install Local R Packages](link-to-install-r-packages)
    *   [R Fitspline Tutorial](link-to-r-fitspline-tutorial)
    *   [R Monte Carlo Simulation Tutorial](link-to-r-montecarlo-tutorial)

### SAS and Enterprise Miner

*   **Description:** SAS (Statistical Analysis System) is a comprehensive software suite for data access, management, analysis, and presentation. SAS Enterprise Miner provides tools specifically for data mining.
*   **Availability:**
    *   SCRC Linux Servers (Load via `module load sas/...`)
    *   Windows (via SCRC Virtual Machines or licensed install)
    *   NYU Virtual Computer Lab (VCL)
    *   Local Installation (Windows): Purchase licenses via [nyu.onthehub.com](https://nyu.onthehub.com/) (Faculty, Staff, Grad Students); Stern PhD students contact Doctoral Office.
*   **Usage on SCRC:** Run SAS programs in batch jobs.
    ```bash
    # Example: Load SAS module
    module load sas/9.4

    # Example: Run SAS program in batch (from crosstab.sbatch)
    sas -nodms crosstab.sas
    ```
*   **Links:**
    *   [SAS Commercial Website](https://www.sas.com/)
    *   [SAS Tutorial](link-to-sas-tutorial)
    *   [UCLA SAS Resources](https://stats.oarc.ucla.edu/sas/)

### SPSS

*   **Description:** SPSS (Statistical Package for the Social Sciences) is a widely used program for statistical analysis in social science.
*   **Availability:**
    *   Windows/Mac (Purchase discounted licenses via NYU Computer Store)
    *   NYU Data Services Workstations
*   **Links:**
    *   [SPSS Commercial Website](https://www.ibm.com/analytics/spss-statistics-software)
    *   [NYU Computer Store](https://www.bookstores.nyu.edu/technology.store)

### Stat/Transfer

*   **Description:** Stat/Transfer is a utility designed to simplify the conversion of data between different statistical package formats (e.g., Stata, SAS, SPSS, R, Excel). Supports over 30 formats.
*   **Availability:**
    *   Windows (via SCRC installation request or purchase)
    *   Stern Faculty/PhD Students: Request local PC installation by emailing research@stern.nyu.edu.
    *   Purchase directly from [Stat/Transfer](http://www.stattransfer.com).
*   **Links:**
    *   [Stat/Transfer Website](http://www.stattransfer.com)

### Stata

*   **Description:** Stata is an integrated statistical software package providing tools for data analysis, data management, and graphics. XStata refers to the graphical interface version.
*   **Availability:**
    *   SCRC Linux Servers (Load via `module load stata/...` or `module load xstata-...`; XStata requires interactive session)
    *   Apps@Stern
    *   NYU Virtual Computer Lab (VCL)
    *   Windows/Mac/Linux (Purchase discounted licenses via [Stata Prof+ Plan](https://www.stata.com/order/new/edu/profplus/))
*   **Usage on SCRC:**
    *   Run Stata `.do` files in batch jobs.
    *   Run Stata interactively in the terminal.
    *   Run XStata graphical interface (requires FastX/`srun`).
    ```bash
    # Example: Load Stata module (Command Line)
    module load stata-se/17.0

    # Example: Load XStata module (GUI - requires interactive session)
    module load xstata-se/17.0

    # Example: Start XStata GUI (requires interactive session)
    xstata
    ```
*   **Links:**
    *   [Stata Commercial Website](https://www.stata.com/)
    *   [Resources for Learning Stata](https://www.stata.com/links/resources-for-learning-stata/)
    *   [Run XStata on SLURM](link-to-run-xstata-slurm)
```