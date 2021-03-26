# Batch job tutorial - Interactive jobs

- In this tutorial we'll get familiar with the basic usage of the Slurm batch queue system at CSC
- The goal is to learn how to request resources that **match** the needs of a job
- A job consists of two parts: resource requests and the job step(s)
- Examples are done on Puhti

## Interactive jobs

- In an interactive batch job, an interactive shell session is launced on a computing node. For heavy interactive tasks one can request specific resources (time, memory, cores, disk). 

- You can also use tools with graphical user interfaces in an interactive shell session. For such usage the [NoMachine](https://docs.csc.fi/support/tutorials/nomachine-usage/) remote desktop often provides an improved experience.  

### A simple interactive job 

- To start an interactive job using one core for ten minutes
```text
sinteractive --account myprojectname --time 00:10:00
```
- See the documetation at docs.csc.fi of [Interactive usage](https://docs.csc.fi/computing/running/interactive-usage/), for further information
 
## Additional material [FAQ on CSC batch jobs ](https://docs.csc.fi/support/faq/#batch-jobs) in Docs CSC
