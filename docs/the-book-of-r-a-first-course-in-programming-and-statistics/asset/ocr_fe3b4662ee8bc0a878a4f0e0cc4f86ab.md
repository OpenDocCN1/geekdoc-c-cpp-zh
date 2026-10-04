Now if you check whether the argument was supplied using NA, you
might call this:

```
R> is.na(x=opt.arg)
[1] FALSE FALSE FALSE
```

The position-specific nature of NA means that this is element-wise and returns an answer for each value in opt.arg. This is problematic because you want only a single answer—is opt empty or is it supplied? This is when NULL comes to the party.

```
R> is.null(x=opt.arg)
[1] FALSE
```

Quite clearly opt.arg is not empty, and the function can proceed necessary. If the argument is empty, using NULL over NA for the check is again better for these purposes.

```
R> opt.arg <- c(NA,NA,NA)
R> is.na(x=opt.arg)
[1] TRUE TRUE TRUE
```

```
R> opt.arg <- c(NULL,NULL,NULL)
R> is.null(x=opt.arg)
[1] TRUE
```

As noted earlier, filling a vector with NULL isn’t usual practice; it’s done just here for illustration. But usage of NULL is far from specific to this particular example. It’s commonly used throughout both ready-to-use and user-contributed functionality in R.

The empty NULL has an interesting effect if it’s included in arithmetic or relational comparisons.

```
R> NULL+53
numeric(0)
R> 53<=NULL
logical(0)
```

Rather than NULL as you might expect, the result is an “empty” vector of a type determined by the nature of the operation attempted. NULL typically dominates any arithmetic, even if it includes other special values.

```
R> NaN+NA/Inf
numeric(0)
```

NULL also occurs naturally when examining lists and data frames. For example, define a new list foo.