# Disk areas in CSC supercomputing environment

**Learning Objectives:**
CSC users working at supercomputing environment have been granted with different disk areas (or directories) to manage their data in supercomputers. It is therefore important to understand your disk areas to manage personal and project-specific data.

Upon completion of this tutorial, you will get familiar with:
- Personal and project-specific disk areas and their quotas in CSC supercomputing environment
- Ideal disk areas for large IO operations

## Identify your personal and project-specific directories in Puhti and Mahti supercomputers

Each user at CSC supercomputer (Puhti or Mahti) owns different disk areas (or directories), each one with a specific purpose. You can get familiar with the directories by issuing the following command in login node:

```bash
csc-workspaces 
```
The resulting output from the above command shows a lot of information about different directories and their current quota. Briefly, these directories are as below:

- User-specific directory: It is your home directory ($HOME) which can contain up to 10 GB of data by default. It is also the default directory when you login to Puhti/Mahti. You can store configuration files and other minor personal data. 

- Project-specific directories: These are *scratch* and *projappl* directories. Each project has 1 TB of scratch disk space by default. This diskspace is temporary space and the files that have not been used for 90 days will be  removed automatically. *Projappl* directory on the other hand can contain up to 50 GB of data and is mainly for storing and sharing compiled applications and libraries etc. with other members of the project. 


## Perform a light-weight pre-porcessing on data files using fast I/O local disks

Once in a while, you come across the cases where you have to handle an uncommonly large number of smaller files that cause heavy IO load on supercomputing environment. In order to facilitate such operations, CSC has provided fast local disk areas in login and compute nodes.

In order to identify such directories in login nodes in Puhti/Mahti, use the following command:

```bash
echo $TMPDIR
```
This local disk area in login nodes is meant for some light-weight preprocessing of data before you start actual analysis on scratch drive. Let's look at the below  toy example where we can download a tar file containing thousands of  small files and then we can  merge all those files into one big file using local storage disks.

1. Download tar file from *allas* object storage

```bash 
cd $TMPDIR           
wget https://a3s.fi/CSC_training/Individual_files.tar.gz
```
2. Unpack the downloaded tar file

```
tar -xavf Individual_files.tar.gz
cd Individual_files
```
3. Merge all those small files into one file and remove all small files

```
find . -name 'individual.fasta*' | xargs cat  >> Merged.fasta
find . -name 'individual.fasta*' | xargs rm
```

However, if you are going to perform heavy-weight computing tasks on those larger number of smaller files, you have to use local storage areas in compute nodes which are accessed either [interactively](https://docs.csc.fi/computing/running/interactive-usage/) or using [batch jobs](https://docs.csc.fi/computing/running/creating-job-scripts-puhti).

In the interactive jobs, use the following command to find out a local storage area in that compute node:

```bash
echo $LOCAL_SCRATCH 
```
When using batch job, use the environment variable $LOCAL_SCRATCH in your [batch job scripts](https://docs.csc.fi/computing/running/creating-job-scripts-puhti/#local-storage) to access the local storage on that node.

## Move your pre-proceessed data to a project-specific scratch area before analysis

Currently, all directories on scratch drive are project-based and one should be aware of a project number to find out actual path on scratch directory. While we can actually find *scratch* directories corresponding to all your project numbers using `csc-workspace`, it may not be immediately obvious to map those project numbers to metadata of your projects. You can instead also use the following command to find more details on your project(s).

```bash
csc-projects
```

Once you know the project number which would be in the form of project_xxx, you can move your pre-processed data (i.e., Merged.fasta file) from earlier step to a project-specific directory on scratch area as below:

```bash
mkdir /scratch/project_xxx/$USER
mv Merged.fasta /scratch/project_xxx/$USER
```
You have now successfully moved your data to scratch area and can start performing actual analysis using batch job scripts which you will learn in-depth in different module.

