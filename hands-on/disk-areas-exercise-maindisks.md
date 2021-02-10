# Where to put files in CSC environment?

## Binary and data files to share

Imagine that you have a data file and software binary (e.g., data.txt and softwareA_binary) on your Puhti home directory and  also have a shared project (e.g., project_1234) on Puhti and Mahti. How would you safely share your files to other project members on the same supercomputer (i.e., on Puhti) as well as on Mahti (i.e, another supercomputer at CSC)?

###  Background

This exercise is aimed at familiarising yourself with main disc areas in Puhti and Mahti supercomputers. Data files needed for computational analysis should be stored and shared in *scratch* directories and any software compilations and binaries should be shared in *proappl* directory. In order to find actual directories use commands such as `csc-workspaces` and `csc-projects`. Data transfer between two supercomputers can be done with many tools including `rsync`. In this example try to avoid using *allas* for data transfer between the supercomupters. 

### Solution

1. First login to Puhti supecomputer using *ssh* command as below:

```bash
ssh <username>@puhti.csc.fi
```
Authenticate using the password associated with CSC user account. Once your login to Puhti is successful, Linux terminal will be opened for command-line interaction in your home directory. Let's assume that file *data.txt* is intended for computational use and *softwareA_binary* is a software tool needed for analysis. As you know the project name, you can share file *data.txt* in scratch folder and *softwareA_binary* file in projapple directory.

2. Share your *softwareA_binary* file in *projappl* directory

```bash
cp softwareA_binary  /projapple/project_1234
````

3. Share *data.txt* file in *scratch* directory
```bash
cp data.txt /scratch/project_1234
```
All new files and directories are also fully accessible for other group members (including read, write and execution permissions). If you want to restrict access from your group members, you can reset the permissions with *chmod* command.

Set read-only permissions for your group members for the file *data.txt*:

```bash
chmod -R g-w data.txt
```
4. sharing files in Mahti supercomputer

you can copy *data.txt* file on puhti to *scratch* drive on Mahti as below:

```bash
rsync -P data.txt <username>@mahti.csc.fi:/scratch/project_1234
```
you can copy *sofwtareA_binary* file on puhti to *projapple* directory on Mahti as below:

```bash
rsync -P sofwtareA_binary <username>@mahti.csc.fi:/scratch/project_1234
```

