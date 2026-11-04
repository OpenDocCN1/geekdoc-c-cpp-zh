instance you can specify custom “header” files (text files with a `.h` suffix), other object files (binary files with a `.o` suffix), or additional libraries (binary files with a `.a` or `.so` suffix) that are necessary for creating a binary executable.

The file `Makefile` can also contain rules that do not involve compilation, such as shell scripts and Unix commands. You can also create a “master” `Makefile` that contains rules that invoke the `make` utility using a `Makefile` located in a subdirectory. This is very useful, because you can subdivide a large project into a set of modules, where the code for each module is in a different subdirectory that contains a module-specific `Makefile`.

The next section discusses some useful commands (such as `ar`, `ranlib`, and `nm`) that you can specify in a `Makefile` target in order to operate compilation-related steps for your `C` programs.

# USEFUL UNIX COMMANDS FOR LIBRARIES

Throughout this book you have used the `gcc` utility to create binary executable files from `C` programs. However, in mid-sized and larger projects, `C` applications often involve “assembling” multiple `C` files into a single binary file. Those `C` files are compiled into so-called object files, which are binary files with a “.o” extension.

The `ar` (“archive”) command enables you to combine multiple “.o” files into a library file, which is a binary file with a “.a” extension (which are static libraries). In particular, the `ar` command enables you to add, remove, or update “.o” files in a library file.