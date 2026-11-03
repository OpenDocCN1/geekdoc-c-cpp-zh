```
```
} return 0;
}
```
```

Modifications to exercise: Again, the same amendments proposed in the two previous programs can be implemented.

# ## Divide and conquer

The idea of splitting a set into two halves and, starting from there, to get to what you want is not exclusive of the *binary search* algorithm. It is the center of one of the most important techniques of programming: the technique of division and conquest (*divide and conquer*) transplanted from a famous strategy of the generals on the battlefield. When we separate the body of a program into modules, whether functions, whether procedures, we are using this famous technique.

On these algorithms presented just above, the reader needs to be reminded that the default file *stdlib.h* contains the *qsort()* (quick sort) and *bsearch()* (binary search) functions. They are algorithms important too much to get out of the standard library. And they are both too important to be not explicitly within this book, so that they can be manipulated by you, reader.

# ## Flowchart

In the era of punch cards it was customary to draw the flow diagram, or flowchart, before writing a program. This was because the *goto* statement had everyday use, unlike what occurred later, and the major problems of involuntary interruption of flow or endless loop were the possible wrong use of that statement. The practice of avoiding it dismissed the use of the diagram, but you should know an example.

Let us look at a mini-program to add the square roots of the integers from 1 to 20.

```
```
#include <stdio.h>
#include <math.h>

main()
```
```