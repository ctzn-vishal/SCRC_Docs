```markdown
---
title: "Installing Local R Packages"
category: "software-and-applications"
description: "Instructions for installing R packages into your user library from CRAN, Bioconductor, and GitHub."
---

# Installing Local R Packages

This document provides instructions for installing R packages into your personal library on the SCRC environment. R packages extend the capabilities of R by adding new functions or improving existing ones. Packages can be installed from various repositories.

**Prerequisite:** Before installing packages, ensure you are running an interactive session on a compute node with R loaded (e.g., via RStudio). For instructions, see [Getting Started with Slurm Interactive Jobs](link-to-getting-started).

## Package Repositories

Repositories are central locations where R packages are stored for download and installation. The most common repositories include:

*   **CRAN (The Comprehensive R Archive Network):** The official repository maintained by the R community. Contains a vast collection of stable R packages.
*   **Bioconductor:** A specialized repository focusing on open-source software for bioinformatics and computational biology.
*   **GitHub:** A popular platform for hosting open-source projects, including many R packages under active development.

## Installing Packages

Package installation is typically done from within an R session (e.g., in the RStudio Console).

### Installing from CRAN

Packages available on CRAN can be installed directly using the `install.packages()` function.

*   **Install a single package:**
    Replace `"package_name"` with the name of the package you want to install.

    ```R
    install.packages("package_name")
    ```

    For example, to install the `vioplot` package:

    ```R
    install.packages("vioplot")
    ```

*   **Install multiple packages:**
    Provide a character vector `c()` containing the names of the packages.

    ```R
    install.packages(c("vioplot", "MASS"))
    ```

*   **Specify a CRAN mirror:**
    You can choose a specific mirror for downloading using the `repo` argument. A list of mirrors is available [here](https://cran.r-project.org/mirrors.html).

    ```R
    install.packages("vioplot", repo = "https://lib.ugent.be/CRAN/")
    ```

### Installing Bioconductor Packages

Bioconductor packages require the `BiocManager` package. Detailed instructions are available on the [Bioconductor installation page](https://www.bioconductor.org/install/).

1.  **Install BiocManager:**
    If you don't have `BiocManager` installed, install it from CRAN first:

    ```R
    install.packages("BiocManager")
    ```

2.  **Find available packages:**
    You can browse available Bioconductor packages [online](https://www.bioconductor.org/packages/release/BiocViews.html#___Software) or check programmatically within R:

    ```R
    BiocManager::available()
    ```

3.  **Install Bioconductor packages:**
    Use the `BiocManager::install()` function. You can install single or multiple packages.

    ```R
    BiocManager::install(c("GenomicFeatures", "AnnotationDbi"))
    ```

### Installing GitHub (and other) Packages via `devtools`

The `devtools` package provides convenient functions to install packages directly from repositories like GitHub, Bitbucket, or even local files.

1.  **Install devtools:**
    Install `devtools` from CRAN if you haven't already:

    ```R
    install.packages("devtools")
    ```

2.  **Use `devtools::install_*` functions:**
    `devtools` offers various functions for installation (see `devtools` [documentation](https://cran.r-project.org/web/packages/devtools/devtools.pdf) for details):
    *   `install_bioc()`: from Bioconductor
    *   `install_bitbucket()`: from Bitbucket
    *   `install_cran()`: from CRAN
    *   `install_git()`: from a git repository
    *   `install_github()`: from GitHub
    *   `install_local()`: from a local file
    *   `install_svn()`: from a SVN repository
    *   `install_url()`: from a URL
    *   `install_version()`: a specific version from CRAN

3.  **Example: Install from GitHub:**
    To install the `babynames` package from the `hadley` repository on GitHub:

    ```R
    devtools::install_github("hadley/babynames")
    ```

## Removing Packages

To remove an installed package, use the `remove.packages()` function:

```R
remove.packages("package_name")
```

For example, to remove the `vioplot` package:

```R
remove.packages("vioplot")
```

## Updating Packages

You can check for outdated packages and update them.

*   **Check for outdated packages:**
    The `old.packages()` function lists installed packages for which newer versions are available on the repositories.

    ```R
    old.packages()
    ```

*   **Update a specific package:**
    Simply reinstall the package using `install.packages()`. This will fetch the latest available version from CRAN.

    ```R
    install.packages("vioplot")
    ```

*   **Update all packages:**
    Use `old.packages()` to identify outdated packages. (Note: The standard function to update all packages is `update.packages()`. The provided source material lists `old.packages()` for this purpose, which is likely an error in the source but is replicated here as per instructions.)

    ```R
    old.packages()
    ```

## Using GUI to Install Packages

RStudio provides a graphical user interface (GUI) for package management.

1.  Go to the menu: `Tools > Install Packages...`
2.  A dialog window will appear where you can type the names of the packages you want to install.
3.  Select the repository (e.g., CRAN) and click "Install".

While the GUI is available, using the console commands (`install.packages()`, `BiocManager::install()`, etc.) is often faster and more reproducible.
```