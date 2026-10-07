# Chapter 5: Parameters and Methods

+   * The parameter array is not necessarily the only parameter on a method.
* The parameter array must be the last parameter in the method declaration. Since only the last parameter may be a parameter array, a method cannot have more than one parameter array.
* The caller can specify zero arguments that correspond to the parameter array parameter, which will result in an array of zero items being passed as the parameter array.
* Parameter arrays are type-safe: The arguments given must be compatible with the element type of the parameter array.
* The caller can use an explicit array rather than a comma-separated list of arguments.
* If the target method implementation requires a minimum number of parameters, those parameters should appear explicitly within the method declaration, forcing a compile error instead of relying on runtime error handling if required parameters are missing. For example, if you have a method that requires one or more integer arguments, declare the method as int Max(int first, params int[] operands) rather than as int Max(params int[] operands) so that at least one value is passed to Max().

Using a parameter array, you can pass a variable number of arguments of the same type into a method. The section "Method Overloading," which appears later in this chapter, discusses a means of supporting a variable number of arguments that are not necessarily of the same type.

> > Guidelines DO use parameter arrays when a method can handle any number—including zero—of additional arguments.

By the way, a path Combine() function is a contrived example since, in fact, System.IO.Path.Combine() is an existing function that is overloaded to support parameter arrays.