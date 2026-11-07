+   c. Assume that two objects of type `strange` are equal if their corresponding member variables are equal. Write the definition of the function `operator==` for the class `strange`, which is overloaded as a member function.

35. Consider the definition of the following function template: (8, 9)

```
template <class Type>
Type surprise(Type x, Type y)
{
    return x + y;
}
```

What is the output of the following statements?

+   a. `cout << surprise(5, 7) << endl;`

+   b.
+   ```cpp
+   string str1 = "Sunny";
+   string str2 = " Day";
+   cout << surprise(str1, str2) << endl;
+   ```

36. Consider the definition of the following function template: (8, 9)

```
template <class type>
type funcExp(type list[], int size)
{
    type x = list[0];
    type y = list[size - 1];

    for (int j = 1; j < size - 1; j++)
    {
        if (x < list[j])
            x = list[j];
        if (y > list[size - 1 - j])
            y = list[size - 1 - j];
    }

    return y + x;
}
```

Further suppose that you have the following declarations:

```
double sales[7] = {280.50, 320.00, 56.00, 78.90, 300.00,
                    100.00, 250.00};
string names[] = {"Mike", "Lisa", "Nancy", "Robinson",
                  "Miller", "Sam"};
```

What is the output of the following statements?

+   a. `cout << funcExp(sales, 7) << endl;`

+   b. `cout << funcExp(names, 6) << endl;`

37. Write the definition of the function template that swaps the contents of two variables. (8, 9)