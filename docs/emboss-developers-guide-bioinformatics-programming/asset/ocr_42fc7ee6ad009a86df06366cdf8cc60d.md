values, can be difficult to understand. Review your code and establish whether the variable really needs to be in the object or whether it's best moved somewhere else.

# C.1.6 Avoid redundancy

Where two or more different objects share common elements there is likely scope for removing redundancy throughout your code. Consider whether a new object encapsulating the common elements would make your code easier to understand and maintain.

# C.1.7 Manage your variables

Functions with very long lists of variables are difficult to understand and maintain. Where a group of variables are always used together, consider encapsulating them in a new object, especially where the group occurs elsewhere in your code.

# C.1.8 Long functions

Big functions are difficult to understand. Smaller functions are easier to document and therefore easier for the programmer to identify. Functionality split into smaller functions is more likely to be reused. Consider breaking big functions down into smaller ones. If necessary, retain the function with the original name which can call the new, smaller functions. Do not overdo it though and try to avoid too many levels of function calls (see Section C.1.10, ‘Nesting of functions’).

# C.1.9 Long parameter lists

Functions with many parameters are difficult to understand, use and maintain. Where possible, you should pass an object pointer rather than the individual elements of a single object. If the parameters do not belong to an object, consider defining a new object to encapsulate them and pass a pointer to that instead.

# C.1.10 Nesting of functions

Code which uses deeply nested chains of functions can be extremely difficult to understand. Design your code to avoid this.

# C.2 Code layout

# C.2.1 Application code layout

Use the following order for laying out the application C source code:

+   1. Application standard header
+   2. Inclusion of system header files
+   3. Inclusion of local header files