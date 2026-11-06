# Cleaning up and making it all

When you have a Makefile and a huge project, you may want to periodically start fresh, cleaning out all your object files and the final executable, before you do a build. For example, you may be working on a project, and so much has changed that you would prefer to start fresh with your next build. To do this, you can include a clean section in your Makefile that looks like this, if you’re using Cygwin:

```
```make
clean :
    rm -f *.o
    rm -f *.obj
    rm -f myprogram.exe
```
```

Note that no files are listed after the colon. Thus, when you type

```
```make
make clean
```
```

the rm commands (which delete the files) will always run.

![](bbox=[0.154, 0.441, 0.234, 0.515])

If you’re using either the MinGW or Borland compiler, you want your clean section to look like this:

```
```make
clean :
    del *.o *.obj myprogram.exe
```
```

# Using macros

Environment variables can include macros. A macro is basically a word that represents something else that is probably more complicated. For example, you may have something like this:

```
```make
MYFILES = one.cpp two.cpp three.cpp four.cpp
```
```

Then, any place in your Makefile where you want to refer to the four files one.cpp, two.cpp, three.cpp, and four.cpp, you can instead simply write

```
```make
$(MYFILES)
```
```

When you access a macro, you precede it with a dollar sign ($), and you put the name inside parentheses. The make utility then knows that this is a macro and needs to be expanded.