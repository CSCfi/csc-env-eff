---
theme: csc-2019
lang: en
---

# How to speed up jobs {.title}

# What supercomputers are for!

One reason to use CSC resources is to get to results faster. This can be accomplished in several ways. Not all of them may be easy with your application. [Read here a concise summary of the typical parallelization options your code may have](https://docs.csc.fi/support/tutorials/biojobs-on-puhti/how-many-cores-can-my-application-use)

# The most common parallelization options
- Can you run your simulation in parallel with OpenMP? 
- Can you run your simulation in parallel with MPI?
- Can you split your work into smaller bits and run them simultaneously?
- Can you automate setting up, running and analysing your jobs?
- Can your job make use of GPUs? 
- Is there a faster code or better algorithm to give you the information you need?
- If your code is not parallelized, maybe you can do it yourself? Here are some examples for R

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
