# 66 Chapter 2. C/C++: Libraries and Makefiles

```
n = len/2;
if(len%2==0)
    n--;
for(i=0; i < n; i++){
    farg = len-2*i; printseq_(seq1,&farg);
    aitken_(seq1, seq2, &farg);
    for(j=0; j < len-2*(i+1); j++)
        seq1[j] = seq2[j];
}
if(len%2==0)
else
    {farg = 1; printseq_(seq1, &farg);
```

Line by line, this is almost the same as the C program for extrapolating the Leibniz series using function names defined in C (see page 22). There are only a few differences. Using function names with the underscore appended is the most obvious one. Another difference is that we invoke printseq as printseq_(seq1,&farg) after taking care to store len-2*i in farg on line 11. Similarly, the call to aitken_ on line 12 gives the third argument as &farg. A value such as len-2 cannot be passed as an argument to a Fortran function. The value must be stored in a memory location, and the address of that memory location must be passed by a pointer. On 17 and 18, the second argument of printseq_ is &farg for the same reason.

To build the executable, we use the source (comprised of the extern declarations, and the definition of main()) leibniz() on page 21 in the file leibnizFinC.c. The following three commands are used to make afile.

```
icc -c leibnizFinC.c
ifort -c aitken.f
icc -o leibnizFinC.exe leibnizFinC.o aitken.o
```

The first two commands create the object files. The -c option tells icc to compile only. The third command attempts to build the executable using the object files. This command uses the icc linker and the Fortran linker, which leads to a problem. We have seen already that the object code for aitken.o contains some undefined