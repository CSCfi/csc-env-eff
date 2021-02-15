# Installing applications and libraries for Java, Perl, Python and R 

## Java
Java applications do not typically require special installation. You just need
to download the .jar file.

If you get an error message about java version, try loading a suitable java 
module. You can check the available modules with command:
`module spider java`

Despite their name, modules named `biojava` are just normal java installations,
and can be used with any software, not just bio applications.

Some java applications fail to run on the login nodes. Try running them using
`sinteractive` instead. 

Naturally no compute heavy tasks should be run on the login nodes.

## Perl

To run Perl applications it usually best to first load a perl module.

To check available versions, use:
```text
module spider perl
```
To install and use your own perl packages, it usually enough to download them
to a suitable location and make sure they are included in perl `@INC`

There are three main ways to do it:
1. Inlude command line option -I (capital i) with the path on the command line:
```text
perl -I /projappl/project_12345/myperl ./my_app.pm
```
2. Include the path in `$PERL5LIB` environment variable.
```text
export PERL5LIB=/projappl/project_12345/myperl:${PERL5LIB}
```
3. Iclude the path in the perl code with `use lib`
```text
    use lib '/projappl/project_12345/myperl';
    use My::Module;
```
### Bioperl
If your code requires bioperl, we have a bioperl installation available.

See our [biperl documentation](https://docs.csc.fi/apps/bioperl/) for details.

## Python

TO BE ADDED

## R

Puhti has several R version available as modules. You should start by checking
if one of these is suitable for you needs. 

To check available versions, use:
```text
module spider r-env
```
It is also possible to install your own R packages.

See the [r-env-singularity](https://docs.csc.fi/apps/r-env-singularity/) 
documentation for instructions.

