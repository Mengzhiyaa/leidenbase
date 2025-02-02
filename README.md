# Leidenbase

An R to C interface that runs the Leiden community detection algorithm to find a basic partition. It is the equivalent of the find_partition() function given in the Leidenalg distribution file *leiden/src/functions.py* and includes the underlying Leidenalg C++ source code files of Leidenalg release version 0.7.0. The Leiden algorithm is described in

> *From Louvain to Leiden: guaranteeing well-connected communities.*  
   V. A. Traag, L. Waltman, and N. J. van Eck,  
   Scientific Reports (2019), DOI: 10.1038/s41598-019-41695-z  


## Getting Started

### Prerequisites

This distribution requires software development tools including C, C++, and FORTRAN compilers. These compilers are provided often with your operating system or as packages. The R Project distributes C, C++, and FORTRAN development tools for [MacOS](https://cran.r-project.org/bin/macosx/tools/) and for [Windows](https://cran.r-project.org/bin/windows/Rtools/).

### Installing
  
Use the devtools::install_github() command

```
devtools::install_github('cole-trapnell-lab/leidenbase')
```

### Tested conditions

#### Linux Debian 10 Buster

R distribution: Debian packages  
C/C++ compilers: Debian distribution packages  
FORTRAN compiler: Debian distribution packages  

#### MacOS Monterey on Apple ARM CPU

R distribution: https://cran.r-project.org/bin/macosx/big-sur-arm64/base/R-4.1.2-arm64.pkg
C/C++ compilers: Xcode 13.2.1
FORTRAN compiler: gfortran 11.0  https://mac.r-project.org/libs-arm64/gfortran-f51f1da0-darwin20.0-arm64.tar.gz
Note: after downloading gfortran, use the command
        sudo tar fxz gfortran-f51f1da0-darwin20.0-arm64.tar.gz -C /
      to install it to /opt.
For more information, see https://mac.r-project.org/tools/

#### MacOS Monterey on Intel CPU

R distribution: CRAN package from https://cran.r-project.org/bin/macosx/R-4.0.2.pkg  
C/C++ compilers: Apple Xcode 13.2.1
FORTRAN compiler: gfortran 8.2 from https://mac.r-project.org/tools/gfortran-8.2-Mojave.dmg

#### MicroSoft Windows 10

R distribution: CRAN package from https://cran.r-project.org/bin/windows/base/R-4.1.2-win.exe
C/C++ compilers: CRAN Rtools40 from https://cran.r-project.org/bin/windows/Rtools/rtools40-x86_64.exe  
FORTRAN compiler: CRAN Rtools40 from https://cran.r-project.org/bin/windows/Rtools/rtools40-x86_64.exe  
For more information, see https://cran.r-project.org/bin/windows/Rtools/rtools40.html

#### Suggestions

Try to use compatible C/C++ and FORTRAN compilers. For example, if you install R using a CRAN package, try to use the R compiler tools, and if you use *brew* on MacOS to install R, try to use brew-installed compilers.

### Leidenbase functions

The R wrapper for running the Leiden algorithm find partition function is  

    leiden_find_partition <- function( igraph,
                               partition_type = c( 'CPMVertexPartition',
                                                   'ModularityVertexPartition',
                                                   'RBConfigurationVertexPartition',
                                                   'RBERVertexPartition',
                                                   'SignificanceVertexPartition',
                                                   'SurpriseVertexPartition' ),
                               initial_membership = NULL,
                               edge_weights = NULL,
                               node_sizes = NULL,
                               seed = NULL,
                               resolution_parameter = 0.1,
                               num_iter = 2 )

The C++ wrapper for running the Leiden algorithm find partition function
is  

    int leidenFindPartition( igraph_t *pigraph,
                             std::string const partitionType,
                             std::vector < size_t > const *pinitialMembership,
                             std::vector < double > const *pedgeWeights,
                             std::vector < size_t > const *pnodeSizes,
                             size_t seed,
                             double resolutionParameter,
                             int numIter,
                             std::vector < size_t > *pmembership,
                             std::vector < double > *pweightInCommunity,
                             std::vector < double > *pweightFromCommunity,
                             std::vector < double > *pweightToCommunity,
                             double *pweightTotal,
                             double *pquality,
                             double *pmodularity,
                             double *psignificance,
                             int *pstatus )`

## Issues with leidenbase

For problems with leidenbase, please consider submitting an issue report to the [leidenbase issue page](https://github.com/cole-trapnell-lab/leidenbase/issues) on github.com. We ask that you include some details that may help us with identifying the source of the problem. For problems with installing leidenbase, please see [reporting install issues](src/doc/issue_report_install.md)  and for problems with running leidenbase, please see [reporting run issues](src/doc/issue_report_run.md).

## Licenses

Leidenbase and leidenalg are distributed under the GPL-3+ license. The C igraph library is distributed under the GPL-2+ license. Licenses for software libraries redistributed with the C igraph library are in LICENSE files in the corresponding sub-directories.

## Acknowledgements

We express our gratitude to the authors of the igraph and Leidenalg packages for designing, writing, and making them freely available as source code.



