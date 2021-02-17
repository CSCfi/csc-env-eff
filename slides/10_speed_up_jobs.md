---
theme: csc-2019
lang: en
---

# How to speed up jobs {.title}

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
- Running with MPI and/or OpenMP [Parallel programmin](https://github.com/csc-training/parallel-prog/)
- Can you split your work into smaller bits and run them simultaneously? [array jobs](https://docs.csc.fi/computing/running/array-jobs/)
- Can you automate setting up, running and analysing your jobs? [workflow](https://docs.csc.fi/support/tutorials/many/)
- Can your software utilize GPUs? 

# What is OpenMP?

- What is OpenMP and link to examples with a couple of codes, e.g. directly to docs/apps/insertcodehere.md
- Bioinformatics tools have often been parallelized with OpenMP

# What is MPI?

- Brief explanation, how to check if your code can do that, link to some codes

# Farming i.e. running multiple jobs simultaneously

- Optimal scaling, caveats:
   - Workflows will reduce manual work and errors
   - beware too many batch jobs or job steps
   - be aware of partition limits
   - optimum job length
   - avoid idling allocations

# Leverage GPUs for speed

- GPUs can give a real boost, but can your code make use of them?
   - How to check if your code can utilize GPUs (FIXME i.e. tell how)
   - Note, just asking for GPUs from SLURM will not help if your code can't use them
   - If you're unsure, here's [how to check if your batch job used GPU](https://docs.csc.fi/support/tutorials/gpu-ml/#gpu-utilization)

# Be more clever instead of (only) using brute force

- Better performance is not only due to ever faster computers, but also because scientists have come up with more clever algorithms
- Different codes may give very different performance
    - Compare the options you have in [the CSC Software selection](https://docs.csc.fi/apps/)
- Before launching massive simulations, look for more efficient algorithms to get the data you need
- Well known boosters are:
    - Enchanced sampling methods in molecular dynamics (vs. brute force plain MD)
    - Bayesian Optimization Structure Search ([BOSS](https://pypi.org/project/aalto-boss/), potential energy mapping)
    - `<insert other discipline example here>` 

# Common misconceptions

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
