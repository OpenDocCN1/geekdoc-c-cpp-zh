# SUMMARY

# Key Terms

+   alphanumeric character
+   null character
+   string class
+   array
+   offset
+   subscriptions
+   binary search
+   one-dimensional array
+   Unified Modeling Language (UML)
+   event space
+   sample space
+   variance
+   C-style string
+   selection sort algorithm
+   vector class
+   character string
+   sequential search
+   whitespace
+   magnitude
+   sorting
+   zero crossing
+   mean
+   standard deviation
+   median
+   statistical measurements

# C++ Statement Summary

```
Include C-style string header file
#include<cstring>
Include string class header file
#include<string>
Include vector class header file
#include<vector>
Range-based for Statement
for(declaration:range)
statement;
Array and vector declaration:
int a[5], b[]={2, 3, -1};
char vowels[]={'a', 'e', 'i', 'o', 'u'};
string words[100];
vector<double> time;
```

# Notes

+   1. The identifier i is commonly used as a subscript for a one-dimensional array.
+   2. Use symbolic constants to declare the size of an array so that it is easy to modify.

# Notes

+   1. Use arrays only when it is necessary to keep all the data available in memory.
+   2. If unexpected characters are printed at the end of a C-style string, the null character may be missing from the string.
+   3. Be careful not to exceed the maximum offset value when referencing an element in an array.
+   4. An array must be declared to be as large as, or larger than, the maximum number of values to be stored in it.
+   5. Because an array reference in a function is always a pass by reference, be careful that you do not inadvertently change values in an array in the function.