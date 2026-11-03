# Pointer Declaration Style

Pointer variables are declared similarly as normal variables except for the addition of the unary * operator. This symbol can appear anywhere between the type name and the pointer variable name. Programmers use the following styles:

```
int * p;    /* style 1 */
int *p;     /* style 2 */
int * p;    /* style 3 */
```

However, the style2 is becoming increasingly popular due to the following reasons:

+   1. This style is convenient to have multiple declarations in the same statement. Example:
+      int *p, x, q;
+   2. This style matches with the format used for accessing the target values. Example:
+      int x, *p, y;
+      x = 10;
+      p = &x;
+      y = *p;    /* accessing x through p */
+      *p = 20;   /* assigning 20 to x */

We use in this book the style 2, namely, int *p;

# 6.5 INITIALIZATION OF POINTER VARIABLES

The process of assigning the address of a variable to a pointer variable is known as initialization. As pointed out earlier, all uninitialized pointers will have some unknown values that will be interpreted as memory addresses. They may not be valid addresses or they may point to some values that are wrong. Since the compilers do not detect these errors, the programs with uninitialized pointers will produce erroneous results. It is therefore important to initialize pointer variables carefully before they are used in the program.

Once a pointer variable has been declared we can use the assignment operator to initialize the variable.
Example:

```
int quantity;
int *p;        /* declaration */
p = &quantity; /* initialization */
```

We can also combine the initialization with the declaration. That is, int *p = &quantity; is allowed. The only requirement here is that the variable quantity must be declared before the initialization takes place. Remember, this is an initialization of p and not *p.