+   8. Consider the definition of the class `dateType` given in Chapter 11. (3)
+      a. Write the statement that includes a `friend` function named `before` in the class `dateType` that takes as parameters two objects of type `dateType` and returns true if the date represented by the first object comes before the date represented by the second object; otherwise, the function returns false.
+      b. Write the definition of the function you defined in part a.

+   9. Suppose that the operator `<<` is to be overloaded for a user-defined class `mystery`. Why must `<<` be overloaded as a friend function? (3)

+   10. Suppose that the binary operator `+` is overloaded as a member function for a class `strange`. How many parameters does the function `operator+` have? (5, 6)

+   11. Which operators must be overloaded as members of a class? (5)

+   12. Consider the following declaration: (6)

```
class strange
{
    .
    .
    .
};
```

+   a. Write a statement that shows the declaration in the class `strange` to overload the operator `>>`.
+   
+   b. Write a statement that shows the declaration in the class `strange` to overload the operator `=`.
+   
+   c. Write a statement that shows the declaration in the class `strange` to overload the binary operator `+` as a member function.
+   
+   d. Write a statement that shows the declaration in the class `strange` to overload the operator `==` as a member function.
+   
+   e. Write a statement that shows the declaration in the class `strange` to overload the post-increment operator `++` as a member function.

+   13. Assume the declaration of Exercise 12. (6)
+      a. Write a statement that shows the declaration in the class `strange` to overload the binary operator `+` as a friend function.
+      b. Write a statement that shows the declaration in the class `strange` to overload the operator `==` as a friend function.
+      c. Write a statement that shows the declaration in the class `strange` to overload the post-increment operator `++` as a friend function.