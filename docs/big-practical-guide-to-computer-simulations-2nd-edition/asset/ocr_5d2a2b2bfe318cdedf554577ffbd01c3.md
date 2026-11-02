```
```c
 4 int main(int argc, char *argv[])
 5 {
 6     int t, *array, sum = 0;
 7
 8     array = (int *) malloc (99*sizeof(int));
 9     for(t=0; t<100; t++)
10         array[t] = t;
11     for(t=0; t<100; t++)
12         sum += array[t];
13     printf("sum= %d\n", sum);
14     free(array);
15     return(0);
16 }
```
```

The program is compiled via

```
```
cc -o memorror1 memorror1.c -g
```
```

We have compiled including -g, because the memory checker shall tell us where the bug appears and, in a second run, we want to transfer the control to the debugger automatically, if a bug appears.

Starting the program produces the following output, the program terminates normally:

```
```
sum= 4950
```
```

The result is correct, everything seems to be fine. Nevertheless, the array was used beyond its allocated regime. This can be seen by invoking valgrind in addition to the program:

```
```
 1 [hartmann@comphy01 debugging]$ valgrind memorror1
 2 Memcheck, a memory error detector.
 3 Copyright (C) 2002-2005, and GNU GPL'd, by Julian Seward et al.
 4 Using LibVEX rev 1575, a library for dynamic binary translation.
 5 Copyright (C) 2004-2005, and GNU GPL'd, by OpenWorks LLP.
 6 Using valgrind-3.1.1, a dynamic binary instrumentation framework.
 7 Copyright (C) 2000-2005, and GNU GPL'd, by Julian Seward et al.
 8 For more details, rerun with: -v
 9
10 Invalid write of size 4
11    at 0x804823: main (memerror1.c:10)
12 Address 0x402A1B4 is 0 bytes after a block of size 396 alloc'd
13    at 0x404405: malloc (vg_replace_malloc.c:149)
14    by 0x80483FF: main (memerror1.c:8)
15
```
```