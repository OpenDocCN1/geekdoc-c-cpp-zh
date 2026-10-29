Suppose you had (foolishly) overloaded the function name `mpg` so that your program contained the following definition of `mpg` as well as the one previous:

```
int mpg(int goals, int misses)
//Returns the Measure of Perfect Goals
//which is computed as (goals − misses).
{
    return (goals − misses);
}
```

In a program that contains both of these definitions for the function name `mpg`, the following will (unfortunately) output 43 miles per gallon (since 43 is 45 − 2):

```
cout << mpg(45, 2) << " miles per gallon";
```

When C++ sees the function call `mpg(45, 2)`, which has two arguments of type int, C++ first looks for a function definition of mpg that has two formal parameters of type int. If it finds such a function definition, C++ uses that function definition. C++ does not convert an int argument to a value of type double unless that is the only way it can find a matching function definition.

The mpg example illustrates one more point about overloading: You should not use the same function name for two unrelated functions. Such careless use of function names is certain to create confusion.

# Self-Test Exercises

+   8. Suppose you have two function definitions with the following declarations:
+   
+   ```cpp
+   double score(double time, double distance);
+   int score(double points);
+   ```
+   
+   Which function definition would be used in the following function call and why would it be the one used? (x is of type double.)
+   
+   ```cpp
+   double finalScore = score(x);
+   ```

+   9. Suppose you have two function definitions with the following declarations:
+   
+   ```cpp
+   double theAnswer(double data1, double data2);
+   double theAnswer(double time, int count);
+   ```
+   
+   Which function definition would be used in the following function call and why would it be the one used? (x and y are of type double.)
+   
+   ```cpp
+   x = theAnswer(y, 6.0);
+   ```