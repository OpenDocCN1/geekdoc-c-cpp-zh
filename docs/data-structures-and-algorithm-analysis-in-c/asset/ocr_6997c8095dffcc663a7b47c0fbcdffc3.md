# Average-Case Analysis

This is the most difficult part. For the average case, we assume that each of the sizes for S1 is equally likely, and hence has probability 1/N. This assumption is actually valid for our pivoting and partitioning strategy, but it is not valid for some others. Partitioning strategies that do not preserve the randomness of the subarrays cannot use this analysis. Interestingly, these strategies seem to result in programs that take longer to run in practice.

With this assumption, the average value of T(i), and hence T(N - i - 1), is (1/N) \sum_{j=0}^{N-1} T(j). Equation (7.1) then becomes

```
T(N) = \frac{2}{N} \left[ \sum_{j=0}^{N-1} T(j) \right] + cN \tag{7.14}
```

If Equation (7.14) is multiplied by N, it becomes

```
NT(N) = 2 \left[ \sum_{j=0}^{N-1} T(j) \right] + cN^2 \tag{7.15}
```

We need to remove the summation sign to simplify matters. We note that we can telescope with one more equation:

```
(N - 1)T(N - 1) = 2 \left[ \sum_{j=0}^{N-2} T(j) \right] + c(N - 1)^2 \tag{7.16}
```

If we subtract Equation (7.16) from Equation (7.15), we obtain

```
NT(N) - (N - 1)T(N - 1) = 2T(N - 1) + 2cN - c \tag{7.17}
```

We rearrange terms and drop the insignificant -c on the right, obtaining

```
NT(N) = (N + 1)T(N - 1) + 2cN \tag{7.18}
```

We now have a formula for T(N) in terms of T(N - 1) only. Again the idea is to telescope, but Equation (7.18) is in the wrong form. Divide Equation (7.18) by N(N + 1):

```
\frac{T(N)}{N + 1} = \frac{T(N - 1)}{N} + \frac{2c}{N + 1} \tag{7.19}
```

Now we can telescope.

```
\frac{T(N - 1)}{N} = \frac{T(N - 2)}{N - 1} + \frac{2c}{N} \tag{7.20}
\frac{T(N - 2)}{N - 1} = \frac{T(N - 3)}{N - 2} + \frac{2c}{N - 1} \tag{7.21}
\vdots
\frac{T(2)}{3} = \frac{T(1)}{2} + \frac{2c}{3} \tag{7.22}
```