--
theme: csc-2019
lang: en
--

# The batch job system in CSC HPC environment {.title}

- CSC uses a batch job system (SLURM) to execute computing tasks in our supercomputers
- SLURM is used to control how the overall computing resources are shared among all projects in an efficient and fair way
- SLURM is used to control how a single job gets resources like:
    - computing time
    - number of cores
    - amount of memory
    - other resources like gpu, local disk, etc.
- in order to utilize the resources in an efficient way, it is important to try to estimate the requests as accurately as possible
- by avoiding excessive "just-in-case" requests, the single job will start earlier


