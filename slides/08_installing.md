---
theme: csc-2019
lang: en
---

# Installing own software {.title}

In this section you will learn about installing your own software on CSC servers.

# Code categories:

# Binares

- If you have ready made binaries, you can just try to run them. 
  - This is not recommended for other than special cases
   (e.g. the code is compiled on an identical computer, and/or the computation
    you are going to make is just a short and computing). 
  - The problem with ready made binaries is that they are hardly ever optimal for the computer they are used on.
  - Especially MPI codes should always be re-compiled

# Interpreted languages
- Code written in a High-level interpreted languages like e.g. python, java, perl, or R. 
  - These languages do not need to be compiled, but they often can be. 
  - These languages are often quite easy and efficient to get a program to do what it should, but for very extensive computations they are rarely optimal (and can easily be very far from optimal). 
  - An efficient code should be constructed so that heavy computations utilize category 3) programming languages

# High-Performance-Computing languages:

- Programming languages that needs compiler (C,C++,Fortran). 
  - This is tricky but should be used for heavy high-performance computing.

# Basic requirements

- You need a computer with a decent internet connection
- You need a CSC account and need to be part of a project: https://research.csc.fi/accounts-and-projects
- Log in to a CSC computer: https://docs.csc.fi/computing/connecting/
- You need to know, at least basic, Unix line commands: 
  - https://www.csc.fi/documents/200270/380972/Working_in_Unix_Command_Line_2019.pdf/fcce16b9-77ca-4582-a27f-f92f1a5c4d6d

