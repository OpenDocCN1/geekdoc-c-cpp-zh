Functions on new data types can use data constructors as patterns, as in ML:

```
flatten:: BST a -> [a]
flatten Nil = []
flatten (Node val left right) =
    (flatten left) ++ [val] ++ (flatten right)
```

Note that the definition is preceded by the type of the flatten function. The type specifier is permitted, although not required. A type specifier can be used to resolve ambiguities or restrict the type of the function beyond what Hindley-Milner type checking would infer. The use of this option is similar to the way ML allows the types of the parameters and returned types to be specified within the definition itself, something not allowed in Haskell98.

Haskell also has a special notation for operations that are applied over lists, called list comprehensions. List comprehensions are designed to look like set definitions in mathematics. For example, if we wanted to square a list of integers, we could write the following:

```
square_list lis = [ x * x | x <- lis ]
```

This is really just syntactic sugar for map (\x -> x * x) lis, but it can make programming with lists even easier and more transparent. The notation can also be extended to include Boolean conditions, such as:

```
square_list_positive lis = [ x * x | x <- lis, x > 0 ]
```

which is also syntactic sugar for map (\x -> x * x) (filter (>0) lis), where filter is a predefined list function defined as follows:

```
filter:: (a -> Bool) -> [a] -> [a]
filter pred [] = []
filter pred (h:t) =
    if pred h then h : filter pred t else filter pred t
```

As another example of the use of list comprehensions, a highly compact definition for quicksort can be given (using the first element of a list as the pivot):

```
qsort [] = []
qsort (h:t) = qsort [x | x <- t, x <= h] ++
    [h] ++ qsort [x | x <- t, x > h]
```

# 3.5.3 Lazy Evaluation and Infinite Lists

Because Haskell is a lazy language, no value is computed unless it is actually needed for the computation of a program. Thus, given the definition:

```
f x = 2
```