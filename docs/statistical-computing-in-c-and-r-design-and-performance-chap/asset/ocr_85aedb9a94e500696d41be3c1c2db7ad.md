# 346 TRUE

# ABSTRACT DATA STRUCTURE

```
[1] push(mQ, 1)
> isNotEmpty(mQ)
> FALSE
[1] push(mQ, matrix(rnorm(16), 4, 4))
> push(mQ, expression(1 + pi))
> push(mQ, 1:5)
> print(pop(mQ))
[1] i
> top(mQ)
```

| [1] | [2] | [3] | [4] |
|---|---|---|--|
| [1] | -0.5604756 | 0.1292877 | -0.6868529 | 0.4007715 |
| [2] | -0.2301777 | 1.7150560 | -0.4456626 | 0.1106827 |
| [3] | 1.55870831 | 0.4609162 | 1.2240818 | -0.5558411 |
| [4] | 0.07505839 | -1.2650512 | 0.3598138 | 1.7869131 |

The output is consistent with the first-in-out behavior that is expected from a queue object.
The databases created with createS and createQ continue to exist beyond the end of the R session they were created. To access them in a future session one uses the initS or initQ functions. To demonstrate we ended our R session and started a new one in the same working directory with the results

```
library(filehash)
filehash: Simple key-value database (2.1 2010-02-04)
mS <- initStack("myStack")
> top(mQ)
expression(1 + pi)
mQ <- initQ("myQueue")
> invisible(pop(mQ))
> top(mQ)
expression(1 + pi)
```

The filehash library was loaded and the existing databases mStack and myQueue were connected to stack and queue objects. A preview of the top on stack remains as it is the same. Then the pop function was used to return the matrix from the queue. The command was "wrapped" in the invisible function to suppress the printed output which would have otherwise produced. The next component of the queue is found to be the expected expression.

# 9.2.4 Hash tables

A hash table is a data structure that solves the problem of efficiently mapping a sparse set of keys, not not integers, into an array while conserving storage. Knuth (1998b) is one of the best references for hashing. An overview of the topic from a C++ perspective is provided by Sedgewick.

The main ideas of a hash table are the hash function and a mechanism for collision resolution. The hash function is a mapping: K -> Nm, where K is the key space (of all possible keys) and Nm = {1,...,m} for some integer m. A given key is said to hash to h(k). The data is stored in an array A = [A[1],...,A[m]] indexed by Nm with the consequence that m is the size of the table.

To insert an object with a key a into the hash table, first compute the value h(a.key), and then there is an already object stored in A[h(a.key)], either the object has already been inserted into the table or there is collision where two different keys map to the same slot in the table. Collisions are generally impossible to