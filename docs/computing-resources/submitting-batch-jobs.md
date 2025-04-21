# Submitting Batch Jobs

This guide provides detailed instructions on how to create Slurm batch scripts (`.sbatch` files) and submit non-interactive jobs to the SCRC Slurm cluster. Batch jobs are ideal for computationally intensive tasks that do not require direct user interaction during execution.

## What is a Batch Job?

A batch job is a script containing commands and Slurm directives that is submitted to the Slurm workload manager. Slurm schedules the job to run on the cluster's compute nodes when the requested resources become available. This allows you to queue up tasks and let them run in the background without needing to stay logged in or actively monitor them. The output and errors are typically written to files for later review.

## Creating a Slurm Batch Script (`.sbatch`)

A Slurm batch script is a text file, typically ending with `.sbatch`, that contains two main components:
1.  `#SBATCH` directives: These lines, starting with `#SBATCH`, provide instructions to the Slurm scheduler about the job's requirements (e.g., runtime, memory, partition) and behavior (e.g., email notifications, output files).
2.  Shell commands: These are the commands needed to set up the environment and execute your program (e.g., loading modules, running Python/SAS/MATLAB/R scripts).

### Basic Structure

```bash
#!/bin/bash
#
# [your-script-name.sbatch]
# Description of what the script does

# --- SLURM Directives ---
#SBATCH --job-name=your_job_name      # Job name
#SBATCH --output=output_file.%j.out   # Standard output file (%j expands to job ID)
#SBATCH --error=error_file.%j.err     # Standard error file (%j expands to job ID)
#SBATCH --time=HH:MM:SS               # Wall clock time limit
#SBATCH --mem=MemoryG                 # Memory requirement (e.g., 4G, 8G)
#SBATCH --partition=partition_name    # Partition (queue) to submit to (e.g., test, gpu)
#SBATCH --mail-type=BEGIN,END,FAIL    # Email notifications
#SBATCH --mail-user=your_netid@stern.nyu.edu # Your email address

# --- Environment Setup ---
echo "Job started on $(hostname) at $(date)"
module purge                          # Start with a clean environment
module load software/version          # Load necessary modules (e.g., python/3.9.7, sas/9.4)

# --- Job Execution ---
# Your commands go here
# Example: python your_script.py
# Example: sas your_script.sas
# Example: R CMD BATCH your_script.R

echo "Job finished at $(date)"
```

### Common `#SBATCH` Directives

| Directive             | Description                                                                                                  | Example                            |
| --------------------- | ------------------------------------------------------------------------------------------------------------ | ---------------------------------- |
| `--job-name`          | Specifies a name for the job.                                                                                | `--job-name=my_analysis`           |
| `--output`            | Specifies the file path for standard output. `%j` is replaced by the job ID, `%A` by job array ID, `%a` by task ID. | `--output=job_%j.out`              |
| `--error`             | Specifies the file path for standard error. If omitted, stderr is merged with stdout.                        | `--error=job_%j.err`               |
| `--time`              | Sets the maximum wall clock time limit (Hours:Minutes:Seconds).                                              | `--time=02:30:00`                  |
| `--mem`               | Specifies the memory required per node (e.g., M for Megabytes, G for Gigabytes).                             | `--mem=8G`                         |
| `--partition`         | Specifies the partition (queue) to submit the job to. Common partitions include `test`, `gpu`, `bigmem`.     | `--partition=test`                 |
| `--mail-type`         | Specifies events for email notification (e.g., `BEGIN`, `END`, `FAIL`, `ALL`).                                 | `--mail-type=END,FAIL`             |
| `--mail-user`         | Specifies the email address for notifications.                                                               | `--mail-user=xy12@stern.nyu.edu`   |
| `--export`            | Exports environment variables from the submission environment to the job. `ALL` exports all variables.     | `--export=ALL`                     |
| `--nodes`             | Specifies the number of nodes to allocate.                                                                   | `--nodes=1`                        |
| `--cpus-per-task`     | Specifies the number of CPU cores required per task.                                                         | `--cpus-per-task=4`                |
| `--array`             | Submits a job array. Specifies the task ID range (e.g., `1-5`, `1-10:2`).                                    | `--array=1-10`                     |
| `--gres` or `--gpus`  | Requests generic resources, commonly used for GPUs.                                                          | `--gres=gpu:1` or `--gpus=1`       |
| `--gpu-bind`          | Defines how tasks should be bound to GPUs (relevant on multi-GPU nodes).                                     | `--gpu-bind=closest`               |

### Loading Modules

It's crucial to load the correct software modules within your batch script to ensure your program runs with the intended environment. Always start with `module purge` to clear any potentially conflicting modules inherited from your login session, then load the specific modules you need.

```bash
module purge                # Clear existing modules
module load python/3.9.7    # Load a specific Python version
module load sas/9.4         # Load SAS
module load R/4.3.2         # Load R
module load matlab/2019a    # Load MATLAB
```

### Executing Your Code

After setting up the environment, include the command(s) needed to run your program.

*   **Python:**
    ```bash
    python your_script.py
    ```
    *   If using a virtual environment:
        ```bash
        source /path/to/your/venv/bin/activate # Activate the environment
        python your_script.py
        deactivate # Optional: Deactivate afterwards
        ```
*   **SAS:**
    ```bash
    sas -nodms your_script.sas
    ```
*   **MATLAB:** (using `-nojvm` can save resources if no Java-based features are needed)
    ```bash
    matlab -nojvm < your_script.m
    ```
*   **R:**
    ```bash
    R CMD BATCH --no-save --no-restore your_script.R output_file.Rout
    ```
    *   The `--no-save` and `--no-restore` flags prevent saving/restoring the R workspace.
    *   Output is typically directed to a `.Rout` file.

## Submitting the Batch Job (`sbatch`)

Once your `.sbatch` script is created, you submit it to the Slurm scheduler using the `sbatch` command from one of the login nodes (`rnd.scrc.nyu.edu` or `vleda.scrc.nyu.edu`).

### Command Syntax

```bash
sbatch [options] your_script.sbatch
```

*   `[options]`: Optional flags that can override directives within the script (e.g., `sbatch --time=1:00:00 your_script.sbatch`).
*   `your_script.sbatch`: The path to your Slurm batch script.

### Example Submissions

```bash
# Submit a simple job
sbatch hello-world.sbatch

# Submit a SAS job
sbatch crosstab.sbatch

# Submit a MATLAB GPU job
sbatch gpu-bench.sbatch

# Submit a Python array job (tasks 1 through 5)
sbatch realVol.sbatch

# Submit an R array job (tasks 5, 10, 15)
sbatch --array=5-15:5 fitspline.sbatch
```

Upon successful submission, Slurm will respond with the assigned job ID:
`Submitted batch job 12345`

## Example Batch Scripts

Here are examples adapted from SCRC tutorials for various software.

### Simple Python Job (`hello-world.sbatch`)

```bash
#!/bin/bash
#
# [hello-world.sbatch]
# Runs a simple Python script printing "Hello World!"
#
#SBATCH --job-name=hello            # Job name
#SBATCH --output=hello_%j.out       # Output file name (%j = job ID)
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
*   **Python Script (`hello-world.py`):**
    ```python
    print("Hello World!")
    ```
*   **Submit:** `sbatch hello-world.sbatch`

### Python with Virtual Environment

```bash
#!/bin/bash
#
# [venv-hello-world.sbatch]
# Runs a Python script inside a specific virtual environment
#
#SBATCH --job-name=venv-hello     # Job name
#SBATCH --output=venv-hello_%j.out # Output file name
#SBATCH --export=ALL             # Export all environment variables
#SBATCH --time=00:01:00          # Set max runtime of job = 1 minute
#SBATCH --mem=4G                 # Request 4 gigabytes of memory
#SBATCH --mail-type=BEGIN,END,FAIL # Send email notifications
#SBATCH --mail-user=you@stern.nyu.edu # email TO
#SBATCH --partition=test       # Specify the partition to submit the job to

module purge                   # Start with a clean environment
module load python/3.9.7       # Load python module (matching venv base)

# Activate the virtual environment (adjust path as needed)
source ~/bigdata/05-virtenvs/py3.9/bin/activate

python hello-world.py          # Run python script within the venv
```
*   **Submit:** `sbatch venv-hello-world.sbatch`

### SAS Job (`crosstab.sbatch`)

```bash
#!/bin/bash
#
# [ crosstab.sbatch ]
# Runs a simple SAS crosstab procedure
#
#SBATCH --job-name=crosstab
#SBATCH --output=crosstab_%j.out # SAS produces .log and .lst files separately
#SBATCH --export=ALL
#SBATCH --time=00:10:00
#SBATCH --mem=512m
#SBATCH --partition=test
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=you@stern.nyu.edu

module purge
module load sas/9.4
sas -nodms crosstab.sas # Runs the SAS script, creates crosstab.log and crosstab.lst
```
*   **SAS Script (`crosstab.sas`):**
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
    ;
    PROC FREQ DATA=Hand;
    TABLES gender*handed;
    RUN;
    ```
*   **Submit:** `sbatch crosstab.sbatch`

### MATLAB GPU Job (`gpu-bench.sbatch`)

```bash
#!/bin/bash
#
# [ gpu-bench.sbatch ]
# Runs a MATLAB script utilizing GPU resources
#
#SBATCH --job-name=gpu-bench
#SBATCH --output=gpu-bench.%j.out
#SBATCH --export=ALL
#SBATCH --gres=gpu:1             # Request 1 GPU
#SBATCH --gpu-bind=closest       # Bind task to the nearest GPU
#SBATCH --time=00:09:00
#SBATCH --mem=32G
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=you@stern.nyu.edu
#SBATCH --partition=gpu          # Specify the GPU partition

echo "Running on node: `hostname`"
echo ""
module purge
module load matlab/2019a
matlab -nojvm < gpu-bench.m # Run the MATLAB script
```
*   **MATLAB Script (`gpu-bench.m`):** (Assumed to exist, performs GPU computation)
*   **Submit:** `sbatch gpu-bench.sbatch`

### Python Array Job (`realVol.sbatch`)

```bash
#!/bin/bash
#
# [ realVol.sbatch ]
# Runs a Python script multiple times with different inputs using job arrays
#
#SBATCH --job-name=realVol                 # Job name
#SBATCH --array=1-5                        # Create 5 tasks with IDs 1, 2, 3, 4, 5
#SBATCH --export=ALL                       # Export env variables
#SBATCH --mem=512m                         # Memory per task
#SBATCH --mail-type=BEGIN,END,FAIL         # Email notifications
#SBATCH --output=realVol.%A-%a.out       # Output file per task (%A=array ID, %a=task ID)
#SBATCH --partition=test                   # Specify the partition
#SBATCH --time=00:10:00                    # Time limit per task

module purge
module load python/3.9.7 # Or the appropriate Python version

# Execute python script, using the task ID to select the input file
# Assumes input files are named series1.txt, series2.txt, ..., series5.txt
INPUT_FILE=$(ls series${SLURM_ARRAY_TASK_ID}*.txt)
echo "Task ID: $SLURM_ARRAY_TASK_ID, Input File: $INPUT_FILE"
python realVol.py < "$INPUT_FILE"
```
*   **Python Script (`realVol.py`):** (Assumed to exist, reads from stdin)
*   **Input Files:** Requires `series1.txt`, `series2.txt`, ..., `series5.txt` in the submission directory.
*   **Submit:** `sbatch realVol.sbatch`

### R Array Job (`fitspline.sbatch`)

```bash
#!/bin/bash
#
# [ fitspline.sbatch ]
# Runs an R script multiple times with different parameters via job arrays
#
#SBATCH --job-name=fitsplineJob
#SBATCH --output=fitsplineJob_%A-%a.Rout # Output file per task
#SBATCH --error=fitsplineJob_%A-%a.err   # Error file per task
#SBATCH --export=ALL
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=you@stern.nyu.edu
#SBATCH --mem=512m
#SBATCH --time=00:10:00
#SBATCH --partition=test
#SBATCH --array=5-15:5 # Tasks with IDs 5, 10, 15

module purge
module load R/4.3.2 # Or appropriate R version

# Run R script in batch mode. The R script uses Sys.getenv("SLURM_ARRAY_TASK_ID")
# to access the task ID. Output goes to fitspline.$SLURM_ARRAY_TASK_ID.Rout
R CMD BATCH --no-save --no-restore fitspline.R fitspline.$SLURM_ARRAY_TASK_ID.Rout
```
*   **R Script (`fitspline.R`):** (Assumed to exist, uses `Sys.getenv("SLURM_ARRAY_TASK_ID")`)
*   **Submit:** `sbatch fitspline.sbatch` (The `--array=5-15:5` is defined in the script, but could also be passed on the command line: `sbatch --array=5-15:5 fitspline.sbatch`)

### R Job (`stock-price.sbatch`)

```bash
#!/bin/bash
#
# [ stock-price.sbatch ]
# Runs an R script for Monte Carlo simulation
#
#SBATCH --job-name=spJob                # Job name
#SBATCH --time=00:10:00               # Wall-clock time limit
#SBATCH --mem=4G                      # Request 4G RAM
#SBATCH --mail-type=END,FAIL           # email user when job ENDs or FAILs
#SBATCH --mail-user=you@stern.nyu.edu  # email TO
#SBATCH --output=stock-price_%j.out    # Standard output file
#SBATCH --partition=test                # Specify partition

module purge
module load R/4.0.2 # Or appropriate R version

# Run the R script, output goes to stock-price.Rout by default
R CMD BATCH stock-price.R
```
*   **R Script (`stock-price.R`):** (Assumed to exist)
*   **Submit:** `sbatch stock-price.sbatch`

## Monitoring Jobs

You can check the status of your submitted jobs using the `squeue` command.

*   **Check your jobs:**
    ```bash
    squeue -u $USER
    ```
*   **Check all jobs on the cluster:**
    ```bash
    squeue
    ```

For more details on monitoring and managing jobs, see the [Common SLURM Commands documentation](link-to-common-slurm-commands). To cancel a job, use `scancel <job_id>`.