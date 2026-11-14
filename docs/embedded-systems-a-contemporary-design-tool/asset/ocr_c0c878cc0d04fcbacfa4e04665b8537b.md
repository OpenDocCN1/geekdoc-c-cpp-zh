Observe that the test parameter is computed with each iteration of the loop. For a large value of x, such an operation can accumulate substantial time. A good compiler should spot and optimize the computed value in a test parameter.

Without relying on the compiler, move the computation outside of the context of the loop:

```
int tempVar = x + 3;
For(j = 0; j < tempVar ; j++)
{
    a[j] = b[j] + c[j] ;
}
```

Now the value of tempVar is computed just a single time.

# Nested Loops

Let's modify the preceding example into a nested loop on several multidimensional arrays:

```
for(i = 0; i < K; i++)
{
    for(j = 0; i < m; j++)
    {
        a[i][j] = b[i][j] + c[i][j] ;
    }
}
```

+   6. Flow of control optimization.

When using branches or switches, avoid repeated jumps or tests. Consider the following assembly code fragment.

```
Instead of...
Je $2
$1: ...
jmp $3 ...
We write...
Je $1
$1: ...
$2: jmp $3 ...
```

For the following C code fragment, instead of the first fragment, we write the second. It may also be possible to set x to value before entering the switch and only change if necessary.