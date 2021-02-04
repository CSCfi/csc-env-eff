# Singularity tutorial

In this tutorial we get familiar with the basic usage of Singularity containers. 

To run these exercises in Puhti, use **sinteractive**.
```text
sinteractive -i
```
## Getting started

To get started, download a test container image from allas.

```text
wget ADDRESS
ls -lh tutorial.sif
```
As you can see, the container is a single file. In this case the container is very 
bare-bones and thus quite small, about 68 MB. 

## Basic usage
There ar three basic ways to run software in Singularity containers:

### 1. Singularity exec
To execute a command inside the container the command is **singularity exec**.

```text
singularity exec tutorial.sif hello_world
```
Compare the outputs of the following commands:
```text
cat /etc/*release
singularity exec tutorial.sif cat /etc/*release
```
The first command is run in the host. The second command is run inside the container.

As you can see, our container is based on Ubuntu 18.04. The host and the container use the same kernel, but 
the rest of the system can vary. That means a container can be based on a different Linux distro than the host 
(as long as they the are kernel compatible), but can't run a totally differen OS like Windows.

### 2. Singularity run
When containers are created, a standard action, called teh *runscript* is defined. Depending
on the container it may simply print out a message or it may launch a program inside the container.
If you are using a container created by somebody else, you will need to check the documentation provded
by the creator for details.

In our test container it prints out a simple message:
```text
singularity run tutorial.sif
```
If the container image has execute rights, you can also run it directly:
```text
./tutorial.sif
```
You can check the actual script with command:
```text
singularity inspect --runscript tutorial.sif
```

### 3. Singularity shell
It is also possible to open a shell inside the container. 
```text
singularity shell tutorial.sif
```
You can see the comamnd prompt change. You can now run any software inside the container interactively:
```text
hello_world
```
You can exit the container with:
```text
exit
```

## Using files
Singularity containers have their own internal file system that is separate from the host file system. 
The internal file system is always read-only when the container is run with normal user rights.

In most real-world use cases you probably want to read input files from the host file system or you wish 
to save something into a file. To do this you must bind a writable folder on host file system to teh internal
file system. 

This is done with command line argument **--bind**. Basic syntax:
```text
--bind /path/in/host:/path/inside/container
```
The bind path does not need to exist inside the container. It is created if necessary. More that one 
bind pair can be specified. The option is available for the run methods described above.

In this example we 
xxMISSINGxx

If you use wrapper script **singularity_wrapper**, it will take care of the binds for most common use cases. 
```text
singularity_wrapper exec tutorial.sif <YO>
```
If environment variable *$SING_IMAGE* is set, you don't even need to provide path to the image file.
```text
export SING_IMAGE=$PWD/tutorial.sif
singularity_wrapper exec <YO>
```
Since some modules set *$SING_IMAGE* when loaded it is a good idea to start with **module purge** if you plan
to use it to make sure correct image is used.

## Environment variables
Some software may reguire some environment variables to be set, e.g. to point to some reference data or 
a configuration file.

Most environment variables set on the host are inherited by the container.

To set an environment variable specifically inside the container, you can set an environment variable 
*$SINGULARITYENV_xxx* on the host before invoking the container.

```text
export TEST1="value1"
export SINGULARITYENV_TEST2="value"
```
Compare the outputs of:

```text
env |grep TEST
singularity exec tutorial.sif env |grep TEST
```

## Exploring containers
XXMISSINGXX

## How to get containers
Building containers from scratch requires root access, so it can not be done on Puhti. 
Instead, you will have to import a ready image file.

There are various option to do this.

### Pull an existing Singularity container from a repository
Use **singularity pull**:
```text
singularity pull shub://vsoch/hello-world
```

### Convert an existing Docker container to Singularity
Use **singularity build**:
```text
singularity build pytorch_20.03-py3.sif docker://nvcr.io/nvidia/pytorch:20.03-py3
```
You can find more detailed instructions for this in Doc CSC: [Running existing containers](ADD LINK)

### Build the image on another system and transfer the image file to Puhti
To do this you will need an access to system where you have root access and that has Singularity installed.

Singularity version does not need to be exactly same, but it should be same major varsion e.g. (3.x as oppsed to 2.x).

You can check the current version on Puhti with:
```text
singularity --version
```
After creating an image file, you can transfer it to Puhti to use.

## More information

This tutorial is meant as brief introduction to get you started.

When searching the internet for instruction, pay attention that the instructions are
for the same version of Singularity that you are using. There has been some command syntax changes
etc. between the versions, so older instructions may not work with copy-paste.

For authoritative instructions see [Singularity documentation](https://sylabs.io/docs/).



```text
```