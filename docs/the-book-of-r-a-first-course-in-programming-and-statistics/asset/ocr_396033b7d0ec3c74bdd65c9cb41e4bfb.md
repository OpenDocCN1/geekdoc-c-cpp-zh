For example, to find the geometric mean of the data 4.3, 2.1, 2.2, 3.1, calculate the following:

```
$$\bar{g} = (4.3 \times 2.1 \times 2.2 \times 3.1)^{1/4} = 61.5846^{0.25} = 2.8$
```

(This is rounded to 1 d.p.p.)

Write a function named geolist that can search through a specified list and compute the geometric means of each member per the following guidelines:

+   Your function must define and use an internal helper function that returns the geometric mean of a vector argument. Assume the list can only have numeric vectors or matrices as its members. Your function should contain an appropriate loop to inspect each member in turn.

+   If the member is a vector, compute the geometric mean of that vector, overwriting the member with the result, which should be a single number.

+   If the member is a matrix, use an implicit loop to compute the geometric mean of *each row* of the matrix, overwriting the member with the results.

+   The final list should be returned to the user.

Now, as a quick test, check that your function matches the following calls:

```
i.
> foo <- list(1:3,matrix(c(3.3,3.2,2.8,2.1,4.6,4.5,3.1,9.4),4,2), matrix(c(3.3,3.2,2.8,2.1,4.6,4.5,3.1,9.4),2,4))
> geolist(foo)
[[1]]
[1] 1.817121
[[2]]
[1] 3.896152 3.794733 2.946184 4.442972
[[3]]
[1] 3.388035 4.106080
```

```
ii.
> bar <- list(1:9,matrix(1:9,1),matrix(1:9,9,1),matrix(1:9,3))
> geolist(bar)
[[1]]
[1] 4.147166
[[2]]
[1] 4.147166
```