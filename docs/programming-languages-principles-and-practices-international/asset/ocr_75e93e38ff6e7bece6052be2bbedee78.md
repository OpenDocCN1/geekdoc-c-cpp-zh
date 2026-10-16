A traversal function for binary search trees that prints out the string nodes is as follows:

```
> fun print_tree Nil = () |
    print_tree (Node (data,left,right)) =
        ( print_tree left;
          output(stdOut,data);
          output(stdOut,"\n");
          print_tree right);
val print_tree = fn : vector BST -> unit
> print_tree tree;
cow
dog
horse
yak
zebra
val it = () : unit
```

# 3.3.3 Higher-Order Functions and Currying in ML

Higher-order functions and expressions whose values are functions are as useful in ML as in Scheme.

ML’s keyword for a function expression, fn, is used with a special arrow (an equals followed by a greater than) to indicate the body of the function. For example:

```
> fn x => x * x;
val it = fn : int -> int
> (fn x => x * x) 4;
val it = 16 : int
```

A fn expression can be used to build anonymous functions and function return values. Indeed a fun definition is, as in Scheme, just syntactic sugar for the use of a fn expression:

```
fun square x = x * x;
```

is equivalent to:

```
val square = fn x => x * x;
```

One difference between ML and Scheme is that, if we use an ML fn expression to declare a recursive function, we must add the rec keyword in ML (similar to a Scheme letrec):

```
val rec fact = fn n => if n = 0 then 1 else n * fact (n - 1);
```