the specific vector to obtain all possible indexes for extracting a particular element in the vector:

```
R> 1:myvec.len
[1]  1  2  3  4  5  6  7  8  9 10
```

You can also delete individual elements by using negative versions of the indexes supplied in the square brackets. Continuing with the objects myvec, foo, bar, and myvec.len as defined earlier, consider the following operations:

```
R> myvec[-1]
[1]  -2.3    4.0    4.0    4.0    6.0    8.0   10.0 40221.0  -8.0
```

This line produces the contents of myvec without the first element. Similarly, the following code assigns to the object baz the contents of myvec without its second element:

```
R> baz <- myvec[-2]
R> baz
[1]  5  4  4  4  6  8  10 40221  -8
```

Again, the index in the square brackets can be the result of an appropriate calculation, like so:

```
R> qux <- myvec[-(myvec.len-1)]
R> qux
[1]  5.0 -2.3  4.0  4.0  4.0  6.0  8.0 10.0 -8.0
```

Using the square-bracket operator to extract or delete values from a vector does not change the original vector you are subsetting unless you explicitly overwrite the vector with the subsetted version. For instance, in this example, qux is a new vector defined as myvec without its second-to-last entry, but in your workspace, myvec itself remains unchanged. In other words, subsetting vectors in this way simply returns the requested elements, which can be assigned to a new object if you want, but doesn’t alter the original object in the workspace.

Now, suppose you want to piece myvec back together from qux and bar. You can call something like this:

```
R> c(qux[-length(x=qux)],bar,qux[length(x=qux)])
 [1]  5.0  -2.3   4.0   4.0   4.0   6.0   8.0  10.0 40221.0
[10] -8.0
```

As you can see, this line uses c to reconstruct the vector in three parts: qux[-length(x=qux)], the object bar defined earlier, and qux[length(x=qux)]. For clarity, let’s examine each part in turn.