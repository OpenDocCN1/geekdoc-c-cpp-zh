A little more complex example is

```
g++ -o myfluxer nyfluxer.cpp -I/opt/include -L/opt/lib -lblas
```

It compiles the file myfluxer.cpp and links it with the BLAS library in directory /opt/lib. Include files are searched in /opt/include in addition to the standard include path.

For generating fast executables, we have to use at least the following flags.

+   -O3 -DNDEBUG

-O3 is the highest optimization in g++. -DNDEBUG defines a macro that lets assert disappear in the executable by conditional compilation (#ifndef NDEBUG). Disabling assertion is very important for performance: MTL4, for instance, is almost an order of magnitude slower since each access is then range-checked. Conversely, we should use certain compiler flags for debugging as well:

+   -O0 -g

-O0 turns off all optimizations and globally disables inlining so that a debugger can step through the program. The flag -g lets the compiler store all names of functions and variables and labels of source lines in the binaries so that a debugger can associate the machine code with the source. A short tutorial for using g++ is found at http://tinf2.vub.ac.be/~dvermeir/manual/utntr0/gpp.html.

# B.2 Debugging

For those of you who play Sudoku, let us dare a comparison. Debugging a program is somewhat similar to fixing a mistake in a Sudoku: it is either quick and easy or really annoying, rarely in between. If the error was made quite recently, we can rapidly detect and fix it. When the mistake remains undetected for a while, it leads to false assumptions and causes a cascade of follow-up errors. As a consequence, in the search for the error we find many parts with wrong results and/or contradictions but which are consistent in themselves. The reason is that they are built on false premises. Questioning everything that we have created before with a lot of thought and work is very frustrating. In the case of a Sudoku, it is often best to ditch it altogether and start all over. For software development, this is not always an option.

Defensive programming with elaborate error handling—not only for user mistakes but for our own potential programming errors as well—not only leads to better software but is also quite often an excellent investment of time. Checking for our own programming errors (with assertions) takes a proportional amount of extra work (say, 5–20%) whereas the debugging effort can grow infinitely when a bug is hidden deep inside a large program.

# B.2.1 Text-Based Debugger

There are several debugging tools. In general, graphical ones are more user-friendly, but they are not always available or usable (especially when working on remote machines). In this section, we describe the gdb debugger, which is very useful to trace back run-time errors.