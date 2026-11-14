```
Total time is 100 · O(1) = O(100 · 1) = O(100)
```

The complexity of this loop is constant.
That this loop is faster makes sense when N >> 100.

# 14.7.2.2 While Loops

Analysis of the while loop shown in Figure 14.5, duplicates that of the for loop.

```
bool done = false;
int result = 1
int n; // n has some value
while ( !done )
{
    result = result * n;
    n--;
    if ( n < 1 ) done = true;
}
```

Figure 14.5 The while Loop.

+   Number of iterations.
+   The loop terminates when done == true, which happens after n iterations.

+   Number of steps per iteration.
+   3 = O(1) steps per iteration
+   1. The multiply result • n
+   2. The assignment result =
+   3. The auto decrement n--

```
Total time is N · O(1) = O(N) · 1 = O(N)
```

# 14.7.3 Sequences of Statements

For a sequence of statements, simply compute their individual complexity functions and add
them up. If the two loops are executed in sequence, the result is as shown in Figure 14.6.

```
int j, k, sum = 0;
for ( j = 0; j < N; j++ )
    for ( k = 0; k < j; k++ )
        sum = sum + k * j;
for ( i = 0; i < N; i++ )
    sum = sum - i;
```

Figure 14.6 Sequences of Statements.