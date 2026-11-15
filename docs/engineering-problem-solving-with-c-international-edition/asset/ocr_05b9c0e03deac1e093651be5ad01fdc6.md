```
long factorial(int k);
long factorial_r(int k);
/* Get user input. */
printf("Enter positive integer: \\n");
scanf("%i", &n);
/* Compute and print factorials. */
printf("Nonrecursive: %i! = %li \\n",n,factorial(n));
printf("Recursive: %i! = %li \\n",n,factorial_r(n));
/* Exit program. */
return 0;
}
```

```
/*--------------------------------------------------------------*/
/* This function computes a factorial with a loop. */
long factorial(int k)
{
/* Declare variables. */
int j;
long term;
/* Compute factorial with multiplication. */
term = 1;
for (j=2; j<=k; j++)
term *= j;
/* Return factorial value. */
return term;
}
```

```
/*--------------------------------------------------------------*/
/* This function computes a factorial recursively. */
long factorial_r(int k)
{
/* Use recursive reference until k=0. */
if (k == 0)
return 1;
else
return k*factorial_r(k-1);
}
```

The condition k == 0 keeps the recursive routine from becoming an infinite loop; this routine calls itself recursively with an argument that is continually being decremented by 1, until the argument reaches zero.

For large values of k, the value of k! can exceed even long integers. In these cases, the computations should be done using double or long double values. An interesting approximation to k! is also discussed in the end-of-chapter problems.