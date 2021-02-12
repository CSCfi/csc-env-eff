# installing, making and making your own C, C++, or Fortran program in the CSC environment

## scenario A: you have a code already, you want to install it and run it.
A1. Create a proper directory for your code (command: mkdir file-name)
A2. You need the codes sources files. Download from e.g. GitHub or use e.g. scp to upload a .zip file to the directory (https://docs.csc.fi/data/moving/scp/)
A3. Unzip you code (line command: unzip code-name.zip)
A4. Follow any instructions on how to install. Usually comes with the code in form of a ‘readme’ or ’how to install’ file.

## Install scenario Aa: the code comes with cmake
Aa1. Load the module cmake with line command: module load cmake, and load also any other e.g. libraries the code needs (avilable modules: module spider), or try download and install also needed libraries.
Aa2. Create a ‘build’ directory, and go to that directory (line commad: mkdir build, then: cd build)
Aa3. Run cmake ..
Aa4. If error messages, try to fix. If it becomes really messed up, remove all and start again from the .zip file
Aa5. Run ‘make’ to compile the specific codes you want to use
Aa6. Ask help from servicedesk if you really get stuck (mail to: servcedesk@csc.fi)

## Install scenario Ab: the code comes with a makefile
Ab1. Module load or install separately any needed libraries (check available modules with line command: module spider. Load module with: module load name-of-module)
Ab2. Edit the ‘makefile’ and replace compile and link commands with proper ones for Mahti (https://docs.csc.fi/computing/compiling-mahti/) or Puhti ( https://docs.csc.fi/computing/compiling-puhti/)
Ab3. Run the command ‘make’
Ab4. Read error messages and try to fix
Ab5. Ask help from servicedesk if not successfull (mail to: servicedesk@csc.fi)

## ScenarioB: you want to write your own code
B1. You need an editor https://docs.csc.fi/support/tutorials/env-guide/text-and-image-processing/
B2. Launch an editor and write the code
B3. Compile your code (on puhti:https://docs.csc.fi/computing/compiling-puhti/, and on Mahti: https://docs.csc.fi/computing/compiling-mahti/)
B4. Fix bugs until compiler accepts code# 
