# Using greasy for handling multiple Gaussian jobs in Puhti

This tutorial requires that you have an [user account at CSC](https://docs.csc.fi/accounts/how-to-create-new-user-account/)
and that your account belongs to a project [that has access to Puhti service](https://docs.csc.fi/accounts/how-to-add-service-access-for-project/). You should also belong to the [Gaussian users group](https://docs.csc.fi/apps/gaussian/)

This example describes a single task where there are multiple gaussian jobs, all defined in separate com-files,
that are kept in a separate subfolder com/ .  

# Setting up the job

First we make a script that will create a tasklist that can be processed by greasy.

```bash
#!/bin/bash
#
submission_dir=$PWD        # Directory from where the job is submitted    
com_dir=${submission_dir}/com    # All com files in a separate subfolder 
# the number of tasks equals the numer of com-files
Ntasks=$(ls -l ${com_dir}/*.com|wc -l)
# set the number of threads per task 
Ncores=4
rm -f greasy_"${Ntasks}".tasklist
for f in ${com_dir}/*.com;
do
input_base=`basename ${f%%.*}`
sed -i '/nproc/Id' $f
sed -i "1 i\%NProcShared=${Ncores}" ${f}
mkdir -p ${input_base}
echo "g16 < ${f} > ${input_base}/${input_base}.log" >> greasy_"${Ntasks}".tasklist
done
```

After executing the script you should have a tasklist file that contains  
the executing commands for all com-files on separate lines, like  

```bash
...
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_10.com > benzene_10/benzene_10.log
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_11.com > benzene_11/benzene_11.log
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_12.com > benzene_12/benzene_12.log
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_13.com > benzene_13/benzene_13.log
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_14.com > benzene_14/benzene_14.log
...
```
```bash

# Run the tasklist

[runeberg@puhti-login2 restart]$ module load greasy
[runeberg@puhti-login2 restart]$ sbatch-greasy --cores 4 --time 02:00 --nodes 1 --account project_2001199  
greasy_100.tasklist
Task list "greasy_100.tasklist" includes 100 tasks.
The first two rows of the task list are:
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_100.com > 
benzene_100/benzene_100.log
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_10.com > 
benzene_10/benzene_10.log
-------------------------------------------------------------------------
Submitting GREASY job consisting of 100 tasks to 1 nodes.
The job will run 10 tasks at the time each using 4 cores.
The maximum runtime reseved to process all the tasks is 0 h 27 m.
Job submitted with ID 4312654
You can monitor the progress of the task with command:
squeue -j 4312654
Once the job has started you can monitor the progress of the job with command:
tail -f greasy-4312654.log

# Restart failed tasks

[runeberg@puhti-login2 restart]$ cat greasy_100.tasklist-undefined.rst
# 
# Greasy restart file generated at 2020-12-16 14:02:40
# Original task file: /scratch/project_2001199/Support/g16/greasy/restart/greasy_100.tasklist
# Log file: /scratch/project_2001199/Support/g16/greasy/restart/greasy-4312654.log
# 
# Warning: Task 12 failed
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_1.com > benzene_1/benzene_1.log
# Warning: Task 20 failed
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_27.com > benzene_27/benzene_27.log
# Warning: Task 59 failed
g16 < /scratch/project_2001199/Support/g16/greasy/restart/com/benzene_62.com > benzene_62/benzene_62.log
# End of restart file
[runeberg@puhti-login2 restart]$ sbatch-greasy --cores 4 --time 02:00 --nodes 1 --account project_2001199  
greasy_100.tasklist-undefined.rst
