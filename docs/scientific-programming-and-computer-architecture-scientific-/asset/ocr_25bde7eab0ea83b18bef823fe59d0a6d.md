# 3.1. Overview of the x86 architecture

```
icc -c addtwo.s
```

to produce the object file addtwo.o (we are back to using icc). The object file can be linked to produce an executable using

```
icc -o addtwo.exe addtwo.o
```

The icc linker takes care of resolving the reference to printf in addtwo.o. When the executable addtwo.exe is run, we are told that

The sum of 1 and 2 is 3

# More about function calls

The output of the next listing, which is

The sum of 1 2 3 4 5 6 7 8 is 36

is hardly more exciting. However, it illustrates function calls made after placing arguments on the stack.

```
1 .file "addmany.s"
2 .section .mydata,"AMS",@probits,1
3 .LCO:
4 .string "The sum of %d %d %d %d %d %d %d %d is %d \n"
5 .text
6 .globl main
7 .type main, @function
8 main:
9 subq $32, %rsp
10 movl $36, 24(%rsp)
11 movl $8, 16(%rsp)
12 movl $7, 8(%rsp)
13 movl $6, (%rsp)
14 movl $5, %r9d
15 movl $3, %ecx
16 movl $2, %edx
17 movl $1, %esi
```