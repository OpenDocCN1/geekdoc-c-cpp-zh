memcheck detects memory-management problems like leaks. It also reports read access of uninitialized memory and partly out-of-bounds access. If we omitted the copy constructor of our vector class (so that the compiler would generate one with aliasing effects), we would see the following output:

```
==17386== Memcheck, a memory error detector
==17386== Copyright (C) 2002-2013, and GNU GPL'd, by Julian Seward et al.
==17386== Using Valgrind-3.10.0.SVN and LibVEX; rerun with -h for copyright info
==17386== Command: vector_test
==17386==
[1,1,2,3]
z[3] is -3
w is [1,1,2,3]
W is [1,1,2,3]
==17386==
==17386== HEAP SUMMARY:
==17386==     in use at exit: 72,832 bytes in 5 blocks
==17386==   total heap usage: 5 allocs, 0 frees, 72,832 bytes allocated
==17386==
==17386== LEAK SUMMARY:
==17386==     definitely lost: 128 bytes in 4 blocks
==17386==     indirectly lost: 0 bytes in 0 blocks
==17386==      possibly lost: 0 bytes in 0 blocks
==17386==     still reachable: 72,704 bytes in 1 blocks
==17386==         suppressed: 0 bytes in 0 blocks
==17386== Rerun with --leak-check=full to see details of leaked memory
==17386==
==17386== For counts of detected and suppressed errors, rerun with: -v
==17386== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

All these errors can be reported in verbose mode with the corresponding source line and the function stack:

```
valgrind --tool=memcheck -v --leak-check=full \
--show-leak-kinds=all vector_test
```

Now we see significantly more details which we refrain from printing here for reasons of size. Please try it on your own.

Program runs with memcheck are slower, in extreme cases up to a factor of 10 or 30. Especially software that uses raw pointers (which hopefully will be an exception in the future) should be checked regularly with valgrind. More information is found at http://valgrind.org.

Some commercial debuggers (like DDT) already contain memory analysis. Visual Studio offers plug-ins for finding memory leaks.

# B.4 gnuplot

A public-domain program for visual output is gnuplot. Assume we have a data file results.dat with the following content:

```
0 1
0 .25 0.968713
0 .75 0.740851
```