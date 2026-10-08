# Compiling Objective-C Programs

# Compiling Objective-C Programs

```
$ gcc scanner.m
Undefined symbols:
"_OBJC_CLASS__NSAutleasePool", referenced
from:
  _objc_classrefs__DATA@00 in ccoRpaJq.o
"_objc_msgSend", referenced from:
  _main in ccoRpaJq.o

$ # On OS X
$ gcc -framework Foundation scanner.m
$ # On other platforms
$ gcc gnustep-config --objc-flags --base-libs
scanner.m
```

The clang front end is intended as a drop-in replacement for GCC, so anywhere you see gcc in some instructions, you can substitute clang. On OS X, GCC is installed in /usr/bin/gcc, so it is on your path. With slightly older versions of the Xcode tools, Clang was installed in /Developer/usr/bin/clang, so you may need to either specify the full path or add this location to your path. On other platforms you will generally find both on your path, if they are installed.

If you are familiar with compiling C or C++ with either of these compilers, you will find compiling Objective-C very familiar. If you just specify a source file on the command line, the compiler will attempt to compile and link it as an executable.