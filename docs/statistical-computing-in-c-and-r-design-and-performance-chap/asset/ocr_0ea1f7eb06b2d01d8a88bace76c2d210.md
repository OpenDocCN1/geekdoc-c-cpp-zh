# AN EXAMPLE

+   [1] "nMach"
> setGetGeneric("nSet", function(object) standardGeneric("nSet")
> [1] "nSet"
> setMethod("nSet", signature = "g5List", function(object)
> object@nSet
> [1] "nSet"

The constructor for the g5List class was applied to the data in our guess5.txt file. One of the properties of the g5List object is applied below.

```
> g5ListObj <- g5List("guess5.txt")
> ndraw(g5ListObj)
> [1] 100
> nMach(g5ListObj)
> [1] 53
> nSet(g5ListObj)
> [1] 4 8 12 14 12 12 7 8 11
> g5ListObj[[2]]
```

```
An object of class "g5"
Slot "drawDate":
[1] "1952-01-21"
```

```
Slot "mName":
[1] "B"
```

```
Slot "sNo":
[1] 4
```

```
Slot "Day":
[1] "M"
```

```
Slot "data":
[1,] [2] [3] [4] [5]
[1,] 11 9 23 10 20
[2,] 32 7 16 18 40
[3,] 38 35 26 36 19
[4,] 24 14 39 1 19
[5,] 35 1 3 7 28
[6,] 30 18 1 3 24
[73 31 6 16 9 3
[8,] 16 3 9 25
[99 12 4   3 28
[10,] 33 39 4 38 29
```

```
> temp <- g5ListObj[[2]]
> g5ListObj[[2]] <- g5ListObj[[1]]
> g5ListObj[[2]] <-@drawDate
[1] "1952-01-17"
> g5ListObj[[2]] <- temp
> g5ListObj[[2]] <-@drawDate
[1] "1952-01-21"
```

The sum of the values for nMach and nSet should be as we find to be. A check with results from Section 5.6 also indicates the second g5 agrees with the one in the guess5.txt file. A test of our replacement version of [[ successfully overwrites the second draw with the first and then reverses the operation. The task remains of actually analyzing the Guess data, and similar to what was