# Slurm Array Jobs

This page explains how to use Slurm array jobs on the SCRC cluster. Array jobs provide an efficient mechanism for submitting and managing collections of similar jobs quickly and easily. They are particularly useful when you need to run the same program multiple times with different input parameters or datasets.

## Overview

Instead of writing multiple individual job scripts or submitting the same script repeatedly, you can use a single job script with the `--array` directive. Slurm then creates multiple "tasks" within a single job allocation, each with its own unique task ID. This task ID can be used within your script to vary parameters, input files, or output filenames.

Benefits of using array jobs include:

*   **Efficiency:** Submit and manage many tasks with a single command.
*   **Scalability:** Easily scale up the number of tasks.
*   **Resource Management:** Each task can request specific resources, though often they share the same resource profile.

## Submitting Array Jobs

To submit an array job, use the `#SBATCH --array` directive in your Slurm script or the `--array` option with the `sbatch` command.

### The `--array` Directive

The `--array` directive specifies the range and stepping of the task IDs.

**Syntax:**

```bash
#SBATCH --array=<indices>
```

*   `<indices>` can be specified in several ways:
    *   A simple range: `1-5` (Tasks 1, 2, 3, 4, 5)
    *   Specific indices: `0,1,5,10` (Tasks 0, 1, 5, 10)
    *   A range with a step: `1-10:2` (Tasks 1, 3, 5, 7, 9)
    *   A range with step and limit on concurrent tasks: `1-100%10` (Tasks 1 to 100, but only 10 run concurrently)

**Example in `sbatch` script:**

```bash
#SBATCH --array=1-5  # Creates 5 tasks with IDs 1, 2, 3, 4, 5
```

**Example with `sbatch` command:**

You can also specify the array range directly when submitting the job, which overrides any `#SBATCH --array` directive in the script.

```bash
sbatch --array=5-15:5 my_script.sbatch # Creates 3 tasks with IDs 5, 10, 15
```

## Using the Task ID

Slurm sets the environment variable `SLURM_ARRAY_TASK_ID` for each task within the array job. You can use this variable in your job script to control the behavior of each task. Common uses include:

*   Selecting different input files based on the task ID.
*   Passing different parameters to your program.
*   Creating unique output directories or filenames for each task.

**Example Usage in Script:**

```bash
#!/bin/bash
#SBATCH --array=1-3
#SBATCH --output=task_%a.out # Use %a for task ID in output name

INPUT_FILE="data_part_${SLURM_ARRAY_TASK_ID}.txt"
OUTPUT_FILE="result_${SLURM_ARRAY_TASK_ID}.log"

echo "Running task ${SLURM_ARRAY_TASK_ID}"
echo "Input file: ${INPUT_FILE}"
echo "Output file: ${OUTPUT_FILE}"

# Your command using the task-specific variables
# ./my_program --input ${INPUT_FILE} --output ${OUTPUT_FILE}
```

## Managing Output Files

It's crucial to manage output files so that tasks don't overwrite each other's results. Slurm provides placeholders for job and task IDs in the `#SBATCH --output` and `#SBATCH --error` directives:

*   `%A`: Replaced by the main Job ID.
*   `%a`: Replaced by the Array Task ID.

**Example:**

```bash
#SBATCH --job-name=myArrayJob
#SBATCH --array=1-10
#SBATCH --output=myArrayJob.%A-%a.out  # Creates files like myArrayJob.12345-1.out, myArrayJob.12345-2.out, etc.
#SBATCH --error=myArrayJob.%A-%a.err
```

## Examples

Run `getSlurmExamples` at the command line of `rnd` or `vleda` to have all the tutorials copied to your home directory.

### Python Example: Real Volatility Calculation

This example runs a Python script (`realVol.py`) five times, each time calculating the real volatility for a different input price series file (`series1.txt` to `series5.txt`).

**Python Script (`realVol.py`)**

This script reads price data from standard input and calculates realized volatility.

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

**Slurm Script (`realVol.sbatch`)**

This script uses `#SBATCH --array=1-5` to create 5 tasks. The `${SLURM_ARRAY_TASK_ID}` variable is used to select the correct input file (`series<ID>.txt`) for each task via input redirection. Output files are named using the Job ID (`%A`) and Task ID (`%a`).

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

**Submission Command:**

```bash
sbatch realVol.sbatch
```

### R Example: Fitspline Model

This example runs an R script (`fitspline.R`) multiple times. The script fits a cubic smoothing spline to simulated data. The amount of noise added to the data depends on the Slurm Task ID, and the output plot filename also incorporates the task ID.

**R Script (`fitspline.R`)**

This script retrieves the task ID using `Sys.getenv("SLURM_ARRAY_TASK_ID")`, uses it to calculate the noise variance (`v`), and generates a task-specific output filename (`result_<ID>.ps`).

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
tid <- as.integer(Sys.getenv("SLURM_ARRAY_TASK_ID")) # Get Task ID
v <- tid / 100 # Use Task ID to vary noise
noise <- rnorm(n, 0, v)

# Simulated observed values (model value + noise)
y <- mval + noise

# Fit a cubic smoothing spline to the data
fit <- smooth.spline(x, y, cv = FALSE, all.knots = TRUE)

# Create a graph that shows the data, the smoothing spline,
# and the original model
r <- paste("result_", tid, ".ps", sep = "") # Use Task ID in filename
postscript(r, height = 8, width = 10, horizo = FALSE)

# Plot data points
plot(x, y, xlab = "x", ylab = "y", cex = 0.5)

# Plot original model values without noise
lines(x, mval, lty = 2)

# Plot smooth spline fit
lines(fit$x, fit$y)

# Save the graph to a PS file
graphics.off()
```

**Slurm Script (`fitspline.sbatch`)**

This script loads the necessary R module and executes the R script using `R CMD BATCH`. The output R log file is named using the `${SLURM_ARRAY_TASK_ID}` variable. Note the comment indicating how to submit this script as an array job with specific task IDs.

```bash
#!/bin/bash
#
# [ fitspline.sbatch ]
#
# This script demonstrates how to run an R job, specifically,
# how to fit a smooth spline model. It uses a range of SLURM_ARRAY_TASK_ID's
# as a noise parameter for the model.
# --------------------------------------------------------------------
# Submit this job via 'sbatch' which accepts these command line options:
#SBATCH --job-name=fitsplineJob        # Define the name of the current job.
#SBATCH --output=fitsplineJob.Rout     # Define the stdout (the terminal output) file name. (Note: Overridden by R CMD BATCH output redirection below)
#SBATCH --error=fitsplineJob.err      # Define the stderr (the terminal error output) file name.
#SBATCH --export=ALL                  # Export ALL environment variables.
#SBATCH --mail-type=END,FAIL           # Send email when the job ENDs or FAILs.
#SBATCH --mail-user=your-stern-netid@stern.nyu.edu  # Specify your Stern email address.
#SBATCH --mem=512m                    # Specifies the maximum memory per task.
#SBATCH --time=00:10:00               # The wall-clock time limit per task.
#SBATCH --partition=test               # Specify the partition.
# --------------------------------------------------------------------
# How to submit an array job to Stern Slurm cluster.
# Pass array variable values 5, 10, 15 to the R script.
#
# sbatch --array=5-15:5 fitspline.sbatch
# --------------------------------------------------------------------

# Select stat package and version to use
module purge
module load R/4.3.2

# Run R script, directing R output to a task-specific file
R CMD BATCH --no-save --no-restore fitspline.R fitspline.$SLURM_ARRAY_TASK_ID.Rout
```

**Submission Command:**

This command submits the script and creates tasks with IDs 5, 10, and 15.

```bash
sbatch --array=5-15:5 fitspline.sbatch
```

## Notes and Considerations

*   **Resource Allocation:** Resources specified with `#SBATCH` directives (like `--mem`, `--time`, `--cpus-per-task`) apply to *each task* in the array job individually.
*   **Job Monitoring:** You can monitor array jobs using `squeue`. Tasks will often appear with an underscore and the task ID appended to the job ID (e.g., `12345_1`, `12345_2`).
*   **Canceling Tasks:** You can cancel the entire array job (`scancel <JobID>`) or individual tasks (`scancel <JobID>_<TaskID>`).