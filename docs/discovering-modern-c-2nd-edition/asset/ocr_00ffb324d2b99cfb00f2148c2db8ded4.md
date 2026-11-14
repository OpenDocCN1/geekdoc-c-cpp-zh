function. However, we can do this using `decltype` for an expression with the function arguments. To this end, we have been granted permission to move the declaration of the `return` type behind the arguments.

The two vectors may have different types and the resultant vector yet another one. With the expression `decltype(v1[0] + v2[0])` we deduce what type we get when we add elements of both vectors. This type will be the element type for our resultant vector.

An interesting aspect of `decltype` is that it only operates on the type level and does not evaluate the expression given as an argument. Thus, the expression from the previous example does not cause an error for empty vectors because `v1[0]` is not performed and only its type is deduced.

The two features `auto` and `decltype` differ not only in their application; the type deduction is also different. While `auto` follows the rules of function template parameters and often drops reference and `const` qualifiers, `decltype` takes the expression type as it is. For instance, if the function `f` in our introductory example returned a reference, the variable `a` at the beginning of this sub-section would be a reference. A corresponding `auto` variable would be a value.

As long as we mainly deal with intrinsic types, we get along without automatic type detection. But with advanced generic and meta-programming, we can greatly benefit from these extremely powerful features. Useful also is the counterpart of `decltype`: `declval`. This is a tool to create an object of any type, which can then be used to deduce the type of an expression thereof. We will demonstrate this in Section 3.5.5 and in some of the following subsections.

# C++11 3.4.3 decltype(auto)

This new feature closes the gap between `auto` and `decltype`. With `decltype(auto)`, we can declare `auto` variables that have the same type as with `decltype`. The following two declarations are identical:

Click here to view code image

```
decltype(expr) v = expr; // redundant + verbose when expr
long
decltype(auto) v = expr; // Ahh! Much better.
```