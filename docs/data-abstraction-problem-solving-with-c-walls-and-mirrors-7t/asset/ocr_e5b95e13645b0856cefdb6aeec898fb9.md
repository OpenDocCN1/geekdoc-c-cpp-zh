should never occur in normal execution. For example, suppose that you are testing a simple linear search algorithm:

```
```cpp
for (int i = 0; i < size; i++)
{
    if (array[i] == target)
        return i;
} // end for
```
```

> Always carefully test boundary values

You should use all of the following values of target:

+   - Just less than index[0] (boundary at the beginning of the array)
+   - Equal to index[0] (boundary at the beginning of the array)
+   - Equal to some entry in the middle of the array
+   - Within the range of values stored in the array, but unequal to any
+   - Equal to index[size - 1] (boundary at the end of the array)
+   - Just greater than index[size - 1] (boundary at the end of the array)

> Values for testing a search

You should also test this algorithm with

+   - An empty array
+   - An array with one entry in it
+   - An array with many entries

For each of these tests, you should manually trace the data so that the results are known ahead of time. In this way, test data can be the input to a module, and you can compare the output with known results.

# B.7.4 Testing Techniques

As indicated in the debugging section, assert statements can be useful for checking assertions. However, the assert statement is not powerful enough for the full-scale testing of a system. Other techniques need to be utilized.

A common technique is to write a block of code that tests a module. When you have finished testing the system, you can simply comment it out—rather than deleting it—as more testing will be required after you make modifications during the next iteration. Alternatively, you can turn these testing blocks of code on and off globally by using one of the techniques that we discuss next.

> Disable, but do not remove, testing code after use

The first technique uses a global boolean variable to grant access to testing code contained within the body of if statements. Setting the variable to false turns testing code “off,” and setting it to true enables testing. For example, the following test is disabled:

```
```cpp
const bool TESTING = false; // Disables testing code
if (TESTING)
{
    ... // Testing code
} // end if
```
```

You could define several different boolean variables to turn different tests “on” and “off.” All that is required is to change the value of the boolean variable and to recompile.

A second, more efficient, technique uses the preprocessor to the compiler. You define a macro that guards the testing code. Then you place the test code within preprocessor directives that test whether that macro has been defined. For example:

```
```cpp
#define TESTING
#ifdef TESTING
... // Testing code in here.
#endif
```
```