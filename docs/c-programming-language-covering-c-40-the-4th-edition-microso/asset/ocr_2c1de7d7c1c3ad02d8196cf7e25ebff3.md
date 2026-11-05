lengths are inferred from the number of elements in each of the corresponding nesting levels of the array initializer. Thus the expression

```
`new int[,] {{0, 1}, {2, 3}, {4, 5}}`
```

exactly corresponds to

```
`new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}`
```

An array creation expression of the third form is referred to as an *implicitly typed array creation expression*. It is similar to the second form, except that the element type of the array is not explicitly given, but determined as the most common type (§7.5.2.14) of the set of expressions in the array initializer. For a multidimensional array—that is, one where the *rank-specifier* contains at least one comma—this set comprises all *expressions* found in nested *array-initializers*.

Array initializers are described further in §12.6.

The result of evaluating an array creation expression is classified as a value—namely, a reference to the newly allocated array instance. The runtime processing of an array creation expression consists of the following steps:

+   - The dimension length expressions of the *expression-list* are evaluated in order, from left to right. Following evaluation of each expression, an implicit conversion (§6.1) to one of the following types is performed: int, uint, long, ulong. The first type in this list for which an implicit conversion exists is chosen. If evaluation of an expression or the subsequent implicit conversion causes an exception, then no further expressions are evaluated and no further steps are executed.
+   - The computed values for the dimension lengths are validated as follows. If one or more of the values are less than zero, a System.OverflowException is thrown and no further steps are executed.
+   - An array instance with the given dimension lengths is allocated. If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown and no further steps are executed.
+   - All elements of the new array instance are initialized to their default values (§5.2).
+   - If the array creation expression contains an array initializer, then each expression in the array initializer is evaluated and assigned to its corresponding array element. The evaluations and assignments are performed in the order the expressions are written in the array initializer—in other words, elements are initialized in increasing index order, with the rightmost dimension increasing first. If evaluation of a given expression or the subsequent assignment to the corresponding array element causes an exception, then no further elements are initialized (and the remaining elements will thus have their default values).