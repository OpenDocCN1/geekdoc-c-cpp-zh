+   - A pointer with the value NULL points to nothing. NULL is a symbolic constant with the value 0 and is defined in the header <stddef.h> (and several other headers, such as <stdio.h>).
+   - Initializing a pointer to 0 is equivalent to initializing it to NULL. The constant NULL is preferred because it emphasizes that you’re initializing a pointer rather than a variable that stores a number. When 0 is assigned, it’s first converted to a pointer of the appropriate type. The value 0 is the only integer value that can be assigned directly to a pointer variable.
+   - Assigning a variable’s address to a pointer is discussed in Section 7.3. Initialize pointers to prevent unexpected results.

ERR ⊗

# Self Check

1 (True/False) The definition:

```
int *countPtr, count;
```

specifies that countPtr and count are of type int *—each is a pointer to an integer. Answer: False. Actually, count is an int, not a pointer to an int. The * applies only to countPtr and does not distribute to the other variable(s) in the definition.

2 (Multiple Choice) Which of the following statements is false?

+   a) A pointer may be initialized to NULL, 0 or an address.
+   b) Initializing a pointer to 0 is equivalent to initializing a pointer to NULL, but 0 is preferred.
+   c) The only integer that can be assigned directly to a pointer variable is 0.
+   d) Initialize pointers to prevent unexpected results.

Answer: b) is false. Actually, NULL is preferred because it highlights the fact that the variable is of a pointer type.

# 7.3 Pointer Operators

Next, let’s discuss the address (&) and indirection (*) operators, and their relationship.

# The Address (&) Operator

The unary address operator (&) returns the address of its operand. For example, given the following definition of y:

```
int y = 5;
```

the statement

```
int *yPtr = &y;
```

initializes pointer variable yPtr with variable y’s address—yPtr is then said to “point to” y. The following diagram shows the variables yPtr and y in memory:

![](bbox=[0.5, 0.8, 0.8, 0.95])