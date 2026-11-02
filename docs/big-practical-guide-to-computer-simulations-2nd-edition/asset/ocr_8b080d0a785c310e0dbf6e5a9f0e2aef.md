# 4.3 Memory checker

Most program bugs are revealed by systematically running the program and cross-checking with the expected results. But other errors seem to appear in a rather irregular and unpredictable fashion. Sometimes a program runs without a problem, in other cases it crashes with a Segmentation fault at rather puzzling locations in the code. Very often a bad memory management is the cause of such a behavior. Writing beyond the boundaries of an array, reading uninitialized memory locations or addressing data which has been freed already, are the most common bugs of this class. Since the operating system organizes the memory in a different way each time a program is run, it is rather unpredictable whether these errors become apparent or not. Furthermore, it is very hard to track them down, because the effect of such errors becomes visible most of the time at program locations different from where the error has occurred.

As an example, we consider the case where the program writes beyond the boundary of an array. This array is stored in the memory area called heap, where all allocated memory is taken from. If at the location behind the array another variable is stored, it may be overwritten in this case. Hence, the error becomes visible the next time the other variable is read. On the other hand, if the memory block behind the array is not used, the program may run without any problems this time. Unfortunately, the programmer is not able to influence the memory management directly.

To detect such types of nasty bugs, one can take advantage of memory checkers. Here, valgrind is considered, which is a very convenient tool and freely available. It works under UNIX and is included by just writing valgrind in front of the calling sequence of your program. No special compile commands or libraries are necessary. You can even debug standard programs like ls, try valgrind ls.

As an example, the program from Sec. 4.1 is considered, which is modified a bit; the memory block allocated for the array is now slightly too short (length 99 instead of 100);

| GET SOURCE CODE |
|---| 
| DIR: `debugging` |
| FILE(S): `nemerror1.c` |

```
1 #include <stdio.h>
2 #include <stdlib.h>
3
```

2 Not to be confused with the data structure heap introduced in Sec. 6.7.1.