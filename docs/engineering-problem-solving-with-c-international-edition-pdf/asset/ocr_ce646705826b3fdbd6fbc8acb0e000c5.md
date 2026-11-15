# C++ Statement Summary

Pointer declaration:

General Form:

data type *identifier [,*identifier];

Example:

int *ptr_1;
double a, *ptr_2=&a;

Dynamic memory allocation:

General Form:

pointer_object = new datatype;

Example:

ptr = new double;

Deallocation of dynamic memory:

General Form:

delete pointer_object;

Dynamic array memory allocation:

arr_ptr = new double[100];

Deallocation of dynamic array:

General Form:

delete pointer_object[];

+   Notes
+   
+   1. Choose identifiers for pointers that clearly indicate that the identifiers are associated with pointer objects.
+   2. If a pointer is not initially assigned to a memory location, give it a value of NULL to indicate that it has not yet been assigned.

+   Debugging Notes
+   
+   1. Be sure that a program initializes an object before using its value in other statements.
+   2. Be sure that a pointer object is initialized before it is used to reference a value.
+   3. The actual parameter that corresponds to a pointer argument in a function must be an address or a pointer.