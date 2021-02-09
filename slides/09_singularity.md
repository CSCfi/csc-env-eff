---
theme: csc-2019
lang: en
---

# Introduction to Singularity containers {.title}

In this section you will learn the basics of Singularity containers
and how to use them in CSC environment.

# Containers
- Containers are a way to package software with its dependencies (libraries,etc)
- Popular container engines include Docker, Singularity, Shifter
- Singularity is the most popular in HPC environments

# Container benefits: Ease of installation
- Containers are becoming a popular way to distribute software
  - Single command installation
  - All dependencies included, so more portable
- When building from scratch, root access and package managers (yum, apt, etc) are available
 
 # Container benefits: Environment isolation
 - Containers use host system kernel, but can have it's own Bins/Libs layer
   - Can effectively be different Linux distribution that host
   - Can solve some incompatibilities
  - Less likely to be effected by changes in the host system
  
 # Container benefits: Enviroment reproducibility
 - Analysis environment can be saved as a whole
   - Especially usefull with e.g. Python, where updating underlaying libraries (Numpy etc) can lead to different performance  
 - Sharing with collaborators easy (single file)

# Singularity in a nutshell
- Designed for HPC environments
- Containers can be run with user level rights
  - But: Building new containers requires root access
- Minimal performance overhead
- Supports MPI
  - Requires containers tailored to host system
- Can use host driver stack (Nvidia/cuda)
  - Add option `--nv`
- Can import and run Docker containers

# Singularity on CSC servers
- Singularity installed only in compute nodes
- Singularity jobs need to run as batch jobs or with sinteractive
- No need to load a module
- Users can run their own containers
- Some CSC software installations provided as containers
- See software pages for details

# Running Singularity containers: Basic syntax
- Run the default action (runscript) of the container
  - Defined when the container is built
  - `singularity run [run options...] <container>`
- Execute a command in the container
  - `singularity exec [exec options...] <container> <command>`
- Open a shell in the container
  - `singularity shell [shell options...] <container>`

# File system (1/2)
- Containers have their own, internal file system
- To access host directories, they  need to be mapped to container directories
`--bind /scratch/project_12345:/data`
host directory `/scratch/project_12345` is mapped to
directory `/data` inside the container
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

# singularity_wrapper
- Running containers with singularity_wrapper takes care of most common `--bind` commands
  - `singularity_wrapper exec image.sif myprog <options>`
- If environment variable `$SING_IMAGE` is set with the path to the image, even image can be omitted
  - `singularity_wrapper exec myprog <options>`

# Using Docker containers with Singularity
- You can build a Singularity container from a Docker container with normal user rights:
  - `singularity build <image> docker://<address>`
- For example:
  - `singularity build pytorch_19.10-py3.sif docker://nvcr.io/nvidia/pytorch:19.10-py3`
- Documentation in Docs:
  - https://docs.csc.fi/computing/containers/run-existing/

# Singularity containers as installation method
- Singularity is a good option in cases where installation is
otherwise problematic:
  - Complex installations with many dependencies
  - Obsolete dependencies incompatible with general environment
    - Still needs to be kernel compatible
- Should be considered even when other methods exist

# Just a random example (FASTX-toolkit)
Installation type | Size on disc | Number of files
Native |1,9 MB| 47
Conda |1,1 GB |27464
Singularity |339 MB |1
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