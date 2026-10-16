This means that when function polarToRectangular() assigns a value to its reference parameter x, the value of the corresponding argument xCoord is changed,

| rCoord | 2.0 |
| tCoord | 3.14159 |
| xCoord | -2.0 |
| yCoord |  |

**r** 2.0

**theta** 3.14159

and when polarToRectangular() assigns a value to its reference parameter y, the value of the corresponding argument yCoord is changed:

| rCoord | 2.0 |
| tCoord | 3.14159 |
| xCoord | -2.0 |
| yCoord | 0 |

**r** 2.0

**theta** 3.14159

Thus, to design a function like polarToRectangular() that sends back more than one value to its caller, we can proceed as follows:

+   1. Declare a reference parameter for each value to be communicated back to the caller:
+   
+   ```cpp
+   void polarToRectangular(double r, double theta,
+   double &x, double &y);
+   ```
+   
+   2. Assign to the reference parameters the values that must be communicated back:
+   
+   ```cpp
+   x = r * cos(theta);
+   y = r * sin(theta);
+   ```
+   
+   3. Call the function with a variable argument for each reference parameter:
+   
+   ```cpp
+   polarToRectangular(rCoord, tCoord, xCoord, yCoord);
+   ```

When the function terminates, the values of the argument variables will be changed to the values the function assigned to its reference parameters.



Although arguments corresponding to value parameters can be constants, literals, variables, or expressions, arguments corresponding to reference parameters must be variables because