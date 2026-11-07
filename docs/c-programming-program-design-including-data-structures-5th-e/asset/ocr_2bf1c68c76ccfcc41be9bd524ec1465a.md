28. Consider the definition of the following function template:

```
template <class Type>
Type funExp(Type list[], int size)
{
    int j;
    Type x = list[0];
    Type y = list[size - 1];

    for (j = 1; j < (size - 1)/2; j++)
    {
        if (x < list[j])
            x = list[j];
        if (y > list[size - 1 - j])
            y = list[size - 1 - j];
    }

    return x + y;
}
```

Further suppose that you have the following declarations:

```
int list[10] = {5, 3, 2, 10, 4, 19, 45, 13, 61, 11};
string strList[] = {"One", "Hello", "Four", "Three",
                     "How", "Six"};
```

What is the output of the following statements?

+   a. `cout << funExp(list, 10);`
+   
+   b. `cout << funExp(strList, 6) << endl;`

29. Write the definition of the function template that swaps the contents of two variables.

+   30.
+   
+   a. Overload the operator + for the class `newString` to perform string concatenation. For example, if s1 is "Hello " and s2 is "there", the statement:
+   
+   ```cpp
+   s3 = s1 + s2;
+   ```
+   
+   should assign "Hello there" to s3, in which s1, s2, and s3 are newString objects.
+   
+   b. Overload the operator += for the class `newString` to perform the following string concatenation. Suppose that s1 is "Hello " and s2 is "there". Then, the statement:
+   
+   ```cpp
+   s1 += s2;
+   ```
+   
+   should assign "Hello there" to s1, in which s1 and s2 are newString objects.