Here, calling attributes returns a list with one member: dim. Of course, you can retrieve the contents of dim with attributes(foo)$dim, but if you know the name of an attribute, you can also use attr:

```
R attr(x=foo,which="dim")
[1] 3 3
```

This function takes the object in x and the name of the attribute as specified as character strings in R. Recall that many things even more convenient, the most common attributes have their own functions (usually named after the attribute) to access the corresponding value. For the dimensions of a matrix, you've already seen the function dim:

```
R dim(foo)
[1] 3 3
```

These attribute-specific functions are useful because they allow access to implicit attributes, which, while still controllable by the user, as a matter of necessity. The names and levels functions mentioned earlier are both attribute-specific functions.
Explicit attributes are often optional; if they aren't specified, they are NULL. For example, when building a matrix with the matrix function, you can use the argument dimnames to annotate the rows and columns with names. You pass dimnames a list up to two members, both character vectors of the appropriate lengths—the first giving row names and the second giving column names. Let's define the matrix bar as follows:

```
R bar <- matrix(data=1:9,nrow=3,ncol=3,dimnames=list(c("A","B","C"),
c("D","E","F")))

```

```
R bar
D E F
A 1 4 7
B 2 5 8
C 3 6 9
```

Because the dimension names are attributes, the dimnames appear when you call attributes(bar).

```
R attributes(bar)
$dim
[1] 3 3
```

```
$dimnames
$dimnames[[1]]
[1] "A" "B" "C"
```

```
$dimnames[[2]]
[1] "D" "E" "F"
```