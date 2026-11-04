The longer way of doing the same thing is to specify the full path to the library as part of the compilation step (preferably as a macro definition), as shown here:

```
```
-L/usr/lib/libm.a
```
```

# DUMMY TARGETS IN A MAKEFILE

If you want to execute commands instead of creating a target, you can define a dummy target, which does not involve any files.

There are some common dummy targets used in makefiles:

```
```
make clean
make all
```
```

The "clean" target is typically used for removing files (such as object files and executables) from a directory. The removal of such files forces the makefile to recompile all the ".o" files.

# INCLUDING A MAKEFILE IN ANOTHER MAKEFILE

Source code trees often have separate makefiles in the main directories of the source code that handle the dependencies that are local to a given directory. A top-level makefile acts as the "master" makefile that contains targets for creating one or more executables.

Listing A.13 displays the contents of `BranchMakefile` that contains a target that will execute a target in `BranchMakefile` that is located in the branch subdirectory.