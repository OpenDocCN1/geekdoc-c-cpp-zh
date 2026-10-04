```
}
matlist
```

c. In R, store the following $4 \times 4 \times 2 \times 3$ array as the object qux:
R> qux <- array(96:1,dim=c(4,4,2))

That is, it is a four-dimensional array comprised of three blocks, each block being an array made up of two layers of $4 \times 4$ matrices. Then, do the following:

+   i. Write an implicit loop that obtains the diagonal elements of all second-layer matrices to only produce the matrix:

| [1] | [2] | [3] |
| [1] | 80 | 48 | 16 |
| [2] | 75 | 43 | 11 |
| [3] | 70 | 38 | 6 |
| [4] | 65 | 33 | 1 |

+   ii. Write an implicit loop that will return the dimensions of the three matrices formed by accessing the fourth column of every matrix in qux, regardless of layer or block, wrapped by another implicit loop that finds the row sums of that returned structure, resulting simply in the following vector:

| [1] | 12 | 6 |

# 10.3 Other Control Flow Mechanisms

To round off this chapter, you'll look at three more control flow mechanisms: break, next, and repeat. These mechanisms are often used in conjunction with the loops and if statements you've seen already.

# 10.3.1 Declaring break or next

Normally a for loop will exit only when the loopindex exhausts the loopvector, and a while loop will exit only when the loopcondition evaluates to FALSE. But you can also preemptively terminate a loop by declaring.

For example, say you have a number, foo, that you want to divide by element in a numeric vector.

```
R> foo <- 5
R> bar <- c(2,3,1,1,4,0,4,1,3)
```

Furthermore, let's say you want to divide foo by element by element but to halt execution if one of the results evaluates to Inf (which will happen if dividing by zero). To do this, you can check each iteration with the