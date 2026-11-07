```
```cpp
38    cout << "\\ncos(" << 0.0 << ") = " << cos(0.0);
39    cout << "\\ntan(" << 0.0 << ") = " << tan(0.0) << endl;
40 } // end main
```
```

```
```text
sqrt(900.0) = 30.0
sqrt(9.0) = 3.0
exp(1.0) = 2.718282
exp(2.0) = 7.389056
log(2.718282) = 1.0
log(7.389056) = 2.0
log10(1.0) = 0.0
log10(10.0) = 1.0
pow(2.0, 2.0) = 4.0
pow(2.0, 7.0) = 128.0
pow(9.0, 0.5) = 3.0
fmod(2.600, 1.200) = 0.200
sin(0.0) = 0.0
cos(0.0) = 1.0
tan(0.0) = 0.0
```
```

+   6.4
+   
+    a) `double hypotenuse( double side1, double side2 )`
+    b) `int smallest( int x, int y, int z )`
+    c) `void instructions()`
+    d) `double intToDouble( int number )`

+   6.5
+   
+    a) `double hypotenuse( double, double );`
+    b) `int smallest( int, int, int );`
+    c) `void instructions();`
+    d) `double intToDouble( int );`

+   6.6
+   
+    a) `register int count = 0;`
+    b) `static double lastVal;`

+   6.7
+   
+    a) *Error:* Function h is defined in function g.  
+    *Correction:* Move the definition of h out of the definition of g.
+   
+    b) *Error:* The function is supposed to return an integer, but does not.  
+    *Correction:* Delete variable result and place the following statement in the function:
+   
+    ```cpp
+    return x + y;
+    ```
+   
+    c) *Error:* The result of `n + sum( n - 1 )` is not returned; sum returns an improper result.  
+    *Correction:* Rewrite the statement in the else clause as
+   
+    ```cpp
+    return n + sum( n - 1 );
+    ```
+   
+    d) *Errors:* Semicolon after the right parenthesis that encloses the parameter list, and re-defining the parameter a in the function definition.  
+    *Corrections:* Delete the semicolon after the right parenthesis of the parameter list, and delete the declaration `float a;`.
+   
+    e) *Error:* The function returns a value when it isn’t supposed to.  
+    *Correction:* Eliminate the return statement or change the return type.

6.8  This creates a reference parameter of type “reference to double” that enables the function to modify the original variable in the calling function.