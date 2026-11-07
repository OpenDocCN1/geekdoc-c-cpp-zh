+   4. In C++, `struct` is a reserved word.
+   5. In C++, `struct` is a definition; no memory is allocated. Memory is allocated for the `struct` variables only when you declare them.
+   6. Components of a `struct` are called members of the `struct`.
+   7. Components of a `struct` are accessed by name.
+   8. In C++, the dot (.) operator is called the member access operator.
+   9. Members of a `struct` are accessed by using the dot (.) operator. For example, if `employeeType` is a `struct`, `employee` is a variable of type `employeeType`, and `name` is a member of `employee`, then the expression `employee.name` accesses the member name. That is, `employee.name` is a variable and can be manipulated like other variables.
+   10. The only built-in operations on a `struct` are the assignment and member access operations.
+   11. Neither arithmetic nor relational operations are allowed on `struct` (s).
+   12. As a parameter to a function, a `struct` can be passed either by value or by reference.
+   13. A function can return a value of type `struct`.
+   14. A `struct` can be a member of another `struct`.

# EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

+   1. Mark the following statements as true or false.
+      a. All members of a `struct` must be of different types. (1)
+      b. A `struct` is a definition, not a declaration. (1)
+      c. A `struct` variable must be declared after the `struct` definition. (1)
+      d. A `struct` member is accessed by using the operator ::. (2)
+      e. The only allowable operations on a `struct` are assignment and member selection. (2)
+      f. Because a `struct` has a finite number of components, relational operations are allowed on a `struct`. (2)
+      g. Some aggregate input/output operations are allowed on a `struct` variable. (2)
+      h. A `struct` variable can be passed as a parameter either by value or by reference. (4)
+      i. A function cannot return a value of the type `struct`. (4)