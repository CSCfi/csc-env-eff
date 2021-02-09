---
theme: csc-2019
lang: en
---

# Introduction to Singularity containers {.title}

In this section you will learn the basics of Singularity containers
and how to use them in CSC environment.

# Singularity in a nutshell
- Designed for HPC environments
- Containers can be run with user level rights
  - Building new containers requires root access
- Minimal performance overhead
- Supports MPI
  - Requires containers tailored to host system
- Can use host driver stack (Nvidia/cuda)
  - Add option `--nv`
- Can import and run Docker containers

# Running Singularity containers: Basic syntax
- Runs a script specified when container was built
  - `singularity run [run options...] <container>`
- Executes a command in the container
  - `singularity exec [exec options...] <container> <command>`
- Opens a shell in the container
  - `singularity shell [shell options...] <container>`


# File system (1/2)
- Containers have their own, internal file system
- To use host file systemfor input/output, host directories need to be mapped to container directories
`--bind /scratch/project_12345:/data`
host directory /scratch/project_12345 is mapped to
directory /data inside the container
- Target directory inside the container does not need to exist. It is created as
necessary
- More than one directory can be mapped

# File system (2/2)
- Mounting container directories with the same path as host directories allows you to
use same command line as you would without a container – but can be confusing
when troubleshooting
`singularity exec --bind /scratch/project_12345/data:/scratch/project_12345/data myimage.sif myprog --input /scratch/project_12345/data/myfile`
`singularity exec --bind $PWD:$PWD myimage.sif myprog --input myfile`
- Using different name space for the container may be clearer, but you need to remember to use it in commands
`singularity exec --bind /scratch/project_12345/data:/container/data myimage.sif myprog --input /container/data/myfile`
Matter of taste: take you pick

# Using Docker containers with Singularity
- You can build a Singularity container from a Docker container with normal user rights:
`singularity build <image> docker://<address>`
For example:
`singularity build pytorch_19.10-py3.sif docker://nvcr.io/nvidia/pytorch:19.10-py3`

# Singularity containers as installation method
- Singularity is a good option in cases where installation is
otherwise problematic:
  - Complex installations with many dependencies
  - Obsolete dependencies incompatible with general environment
    - Still needs to be kernel compatible
- Should be considered even when other methods exist

# Just a random example (FASTX-toolkit)
Installation type Size on disc Number of files
Native 1,9 MB 47
Conda 1,1 GB 27464
Singularity 339 MB 1
- Containers are not the solution for everything, but they do have their uses…

# Building a new Singularity container
Typical steps
- Build a basic container in sandbox mode (`--sandbox`)
  - Uses a folder structure instead of an image file
  - Requires root access!
- Open a shell in the container and install software
  - Depending on base image system, package managers can be used to install libraries etc (apt install, yum install etc)
  - Installation as per software developer instructions
- Build a production image from the sandbox
- (optional) Make a definition file and build a productio image from it

Requires root access: Can not be done directly in e.g. Puhti