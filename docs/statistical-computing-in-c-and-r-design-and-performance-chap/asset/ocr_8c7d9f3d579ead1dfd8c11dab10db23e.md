# AN INTRODUCTION TO R

point you may be entering commands. To suppress the copyright information, you can
use a silent option in

```
$ R --silent
>
```

In order to access a previously saved workspaceName, one must either supply
full path to R from the directory where the saved image resides. If R has
been started in a different directory, the working directory can be changed to the one specified by setwd("pathToDoDirectory") the
working directory can be determined via the command getwd(). Somewhat more generally,
commands to the underlying Unix system can be executed while in R using the system
command. For instance, entering system("pwd") at the R command will produce
tame information as getwd.

Once a R session it may be of interest to load various R packages or libraries.
The library function, e.g., library(lattice) has
effect of making the objects in the R graphics package accessible from the R
session. The command search() will return a list of all the packages that are currently
loaded.

To see a list of all the help topics are available for the installed packages
help.start(). This produces an html file for which packages link will allow access
to information about a specific package of interest. Some packages also have "vignettes"
are pdf files containing discussions (including code) of topics related to the package.
The command vignette(package = "packageName") will return a list of the available
vignettes for the package packageName.

There are many packages that are not part of the standard installation but can
downownloaded separately. To install a package one uses packages("packageName")
that install an R package packageName (if it exists). The user will be asked to select
a repository (or CRAN mirror) from a list which installation should proceed
automatically.

R has along of the Unix commands for listing the contents and removing objects
a workspace. The command ls() provide a list of the objects in the
workspace. To remove objects from the current session use rm(o1, o2, ...) with o1, o2,
a comma separated list of the names of the objects that are to delete. In particular,
rm(list = ls()) will remove all objects from workspace.

The three most common data structures in R are data frame, matrix and list. The matrix
 list structures possesses the expected properties; e.g., matrix(pi, 2, 3) creates a 2x3
matrix with every entry equal to pi approximation to the value of pi. The command

> * As noted in Appendix A, the . prefixed to the file name will render it to the ls command
unless its -a option is used.