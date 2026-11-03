# CHAPTER 9

# LIBRARY FUNCTIONS - Header files

The header files, or libraries, of the ANSI standard library, are as follows:

| assert.h | setjmp.h |
| ctype.h | signal.h |
| errno.h | stdarg.h |
| float.h | stddef.h |
| limits.h | stdio.h |
| locale.h | string.h |
| math.h | time.h |

The smaller of these libraries are signal.h - with only two functions, raise() and signal(); setjmp.h - with the functions longjmp() and setjmp(), for non-local jumps - and assert.h that just have the function assert(), to test assertions, i.e., to verify the validity of expressions.

Each company that developed C++ compilers has added over a certain amount of file headers, but the names in this case are not the same from one brand to another. Where there are more differences is the concerning to the screen manipulation functions. For example, the graphic file in the Turbo C++ is graphics.h, whereas in the Microsoft C++ is graph.h. Rarely there is correspondence between the functions of video of a compiler and another, but in this area, this phenomenon not only occurs with C language. In not dealing with video manipulation, there is a general agreement among several companies, mainly because of unification efforts of the ANSI.

# Mathematical functions