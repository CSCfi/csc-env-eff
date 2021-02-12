# installing, making and making your own C, C++, or Fortran program in the CSC environment

## scenario A: you have a code already, you want to install it and run it.
A1. Create a proper directory for your code
A2. You need the codes sources files. Download from e.g. GitHub or use e.g. scp to upload a .zip file to the directory
A3. Unzip you code
A4. Follow any instructions on how to install. Usually comes with the code in form of a ‘readme’ or ’how to install’ file.

## Install scenario Aa: the code comes with cmake
Aa1. Module load cmake, and any other e.g. libraries the code needs (module spider), or try download and install also needed libraries.
Aa2. Create a ‘build’ directory, and go to that directory
Aa3. Run cmake ..
Aa4. If error messages, try to fix. If it becomes really messed up, remove all and start again from the .zip file
Aa5. Run ‘make’ to compile the specific codes you want to use
Aa6. Ask help from servicedesk if you really get stuck

## Install scenario Ab: the code comes with a makefile
Ab1. Module load or install separately any needed libraries
Ab2. Edit the ‘makefile’ and replace compile and link commands with proper ones for Mahti or Puhti
Ab3. Run the command ‘make’
Ab4. Read error messages and try to fix
Ab5. Ask help from servicedesk if not succesfull

## ScenarioB: you want to write your own code
B1. You need an editor
B2. Launch an editor and write the code
B3. Compile your code
B4. Fix bugs until compiler accepts code# 