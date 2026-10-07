# PARALLEL PROCESSING IN R

$slave1
$slave1[[1]]

| Var1 Var2 Var3 Var4 Var5 Var6 Var7 Var8 Var9 Var10 |
| 376 1 1 0 1 1 0 1 1 0 |

$slave1[[2]]

```
[1] 8.00000 54.56251
```

$slave2
$slave2[[1]]

| Var1 Var2 Var3 Var4 Var5 Var6 Var7 Var8 Var9 Var10 |
| 630 0 1 0 0 1 1 0 0 1 |

$slave2[[2]]

```
[1] 7.000 2088.777
```

$slave3
$slave3[[1]]

| Var1 Var2 Var3 Var4 Var5 Var6 Var7 Var8 Var9 Var10 |
| 888 1 1 1 0 1 1 0 0 1 |

```
$slave3[[2]]
> myRegTask(indexList([[1]])
[[1]]
```

| Var1 Var2 Var3 Var4 Var5 Var6 Var7 Var8 Var9 Var10 |
| 120 1 1 1 0 0 1 1 0 0 |

```
[[2]]
[1] 7.000 2082.128
```

The best-fitting variable is therefore the one that generated the data; i.e., the one with eighth, ninth and tenth variables deleted.

The R package contains a function regresssets that will also carry out all-subsets (as with other variables) selection. An application of it to our simulated dataset produced

```
> library(leaps)
> summary(regresssets(x, y, nbest=1, nmax=10))[[c(1,6)]
$which
```

| (Intercept) a b c d e f g h j |
| 1 TRUE TRUE TRUE FALSE FALSE FALSE TRUE FALSE FALSE TRUE |
| 2 TRUE TRUE TRUE FALSE FALSE FALSE TRUE FALSE FALSE TRUE |
| 3 TRUE TRUE TRUE FALSE FALSE FALSE TRUE FALSE FALSE TRUE |
| 4 TRUE TRUE TRUE FALSE TRUE TRUE TRUE TRUE FALSE TRUE |
| 5 TRUE TRUE TRUE FALSE TRUE TRUE TRUE TRUE FALSE TRUE |
| 6 TRUE TRUE TRUE FALSE TRUE TRUE TRUE TRUE FALSE TRUE |
| 7 TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE |
| 8 TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE |
| 9 TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE |
| 10 TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE |

```
$bic
[1] -457.0253 -953.7679 -1879.9000 -2558.5660 -3136.6823 -3210.0709
[2] -7236.5377 -3223.6831 -3228.3021 -3221.8135
```

The first lists is applied to the regression variables. The subsets function is then applied