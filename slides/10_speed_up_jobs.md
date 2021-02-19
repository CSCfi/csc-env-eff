---
theme: csc-2019
lang: en
---

# Getting most out of CSC computers {.title}

## The purpose of large computers

Typically, large computers, like the ones at CSC, are not faster than others - they are just bigger. That is, for fast computation they utilize parallelism.
Parallelism means that you may use, simply speaking, hundreds or thousands of ordainary computers simultaneously for the solution of a single problem.

## Basic considerations
- Spend a little time to investigate which of all available software would be the best solve the kind od problem you have. Experienced colleagues and servicedesk@csc.fi are good places to ask for guidance.
- The software that has the capacity to solve it the fastest may, however, not always be the best. Issues like ease-of-use and compute-power/memory demands are also higly relevant. Quite often it is useful to start simple and gradually use more complex approaches if needed.
- Once you have found the software you want to use, check if it is available at CSC as a ready installed optimal version https://docs.csc.fi/apps/, and spend some time getting familiar with the softwares users manual, if available.
- If you cant find a suitable software, consider writing your own code.

## Optimize the performance of your own code
- Compile it with optimizing compiler options. [Compiling Puhti](https://docs.csc.fi/computing/compiling-puhti/), [Compiling Mahti](https://docs.csc.fi/computing/compiling-mahti/)
- Construct a small and quick test case and run it in the test queue [Queue options](https://docs.csc.fi/computing/running/batch-job-partitions/)
- Use profiling tools to find out how much time is spent in different parts of the code [Performance tools](https://docs.csc.fi/computing/performance/)
- When the compute bottle-necks are identified try to figure out ways to improve the code. Again, servicedesk@csc.fi is a channel to ask for help. The more concrete the problem is descried, the better.

## Running your software
- It is not only how your software is constructed and compiled that affect performance. It can also be run in different ways

### Running in parallel 
- Running in parallel with MPI and/or OpenMP.  
- Can you split your work into smaller bits and run them simultaneously? [array jobs](https://docs.csc.fi/computing/running/array-jobs/)
- Can you automate setting up, running and analysing your jobs? [workflow](https://docs.csc.fi/support/tutorials/many/)
- Can your software utilize GPUs? 

### What is OpenMP and what is MPI? 
- MPI and OpenMP and widely used standards for writing software that run in parallel
- MPI or (Message Passing Interface) is standard the utilize compute cores that do not share their memory, and therefore passes data-messages back and forth between the compute cores.
- OpenMP or Open Multi-Processing is a standard that utilize compute cores that share memory, and therefore do not need to send messages betwwen each other. Basically OpenMP is easier for beginners, but problems quickly arise with so called 'race conditions'. This appears when different compute cores process and update the sama data without proper synchronization.
- There are many tutorials available on the internet that can be found with simple search for e.g. 'MPI tutorial'. 
-There are documented exercise material and model answers from the CSC course "Introduction to Parallel Programming" availabel on GitHub [Parallel programming](https://github.com/csc-training/parallel-prog/). 


### Task farming - running multiple independent jobs simultaneously

- Task farming means that you have a set of, more or less, similar jobs that can be run independently of each other.
- Such jobs are most easily run as, so called, array-jobs. [array jobs](https://docs.csc.fi/computing/running/array-jobs/)
- In slightly more complex situations, workflows can be used. [workflow](https://docs.csc.fi/support/tutorials/many/) 
- Task farming can be combined withe.g. OpenMP to speed up independent jobs, and with MPI to run several jobs in parallel.
- There are a few things to consider: if the separate jobs are very different, running them in parallel with MPI easily waste
  allocated resources when the fast jobs wait for slower ones.
- Try to estimate as exact as possible the amount of memory and the time it the separate runs demand. [Run considerations](https://docs.csc.fi/support/tutorials/biojobs-on-puhti/)

### Use GPUs

- GPUs, or Graphics Processing Units, are exteremly powerful processors developed for graphics and gaming. They can be used for computations, but are often really tricky to program. Only a small set of algorithms can use the full power of GPUs.
- For any ready made software, the best way to check if the software can utilize GPUs, is to consult the software user's manual.  
- Do not try to use GPUs, unless you know what you are doing. If you're unsure, here's [how to check if your batch job used GPU](https://docs.csc.fi/support/tutorials/gpu-ml/#gpu-utilization)

### Be more clever instead of (only) using brute force

- It is reasonable to try to achieve best performance by using fastest computers available. This is however far from the only important issue.
- Different codes may give very different performance. Compare the options you have in [the CSC Software selection](https://docs.csc.fi/apps/)
- Before launching massive simulations, look for the most efficient algorithms to get the data you need
- Well known boosters are:
    - Enchanced sampling methods in molecular dynamics (vs. brute force plain MD)
    - Bayesian Optimization Structure Search ([BOSS](https://pypi.org/project/aalto-boss/), potential energy mapping)
    - When starting a new project, begin with small and fast test cases, and increase comutations gradually.
    - When scanning parameters, start with a coarse scan, and improve resolution where needed.
    - Be carefully submitting large numbers of jobs before you know the results are really what you are looking for.
    - Try to use or implement so called 'restart options' in software, and always check results in between restarts.
    - Try to preliminary formulate your scientific results when you have a minimum amount of computational results - it often helps
      to clarify what you still need to be computed and what is redundant.
   

### Common misconceptions

- Just adding more memory, more cores, more *X* does not necessarily help, if that is not the limiting step.
- When you allocate more resources, always confirm that the jobs actually complete faster - otherwise there is no use to allocate more resources.
    - Before starting simulations on a new system, [perform a scaling test](link to be added)
- Running the same job on your laptop with *one* core may be faster than doing the same in *e.g.* Puhti. Just using Puhti might not speed up things.
    - You might benefit of the application being there for you, though, or have faster access to a lot of data, but if your code can not be run in parallel, then you should consider some of the options above.

# Optimal use of CSC resources

The CSC supercomputers are used by hundreds of researchers. Please consider that when setting up your computational jobs. The most important things are:

- [Don't run heavy jobs in the login nodes](usage policy)
     - Either [use `sinteractive`](link) or regular [batch jobs](puhti tutorial, or something)
- Only reserve the amount of memory you need. You can [estimate the memory requirement from past jobs](https://docs.csc.fi/support/faq/how-much-memory-my-job-needs/)
- If your job reads and/or writes data to disk a lot, consider using NVMe.
     - Don't write lots of small files, FIXME more on this topic: separate page?
- Don't run too short jobs. There's an overhead in setting up a batch job. Aim for at least 30 minute jobs.
- Don't run too long jobs. In very long jobs the possibility of something going wrong is bigger and may lose used computing time. Investigate the possibility of restarts and chaining shorter simulations.

- If you run your own code, make sure it is optimized (Compiling code for Puhti, Guidelines for optimizing R-code, CSC R-environment, file IO? )
