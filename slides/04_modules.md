--
theme: csc-2019
lang: en
--

# Module system {.title}

In this section, you will learn about module systems and how to use them in CSC supercomputers.
Same information can be found in [the module section of our user guide at docs.csc.fi](https://docs.csc.fi/computing/modules/)

# Module systems in supercomputers

- Several, mutually incompatible softwares needed in one supercomputer
- The solution for managing this situation: separate the applications in *modules*
- *Environment modules* set up everything required by a particular application:
- Load libraries, adjust path, set environment variables 

# Module system in CSC supercomputers

- CSC uses [*Lmod*](https://lmod.readthedocs.io/en/latest/) environment modules, which are using *Lua* programming language
- These modules are used both in interactive and batch jobs
- Some softwares/applications have their own module (like *gromacs-env*), whereas some are combined in larger modules (like *biokit*, *geoconda*), and some can be find in many different modules (like *GDAL*, 
- The syntax is simple: module command module-name (for example: module load gromacs-env)
- You can check the available applications and their respective modules in the [Application list](https://docs.csc.fi/apps/)

# How to navigate in the jungle of modules?

- You can't just load all the modules because of the dependencies
- Commands: *module spider*, *module list* and *module avail* will help you 
- Search for an application in the list of all modules: *module spider searchword* 
- See the list of modules loaded at the moment: *module list*
- Modules available at the moment (due to depencies): *module avail* (hides modules that can't be loaded atm)
- If you try to load a module that is not available, you will get an error message saying so 
- [List of commands](https://docs.csc.fi/computing/modules/#basic-usage)
