the same directory; launch this file and you will see the following output:

Hello World

A Makefile often contains multiple targets and can include other constructs such as macro definitions and also reference other makefiles. Keep in mind that the files that are specified on the right-side of the colon are the dependencies, which is HelloWorld.c in this example. The second line has a tab-based indentation that is required for any target in a makefile but is not visible in this example. If you use spaces instead of a tab, you will see the following type of error message when you invoke the make utility:

```
Makefile1:13: *** missing separator (did you mean TAB instead of 8 spaces?). Stop.
```

This is one of the most common errors that developers make when they create makefiles.

> NOTE The first character in a rule line must be a tab character.

A very simple makefile with the preceding target is discussed in the next section.

# BIG MAKE AND LITTLE MAKE

As you saw earlier in this Appendix, the file Makefile is called “big make” and the file makefile is called “little make.” If you type make on the command line, it will search for “big make” and execute the first target in that makefile. If “big make” does not exist, the make utility searches for “little make” and execute the first target in that makefile.