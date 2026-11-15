will install the binaries and supporting files into bin, lib and share subdirectories of the directory you specified using - -prefix on the configure line. In the example above, this is the top-level EMBOSS directory level from the CVS checkout, e.g.:

```
/home/auser/emboss
```

Had you not specified - -prefix=/home/auser/emboss they'd be installed to /usr/local by default (that isn't recommended).

> **Tip**
> If you want EMBOSS installed in somewhere other than /usr/local then use the - -prefix option of GNU configure to specify the EMBOSS installation directory. This is the recommended method of installation as EMBOSS has hundreds of files which might otherwise obscure other software, particularly under /usr/local/bin.

To compile and reinstall EMBOSS on subsequent occasions, use the following commands:

```
make clean
./configure
make
make install
```

Though extremely rare, there are circumstances where you may have to type rm config.cache (on very old installations) or rm -rf autom4te.cache before doing the above. Those occasions generally happen when trying to update a rather old existing version of EMBOSS.

# 1.2.4.1 Static and dynamic compilation

> **Note**
> A static library (statically linked library) is a library called by an application in which links to external functions and variables are resolved at compile-time by a linker. Static libraries are either compiled into object files and merged with the application during building/linking into a single executable, or are loaded at run-time and are accessible to the executable.
> 
> A dynamic library (dynamically linked library) in contrast implements dynamic linking, where libraries remain in separate files on disk and are not copied into the executable or library at compile-time. Instead a loader is used to access the library at load or run-time.
> 
> Executables created using static libraries are larger than executables linked to dynamic libraries, because static libraries include the code for the library function(s) within the executable. Static libraries, however, can be useful for debugging purposes and sometimes result in faster executables than when using dynamic libraries.