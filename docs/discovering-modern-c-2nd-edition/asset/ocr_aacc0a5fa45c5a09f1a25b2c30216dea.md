```
==17306== Memcheck, a memory error detector
==17306== Copyright (C) 2002-2013, and GNU GPL'd, by Julian Seward et al.
==17306== Using Valgrind-3.10.0.SVN and LibVEX; rerun with -h for copyright info
==17306== Command: vector_test
==17306==
[1,1,2,-3,]
z[3] is -3
w is [1,1,2,-3,]
w is [1,1,2,-3,]
==17306==
==17306== HEAP SUMMARY:
==17306==     in use at exit: 72,832 bytes in 5 blocks
==17306==     total heap usage: 5 allocs, 0 frees, 72,832 bytes allocated
==17306==
==17306== LEAK SUMMARY:
==17306==     definitely lost: 128 bytes in 4 blocks
==17306==     indirectly lost: 0 bytes in 0 blocks
==17306==       possibly lost: 0 bytes in 0 blocks
==17306==     still reachable: 72,704 bytes in 1 blocks
==17306==         suppressed: 0 bytes in 0 blocks
==17306== Rerun with --leak-check=full to see details of leaked memory
==17306==
==17306== For counts of detected and suppressed errors, rerun with: -v
==17306== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```