---
theme: csc-2019
lang: en
---

# Installing own software {.title}

In this section you will learn about installing your own software on CSC servers.

# Code categories
- It is possible to install software on CSC servers
- Start by reading the software documentation
- Check the installation instructions to based the code type
  - Installation method depends on code type
  - Instructions found on the web rarely work "copy/paste" in HPC environment
- Before doing a lot of work, check if an alternative is already available in [CSC application list](https://docs.csc.fi/apps/)

# Binares
- If you have ready made binaries, you can just try to run them
- Problem with ready made binaries is that they are hardly ever optimal for the computer they are used on
  - Especially MPI codes should always be re-compiled
- Ready binaries should be considered if
  - Source code not available
  - Software is compiled on identical computer 
  - Software is for relatively light (serial or threaded) computation

# Interpreted languages
- Examples of High-level interpreted languages are
  -  Python, Java, Perl, R etc. 
- These languages do not need to be compiled, but they often can be. 
- These languages are often quite easy and efficient to program and therefore to get a result, but for very extensive computations they are rarely optimal (and can easily be very far from optimal). 
- An efficient code should be constructed so that heavy computations utilize libraries and/or subroutines written in High-Performance-Computing programming languages

# High-Performance-Computing languages
- Programming languages that need a compiler (C,C++,Fortran). 
- These languages are not easy to program and for complicated tasks need quite a lot of experience and much work.

# Basic requirements
- You need a computer with a decent internet connection.
- You need a CSC account and need to be [part of a project](https://research.csc.fi/accounts-and-projects)
- You need to [log in to a CSC computer](https://docs.csc.fi/computing/connecting/)
- You need to know, at least basic, Unix/Linux line commands 
  - CSC's [Linux basics tutorial](https://docs.csc.fi/support/tutorials/env-guide/using-linux-in-command-line/)
  - [Linux Command line quick reference / Cheat Sheet](https://docs.csc.fi/img/csc-quick-reference.pdf)


# Instructions
- See tutorials for each category for more detailed instructions
 - Interpreted languages (link)
 - High-Performance-Computing languages (link)
 - Applications may also be available as [containers](09_singularity.html), which can be used in CSC environment.

# Testing
- Construct a batch script
- Make a short and simple test run
  - Use known test data, e.g. test data provided by the code developer if you use a ready made code.
  - Write a simple program and compile it.
- Run a test in the `test` queue or in an [interactive session](https://docs.csc.fi/computing/running/interactive-usage/) directly from the command line
