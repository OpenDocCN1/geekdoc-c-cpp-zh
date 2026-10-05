implemented by compilers only several years after that, one has to acknowledge that there is some basis to that belief. Modern C++ compilers such as icpc and g++ support restrict pointers. So the point about aliasing is no longer valid.

Once C and C++ are well understood, their advantages are considerable. The C language encourages and seldom impedes hiding of how program variables and objects are laid out in memory. A variety of data structures ranging from lists to trees to graphs hash tables can be implemented with a suppleness that is not approached by languages such as Fortran. While C and C++ are routinely used to implement device drivers, operating systems, compilers, and network protocols, the limitations of Fortran's idiom would become apparent if anyone attempted to use it for such complicated programming tasks. Even when the programming task is not so complicated, C/C++ have much more to offer if the idom native to these languages are understood.

# 3.2.7 A little compiler theory

The compiler's view of a program is quite different from that of a human programmer. A human programmer has a problem to be solved and an idea to solve that problem that is expressed as a computer program. What the compiler sees is a sequence of statements that obey the syntactic rules of the programming language. The global view of what the program does is lost.

To generate good assembly, the compiler has to grasp which variables are used heavily and other global aspects of the program. Uncovering global information from a program, which is presented to the compiler as a sequence of statements is quite hard. In this section, we will consider some of the ideas on optimizing compilers rely.¹¹⁸

In a sequential program, the statements depend on one another. We assume that x, y, and z are program variables. The following is an example:

```
y=x;
.\.
z=x;
```

> ¹⁸Our main reference is Allen and Kennedy (2002). In it may be found bibliographic discussions of the work of Kuck, Banerjee, Kennedy, and other researchers. Our earlier discussion of compiler optimizations drew heavily from this reference.