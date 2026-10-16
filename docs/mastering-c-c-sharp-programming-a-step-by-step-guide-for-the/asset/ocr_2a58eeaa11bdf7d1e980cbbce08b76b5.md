+   - The * operator – used for pointer indirection
+   - The -> operator – used for accessing struct members via a pointer
+   - The [] operator – used for indexing pointers
+   - The & operator – used for getting variable addresses
+   - The ++ and – operators – used for incrementing and decrementing pointers
+   - The + and – operators – used for arithmetic on pointers
+   - The !=, ==, <=, >=, < and > operators – used for pointer comparison
+   - The stackalloc operator – used for allocating memory from the stack
+   - The fixed statement – used for a temporary fix on a variable so we can obtain the address

# Fixed And Moveable Variables

Fixed statements and address-of operators split the variables into two separate categories called fixed variables and moveable variables respectively.

A fixed variable will live in those storage locations that the garbage collector doesn’t touch. Fixed variables include value parameters, local variables, and those created by dereferencing pointers. The moveable variable will live in the storage locations that the garbage collector will either dispose of or relocate. Moveable variables include array elements and object fields.

The address-of operator (&) will allow us to get a fixed variable address without any restrictions. However, as a moveable variable can be disposed of or relocated, we need to use a fixed statement to get the address and the address will only be valid for the lifetime of the fixed statement.

A fixed variable is:

+   - A variable that comes from a simple_name which is referencing value parameters or local variables. The exception is if an anonymous function captures the variable.