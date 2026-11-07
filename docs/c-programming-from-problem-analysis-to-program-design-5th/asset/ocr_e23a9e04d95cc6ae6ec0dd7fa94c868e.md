Further suppose that you have the following declarations:

```
```cpp
int list[10] = {5, 3, 2, 10, 4, 19, 45, 13, 61, 11};
string strList[] = {"One", "One", "Three",
                    "How", "Six"};
```
```

What is the output of the following statements?

+   a. `cout << funExp(list, 10);`
+   
+   b. `cout << funExp(strList, 6) << endl;`

+   29. Write the definition of the function template that swaps the contents of two variables.

+   30.
+   
+    a. Overload the operator + for the class `newString` to perform string concatenation. For example, if `s1` is "Hello " and `s2` is "there", the statement:
+   
+   ```cpp
+   s3 = s1 + s2;
+   ```
+   
+   should assign "Hello there" to `s3`, in which `s1`, `s2`, and `s3` are `newString` objects.
+   
+    b. Overload the operator += for the class `newString` to perform the following string concatenation. Suppose that `s1` is "Hello " and `s2` is "there". Then, the statement:
+   
+   ```cpp
+   s1 += s2;
+   ```
+   
+   should assign "Hello there" to `s1`, in which `s1` and `s2` are `newString` objects.

# PROGRAMMING EXERCISES

+   1.
+   
+    a. Write the definitions of the functions to overload the increment, decrement, arithmetic, and relational operators as members of the class `rectangleType`.
+   
+    b. Write a test program that tests various operations on the class `rectangleType`.

+   2.
+   
+    a. Write the definitions of the functions to overload the increment, decrement, arithmetic, and relational operators as nonmembers of the class `rectangleType`.
+   
+    b. Write a test program that tests various operations on the class `rectangleType`.

+   3.
+   
+    a. Extend the definition of the class `clockType` by overloading the post-increment operator function as a member of the class `clockType`.
+   
+    b. Write the definition of the function to overload the post-increment operator for the class `clockType` as defined in part a.