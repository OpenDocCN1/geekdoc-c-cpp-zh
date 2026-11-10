# 11.7. **FINDING SYNCHRONIZATION-FREE PARALLELISM**

statements nested in the same loop follow the lexicographic order. Geometrically, dependence of a two-dimensional loop nest always point within the range [0°, 180°), meaning that the angle of the dependence must be below 180°, but no less than 0°.

The affine transforms change the ordering of iterations such that all the dependences are found only between operations nested within the same iteration of the outermost loop. In other words, there are no dependence edges at the boundaries of iterations in the outermost loop. We can parallelize simple source codes by drawing their dependences and finding such transforms geometrically.

# 11.7.9  Exercises for Section 11.7

**Exercise 11.7.1:** For the following loop

```
for (i = 2; i < 100; i++)
    A[i] = A[i-2];
```

+   a) What is the largest number of processors that can be used effectively to execute this loop?
+   
+   b) Rewrite the code with processor *p* as a parameter.
+   
+   c) Set up and find one solution to the space-partition constraints for this loop.
+   
+   d) What is the affine partition of highest rank for this loop?

**Exercise 11.7.2:** Repeat Exercise 11.7.1 for the loop nests in Fig. 11.37.

**Exercise 11.7.3:** Rewrite the following code

```
for (i = 0; i < 100; i++)
    A[i] = 2*A[i];
for (j = 0; j < 100; j++)
    A[j] = A[j] + 1;
```

so it consists of a single loop. Rewrite the loop in terms of a processor number *p* so the code can be partitioned among 100 processors, with iteration *p* executed by processor *p*.

**Exercise 11.7.4:** In the following code

```
for (i = 1; i < 100; i++)
    for (j = 1; j < 100; j++)
/* (s) */    A[i,j] =
        (A[i-1,j] + A[i+1,j] + A[i,j-1] + A[i,j+1])/4;
```