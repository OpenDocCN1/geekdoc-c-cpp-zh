Note that variable `a` was never defaulted when a function call was made unless variable `b` was first defaulted. It's impossible to provide a value for the last parameter and take any default values for previous parameters.

# Restrictions on Default Arguments

If default arguments are used, the right-most value must be given a default value before arguments to its left are defaulted. Only trailing arguments can be defaulted.

After the first default argument, all subsequent arguments must also include default arguments.

```
void foo(int width, float v = 3.14159, char q = 'S');
```

In this example, `width` could not be declared anywhere else, i.e., it could not be placed between `v` and `q` or at the end of the argument list. When calling `foo()`, a program must specify a width. You always have to supply argument values for a function's normal parameters

+   - Default arguments appear only in the function prototype (declaration), not in the function definition header.
+   - Default arguments can only be declared once.
+   - Default arguments must be included in header files that are included in all files that use the defaulted notation.
+   - Default arguments must be passed by value, not reference or pointer.
+   - Default argument values may be literal values or constant definitions. They may not be variables:

```
void foo(int x, int y = n); // invalid
```

So default arguments can be useful when function calls typically need to supply only some, but not all arguments.