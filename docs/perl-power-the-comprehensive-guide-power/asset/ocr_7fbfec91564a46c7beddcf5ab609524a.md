block. You call the `print()` function to print the contents of the tag. You use the `$ML` and `$NL` identifiers to position the text for display.

# Functions That Accept Arguments

You can create functions that handle one or more arguments. To accomplish this, you make use of the *argument array* that is associated with every Perl function. You identify the argument array using a special array notation, which consists of the array sign followed by a single underscore:

```
`@_`
```

You can use the argument array in a variety of ways, but at least initially passing it the values it contains to an array you name in the context of your function makes the flow logic in your function clearer. For this reason, in Figure 12.8, the contents of `@_` are passed to `@functionArray`. This array then contains all the values passed to the function through the argument array (`@_`).

When you define a function that accepts parameters, you do not have to process the argument array in such an explicit manner. Instead, you can use the argument array directly, with no intermediate array (as with `@functionArray`).

In Figure 12.8, the programmer passes `argument1` and `argument2` to the `showTwo()` function. In the definition of the function, you see that the contents of the argument array (`@_`) are assigned to a local array (`@functionArray`). Then, to use the values in the local array, the two print functions take as their argument the first (0) and second (1) elements of `@functionArray` (used in its scalar form).

![](bbox=[0.15, 0.619, 0.687, 0.823])

Passing an argument to a function involves passing a value from the general scope of a program to the local scope of the function. Listing12_02 explores the use of arguments with two