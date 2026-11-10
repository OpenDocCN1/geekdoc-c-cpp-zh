```
Here is a slightly more complex example that uses the function square:
```lisp
(defun hypotenuse (a b)
  (sqrt (+ (square a) (square b))))

The function to find the length is defined
as (defun list-length(x)
     (if (null x)
         0
         (+ 1 (length(rest x)))))
```
```

If the list is null (i. e., empty), then the length is 0. Otherwise, the length is 1 plus the length of the list with the first element removed. Since Lisp functions are stored as data, it is very easy to write functions that define and manipulate other functions. This is exactly what genetic programming does. It is relatively easy to write a simple genetic programming package in Lisp.

# 14.4 Functionality of Genetic Programming

The operational steps such as creating an individual, creating a random population, fitness test, functions and terminals, the genetic operations, selection functions, crossover operation, mutation and user decisions of a typical genetic programming are described in this section (Figure 14.3).

# 14.4.1 Generation of an Individual and Population

The basic elements of an individual are its genes. These genes are combined together to form a program. An individual’s program is a tree-like structure and as such there are two types of genes: *functions* and *terminals*.

Terminals are defined as leaves or nodes without branches and functions are defined as the nodes with children. The node’s children provide the arguments for the function. In the example (Figure 14.4) there are three functions (−, + and /) and four terminals (x, 3, y and 6). The / (division) function requires two arguments: the return value of “−” and the return value of the subtree whose root is “+”. The − (subtraction) function takes two arguments which are provided by x and 3. The + (addition) function also takes two arguments which are provided by y and 6.