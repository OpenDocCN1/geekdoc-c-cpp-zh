This call returns the new list (A B (C D)).

ML has lists and list operations, although their appearance is not like those of Scheme. Lists are specified in square brackets, with the elements separated by commas, as in the following list of integers:

```
```
[5, 7, 9]
```
```

`{}` is the empty list, which could also be specified with `nil`.

The Scheme `cons` function is implemented as a binary infix operator in ML, represented as `::`. For example,

```
```
3 :: [5, 7, 9]
```
```

returns the following new list: `[3, 5, 7, 9]`.

The elements of a list must be of the same type, so the following list would be illegal:

```
```
[5, 7.3, 9]
```
```

ML has functions that correspond to Scheme's `CAR` and `CDR`, named `hd` (head) and `tl` (tail). For example,

```
```
hd [5, 7, 9] is 5
tl [5, 7, 9] is [7, 9]
```
```

Lists and list operations in Scheme and ML are more fully discussed in Chapter 15.

Lists in F# are related to those of ML with a few notable differences. Elements of a list in F# are separated by semicolons, rather than the commas of ML. The operations `hd` and `tl` are the same, but they are called as methods of the `List` class, as in `List.hd [1; 3; 5; 7]`, which returns 1. The `cons` operation of F# is specified as two colons, as in ML.

Python includes a list data type, which also serves as Python's arrays. Unlike the lists of Scheme, Common Lisp, ML, and F#, the lists of Python are mutable. They can contain any data value or object. A Python list is created with an assignment of a list value to a name. A list value is a sequence of expressions that are separated by commas and delimited with brackets. For example, consider the following statement:

```
```
myList = [3, 5.8, "grape"]
```
```

The elements of a list are referenced with subscripts in brackets, as in the following example:

```
```
x = myList[1]
```
```

This statement assigns 5.8 to `x`. The elements of a list are indexed starting at zero. List elements also can be updated by assignment. A list element can be deleted with `del`, as in the following statement:

```
```
del myList[1]
```
```