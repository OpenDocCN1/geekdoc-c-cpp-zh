![](bbox=[0.38, 0.12, 0.62, 0.24])

# FIGURE 14.5 Second cut on the make dependency tree.

The make rule corresponding to this dependency relationship is, therefore, the following. Note that the math library has to be linked because the compute function in the compute.c file uses the pow function in this library.

```
power: power.o compute.o
    gcc power.o compute.o -o power -lm
```

We also know that the object file power.o is built from the source file power.c and that the object file compute.o is built from the source file compute.c. Figure 14.5 shows the second cut on the dependency relationship.

Thus, the make rules for creating the two object files are

```
power.o: power.c
gcc -c power.c
compute.o: compute.c
gcc -c compute.c
```

The final makefile is shown as

```
$ cat makefile
power: power.o compute.o
    gcc power.o compute.o -o power -lm
power.o: power.c
    gcc -c power.c
compute.o: compute.c
    gcc -c compute.c
$
```

We then execute the make utility with the preceding makefile:

```
$ make
gcc -c power.c
gcc -c compute.c
gcc power.o compute.o -o power -lm
$
```

In the following in-chapter exercise, you will use the make utility to create the executable code for a C source code that is partitioned into two files.

# Exercise 14.6

Create the two source files power.c and compute.c and follow the steps just discussed to create the executable file power by using the make utility.

We now change the structure of this software and divide it into six files called main.c, compute.c, input.c, compute.h, input.h, and main.h. The contents of these files are shown in the following session. Note that the compute.h and input.h files contain declarations (prototypes) of the compute and