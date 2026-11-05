+   - The binary + and - operators may be used to perform pointer arithmetic (§22.6.7).
+   - The ==, !=, <, >, <=, and >= operators may be used to compare pointers (§22.6.8).
+   - The stackalloc operator may be used to allocate memory from the call stack (§22.9).
+   - The fixed statement may be used to temporarily fix a variable so its address can be obtained (§22.7).

# 22.4 Fixed and moveable variables

The address-of operator (§22.6.5) and the fixed statement (§22.7) divide variables into two categories: Fixed variables and moveable variables.

Fixed variables reside in storage locations that are unaffected by operation of the garbage collector. (Examples of fixed variables include local variables, value parameters, and variables created by dereferencing pointers.) On the other hand, moveable variables reside in storage locations that are subject to relocation or disposal by the garbage collector. (Examples of moveable variables include fields in objects and elements of arrays.)

The & operator (§22.6.5) permits the address of a fixed variable to be obtained without restrictions. However, because a moveable variable is subject to relocation or disposal by the garbage collector, the address of a moveable variable can only be obtained using a fixed statement (§22.7), and that address remains valid only for the duration of that fixed statement.

In precise terms, a fixed variable is one of the following:

+   - A variable resulting from a simple_name (§11.7.4) that refers to a local variable, value parameter, or parameter array, unless the variable is captured by an anonymous function (§11.16.6.2).
+   - A variable resulting from a member_access (§11.7.6) of the form V.I, where V is a fixed variable of a struct_type.
+   - A variable resulting from a pointer_indirection_expression (§22.6.2) of the form *P, a pointer_member_access (§22.6.3) of the form P->I, or a pointer_element_access (§22.6.4) of the form P[E].

All other variables are classified as moveable variables.

A static field is classified as a moveable variable. Also, a ref or out parameter is classified as a moveable variable, even if the argument given for the parameter is a fixed variable. Finally, a variable produced by dereferencing a pointer is always classified as a fixed variable.

# 22.5 Pointer conversions

# 22.5.1 General

In an unsafe context, the set of available implicit conversions (§10.2) is extended to include the following implicit pointer conversions:

+   - From any pointer_type to the type void*.
+   - From the null literal (§6.4.5.7) to any pointer_type.

Additionally, in an unsafe context, the set of available explicit conversions (§10.3) is extended to include the following explicit pointer conversions: