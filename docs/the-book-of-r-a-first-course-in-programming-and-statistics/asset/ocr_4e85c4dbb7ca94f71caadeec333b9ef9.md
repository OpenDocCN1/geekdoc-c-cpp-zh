The first line checks whether the entries in foo are equal to the corresponding entries in bar, which is true only for the fifth and ninth entries. The returned vector will contain a logical result for each pair of elements, so it will be the same length as the vectors being compared. The second line compares foo and bar in the same way, this time checking whether the entries in foo are less than the entries in bar. Contrast this result with the third comparison, which asks whether entries are less than or equal to one another. Finally, the fourth line checks whether foo’s members are less than or equal to bar, when the elements of bar are increased by 10. Naturally, the results are all TRUE.

Vector recycling also applies to logicals. Let’s use foo from earlier, along with a shorter vector, baz.

```
R> baz <- foo[c(10,3)]
R> baz
[1] 3 1
```

Here you create baz as a vector of length 2 comprised of the 10th and 3rd elements of foo. Now consider the following:

```
R> foo>baz
[1] FALSE  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE  TRUE
```

Here, the two elements of baz are recycled and checked against the 10 elements of foo. Elements 1 and 2 of foo are checked against 1 and 2 of baz, elements 3 and 4 of foo are checked against 1 and 2 of baz, and so on. You can also check all the values of a vector against a single value. Here’s an example:

```
R> foo<3
[1] FALSE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE
```

This is a typical operation when handling data sets in R.
Now let’s rewrite the contents of foo and bar as 5 × 2 column-filled matrices.

```
R> foo.mat <- matrix(foo,nrow=5,ncol=2)
R> foo.mat
     [,1] [,2]
[1,]    3    2
[2,]    2    1
[3,]    1   -1
[4,]    4    0
[5,]    1    3
R> bar.mat <- matrix(bar,nrow=5,ncol=2)
R> bar.mat
     [,1] [,2]
[1,]    4    0
```