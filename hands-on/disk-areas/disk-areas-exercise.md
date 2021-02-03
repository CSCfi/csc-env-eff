---
title: Disk areas in CSC supercomputing environment
---

#### Imagine that you have a data file and software binary (e.g., data.txt and softwareA_binary) on your Puhti home directory and  also have a shared project (e.g., project_1234) on Puhti and Mahti. How would you safely share your files to other project members on the same supercomputer (i.e., on Puhti) as well as on Mahti (i.e, another supercomputer at CSC)?

*Background*: This exercise is aimed at familiarising yourself with main disc areas in Puhti and Mahti supercomputers. Data files needed for computational analysis should be stored and shared in *scratch* directories and any software compilations and binaries should be shared in *proappl* directory. In order to find actual directories use commands such as `csc-workspaces` and `csc-projects`. Data transfer between two supercomputers can be done with many tools including `rsync`. In this example try to avoid using *allas* for data transfer between the supercomupters. 

***Solution:***

1. First login to Puhti supecomputer using *ssh* command as below:

```bash
ssh <username>@puhti.csc.fi
```
Authenticate using the password associated with CSC user account. Once your login to Puhti is successful, Linux terminal will be opened for command-line interaction in your home directory. Let's assume that file *data.txt* is intended for computational use and *softwareA_binary* is a software tool needed for analysis. As you know the project name, you can share file *data.txt* in scratch folder and *softwareA_binary* file in projapple directory.

2. Share your *softwareA_binary* file in *projapple* directory

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

#### What would be the ideal disk area to perform the following task that require high I/O operations ?
*The task description*: Analysis is based on a big tar file containing around 52000 small files, each one comprises one or more nucleotide sequences. Unpack the tar file and convert the nucleic acids sequences in each file to corresponding protein sequences using *transeq* software. Once analysis is finished, pack all files into a tar file again.

*Background*: The “normal” Lustre based project-specific directories, *scratch* and *projappl*, can store large amounts of data and make it accessible to all the nodes of Puhti. However, these directories are not good for managing a large number of files.  If you need to work with a huge number of smaller files, you should consider using the NVME based local temporary scratch directories, either through normal or interactive batch jobs.

***hints:***
- Use interactive job option. One can launch an interactive session using the following command:
```text
sinteractive -c 2 -m 4G -d 250 #  grants you a compute node with 2 cores, 4 GB of memory and 250 GB of fast temporary scratch disk.
```
- Move to fast local scratch area (i.e, cd $LOCAL_SCRATCH) and unpack tar file to the local scratch directory.
- Run the analysis using the command *transeq* to translate all the fasta files (i.e., transeq necleicacid_input.file  protein_output.file)
- After analysis on each file, create again a tar file with protein sequences

***Solution:***

```
# launch an interactive session with required resources
sinteractive -c 2 -m 4G -d 250

# chnage working directory to fast local scratch directory
cd $LOCAL_SCRATCH

# download tar file and unpack it (fix this link)

wget https://a3s.fi/big_data.tar
tar big_data.tar ./

# perform actual analysis

for ffile in $(find ./ | grep fasta$ )
do
     transeq $ffile ${ffile}.pep
done 

# pack all the resulting files
tar cvf big_data.pep.tar ./

```

Below is the execution time comparison for running the three steps above in LOCAL_SCRATCH and in normal scratch.  

|                               | LOCAL_SCRATCH |         scratch|
|-------------------------------|---------------|----------------|    
|Step 1. Opening tar file       | 2m 8s         |   4m 12s       |
|Step 2. Analysis               | 9m 42s        |   21m 58s      |
|Step 3. Creating new tar file  | 2m 25s        |   42m 21s      | 
|Total                          | 14m 15s       |   1h 8m 31s    |
              
 
#### How do you make use of local scratch drive on compute node for faster computational tasks? Convert the following normal batch job into the one that uses local scratch drive?

Below is a normal batch job that pulls docker image from DockerHub and converts into a singularity one that is compatible with working in HPC environments such as CSC Puhti and Mahti supercomputers. During the conversion process, several layers are retrieved, cached and then converted into a singularity file (.sif format)

```bash
#!/bin/bash
#SBATCH --time=01:00:00
#SBATCH --partition=small
#SBATCH --account=project_xxx

export SINGULARITY_TMPDIR=/scratch/project_xxx/$USER
export SINGULARITY_CACHEDIR=/scratch/project_xxx/$USER
singularity pull --name trinity.simg  docker://trinityrnaseq/trinityrnaseq
```

***Hints***:
- Request NVME fast local storage using the --gres flag  in sbatch directive as below:

```
#SBATCH --gres=nvme:<local_storage_space_per_node>  # e.g., to claim 200 GB of storage, use option --gres=nvme:200 

```
- Use environment variable $LOCAL_SCRATCH to access the local storage on each node.

- Please move any data to shared area once  the job is finished


***Solution:***

```bash
#!/bin/bash
#SBATCH --time=01:00:00
#SBATCH --partition=small
#SBATCH --account=project_xxx
#SBATCH  --gres=nvme:100

export SINGULARITY_TMPDIR=$LOCAL_SCRATCH
export SINGULARITY_CACHEDIR=$LOCAL_SCRATCH
unset XDG_RUNTIME_DIR

cd $LOCAL_SCRATCH
#pwd
#df -lh
singularity pull --name trinity.simg docker://trinityrnaseq/trinityrnaseq
mv trinity.simg /scratch/project_xxx/$USER/                                                            
```

Below is the comparison of execution time for running the same job in LOCAL_SCRATCH *vs.* normal scratch.  

|                               | LOCAL_SCRATCH |         scratch|
|-------------------------------|---------------|----------------|    
|Wall-clock time     |22m 06s      |  50m 06s        |
