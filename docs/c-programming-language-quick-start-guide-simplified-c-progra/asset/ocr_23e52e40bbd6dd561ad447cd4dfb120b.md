the other hand are dependent on their blocks that can be molded for use by programmers.

Let us use this facility to provide a variable that is global to a family of functions but, at the same time, is private to the file.

Another use of static is as a storage class to specify function definitions and prototypes.

This use causes the scope of the function to be restricted. Static functions are visible only within the file in which they are defined. Unlike ordinary functions, which can be accessed from other files, a static function is available throughout its own file, but no other.

# 3.5 Default Initializations

In C, both external variables and static variables that are not assigned any values at the time of declaration are automatically initialized with 0. This default initialization is applicable on arrays, strings, pointers, structures and union.

In contrast to this, automatic and register variables are not automatically initialized by the system. This means compiler either generates an error or uses a garbage value if you