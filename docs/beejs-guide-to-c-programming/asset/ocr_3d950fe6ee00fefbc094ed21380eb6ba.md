# #endif    // End of the #ifndef BAR_H

This will effectively cause the header file to be included only a single time, no matter how many places try
to #include it.

When it comes to multifile projects, you can make sure file-scope variables and functions are not visible
from other source files with the static keyword.

And you can refer to other files with extern.

For more info, check out the sections in the book on the static and extern storage-class classifiers.

# 17.3 static extern

This isn't part of the spec, it's 99.999% common in the C world.

You can compile C files into an intermediate representation called object files. These are compiled machine
code that hasn't been put into an executable.

Object files in Windows have a .OBJ extension; in Unix-likes, they're .o.

In gcc, we can build something like this, with the -c (compile only!) flag:

```
gcc -c foo.c      # produces foo.o
gcc -c bar.c      # produces bar.o
```

And we can link those together into a single executable:

```
gcc -o foo.o bar.o
```

Voila, we've produced an executable foo from the two object files.

But you're thinking, why bother? Can't we just:

```
gcc -o foo.c bar.c
```

and kill two boids with one stone?

For little programs, that's fine. I do it all the time.

For larger programs, we can take advantage of the fact that compiling from source to object files is
relatively slow, and linking a bunch of object files is relatively fast.

This really shows with the utility that only rebuilds sources that are newer than their outputs.

Let's say you have a thousand C files. You could compile all object files to start (slowly) and then
combine all object files into an executable (fast).

Now say you modified one of those C source files—here's the magic: you only have to rebuild that one
object file for that source file! And you rebuild the executable (fast). All the other C files don't have to
touched.

In other words

# 17.4 Compiling with Object Files