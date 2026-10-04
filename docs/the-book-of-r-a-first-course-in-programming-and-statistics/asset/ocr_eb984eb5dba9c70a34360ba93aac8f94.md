# R > baz

```
[,1] [2] [3]
[1,] 1 NA NA
[2,] 2 5 8
[3,] 6 NA Nan
```

The object foo is a character vector with entries 2, 3 and 6 missing; bar is a factor vector of length 11 with elements 2, 3, 7, and 10 missing; and baz is a numeric matrix with row 1, columns 2 and 3, and row 3, elements missing. In the factor vector, note that the NAs are <NA>. This is to differentiate between bona fide values of the factor and the missing observations from being mistakenly interpreted as one of the levels.

Like the other special values so, you can identify NA elements using the function is.na. This is often useful for removing or replacing NA values. Consider the following numeric vector:

```
R qux <- c(NA,5.89,Inf,NA,9.43,-2.35,NaN,2.10,-8.53,NA,-4.58,2.01,NaN)
R qux
[1] NA 5.89 Inf NA 9.43 NaN 2.10 -7.58 NA -4.58
[13] 2.01 NaN
```

This vector has a total of 14 entries, including NA, NaN, and Inf.

```
R is.na(x=qux)
[1] TRUE FALSE FALSE TRUE FALSE FALSE TRUE FALSE TRUE TRUE
[13] TRUE FALSE
```

As you can see, is.na flags the corresponding NA entries in qux as TRUE. But this is not all—note that it also flags elements 7 and 14, which are NaN, not NA. Strictly speaking, NA and NaN are different entities, but they are practically the same since there is almost nothing you can do with either value. Using is.na labels as TRUE, allowing the user to remove or recode at the same time.

If you want to identify NA and NaN entries separately, you can use is.nan in conjunction with logical operators. Here’s an example:

```
R which(x=is.nan(x=qux))
[1] 7 14
```

This identifies the indices whose elements elements are specifically NaN. If you want to identify NA entries only, try the following:

```
R which(x=(is.na(x=qux))&is.nan(x=qux))
[1] 4 11
```

This identifies entries only for the NA entries (by checking for entries where is.na is TRUE AND is.nan is NOT TRUE).