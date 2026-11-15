# # C++ Statement Summary

Two-dimensional array declaration:

```
```
double x[10] [5] :
```
```

# ## Notes

+   1. Use symbolic constants to declare the size of an array so that it is easy to modify.
+   2. In documentation, describe a two-dimensional array as a grid with rows and columns.
+   3. The objects i and j are commonly used as offsets for a two-dimensional array.
+   4. Include pre- and post-conditions in function definition.

# ## Debugging Notes

+   1. The declared column size of an array must be specified in the formal parameter list and in the function prototype.
+   2. Be careful not to exceed the maximum offset value when referencing an element in a multidimensional array.
+   3. Be sure to enclose each offset in its own set of brackets when referencing elements of a multidimensional array.
+   4. When translating matrix notation to C++, remember that the first row and column in a matrix is referenced with the number 1, not 0.
+   5. Multidimensional matrices complicate the logic of a program and should be used only when they are necessary.
+   6. When declaring a two-dimensional vector, remember that the space between the last two >> characters in the type declaration statement is required.

# ## Problems

# ### Exam Practice!

Give the corresponding snapshots of memory after each of the following sets of statements is executed. Use ? to indicate an array element that is not initialized.

+   1. int x[5] [6];
+      ...
+      for(int r=0; r<=5; ++r)
+      for(int c=0; c<6; ++c)
+      x[r] [c] = r * c;
+   2. int x[3] [4];
+      for(int r=0; r<3; ++r)
+      for(int c=0; c<4; ++c)
+      x[r] [c] = c;