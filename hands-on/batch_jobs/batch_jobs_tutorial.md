# Batch job tutorial

- In this tutorial we'll get familiar with the basic usage of the Slurm batch queue system at CSC
- The goal is to learn how to request resources that **match** the needs of a job  
- A job consists of two parts: resource requests and job step(s)
- We'll go through examples for both serial and parallel jobs
- Examples are done on Puhti 

## Serial jobs

- For a program that can use only one core (cpu), one should request only one core from Slurm. 
- The job doesn't benefit from additional cores, hence don't request more 
- Excess reservation is waisted since it's not available to other users
- Within the job, the actual program is launched using the command `srun` 

```text 
#!/bin/bash
#SBATCH --account=myprojectname
#SBATCH --partition=test
#SBATCH --ntasks=1
#SBATCH --time=00:02:00

srun hostname
srun sleep 60
```
- In the batch job example above we are requesting one core (`--ntasks=1`) for two minutes (`--time=00:02:00`) from the test queue (`--partition=test`)
- We want to run the program `hostname`, that will print the name of the Puhti computing node that has been allocated for this particular job.
- In addition, we are running the `sleep` program to keep the job running for an additional 60 seconds, in order to have time to monitor the job
- Copy the example above into a file called `my_serial.bash` and change the `myprojectname` to the project you actually want to use
- Submit the job to the queue with the command `sbatch my_serial.bash`  
- If you are quick enough you should see your job in the queue by issuing the command `squeue -u $USER` 
- By default the output is written into a file named `slurm-XXXXXXX.out` where `XXXXXXX` is a unique number corresponding to the job ID of the job 
- Check the efficiency of the job compared to the reserved resources by issuing the command `seff XXXXXXX` (replace `XXXXXXX` with the actual  job ID number from the `slurm-XXXXXXX.out` file) 
- You can get a list of all your jobs that are running or queuing with the command `squeue -u $USER`
- A submitted job can be cancelled using the command `scancel XXXXXXX` 


## Parallel jobs
- A parallel program is capable of utilizing several cores simultaneously for the same job
- The aim of a parallel program is to solve problems (jobs) faster and to be able to tacle larger problems that wouldn't fit into a single core
- Depending on the parallel program and the type of job, the optimal resource request is often difficult to decide
- Dowload a simple parallel program with the command `wget https://a3s.fi/hello_mpi.x/hello_mpi.x`
- Make it executable using the command `chmod +x hello_mpi.x` 

```text
#!/bin/bash
#SBATCH --account=myprojectname
#SBATCH --partition=test
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=4
#SBATCH --time=00:00:10

srun hello_mpi.x
```

- In the batch job example above we are requesting resources from two nodes (`--nodes=2`), and four cores from each node (`--ntasks-per-node=4`) for ten seconds (`--time=00:00:10`) from the test queue (`--partition=test`)
- We want to run the program `hello_mpi.x`, that will, based on the resource request, start 8 simultaneous tasks  
- Each of the 8 tasks launced by `hello_mpi.x` will report on which node they got their resource 
- Copy the example above into a file called `my_parallel.bash` and change the `myprojectname` to the project you actually want to use
- Submit the job to the queue with the command `sbatch my_parallel.bash`
- When finished, the output file `slurm-XXXXXXX.out` should contain the results obtained by the `hello_mpi.x` program on how the 8 tasks were distributed over the two reserved nodes
- Check it with the `cat slurm-XXXXXXX.out` command:

```text
cat slurm-5099873.out
Hello world from node r07c01.bullx, rank 0 out of 8 tasks
Hello world from node r07c02.bullx, rank 5 out of 8 tasks
Hello world from node r07c02.bullx, rank 7 out of 8 tasks
Hello world from node r07c01.bullx, rank 2 out of 8 tasks
Hello world from node r07c02.bullx, rank 4 out of 8 tasks
Hello world from node r07c01.bullx, rank 3 out of 8 tasks
Hello world from node r07c01.bullx, rank 1 out of 8 tasks
Hello world from node r07c02.bullx, rank 6 out of 8 tasks
```
- The output above verifies that the requested 8 tasks were distributed over two nodes (`r07c01.bullx, r07c02.bullx`), four tasks on each
- Check the efficiency of the job compared to the reserved resources by issuing the command `seff XXXXXXX` (replace `XXXXXXX` with the actual  job ID number from the `slurm-XXXXXXX.out` file)
- You can get a list of all your jobs that are running or queuing with the command `squeue -u $USER`
- A submitted job can be cancelled using the command `scancel XXXXXXX` 

## Gathering information
- The `sinfo` command gives an overview of the partitions(queues) offered by the computer
- The `squeue` command shows the list of jobs which are currently queued (they are in the RUNNING state, noted as ‘R’) or waiting for resources (noted as ‘PD’, short for PENDING)
- the command `squeue -u $USER` lists your jobs 
 
## Additional material 
- [Hands-on batch jobs in Puhti tutorial](https://docs.csc.fi/support/tutorials/cmdline-handson/)
- [FAQ on CSC batch jobs ](https://docs.csc.fi/support/faq/#batch-jobs)
