```
```cpp
int funcAdd (plus<int> sum, int x, int y)
{
    return sum(x, y);
}
```
```

# **Sample Run:**

```
Line 3: num = 90
Line 8: str = Hello There
Line 9: Sum of 34 and 26 = 60
Line 13: intList: 1 2 3 4 5 6 7 8
Line 17: Sum of the elements of intList = 36
Line 19: Product of the elements of intList = 40320
```

Table 21-27 describes the relational STL function objects.

| Function object name | Description |
|---|---|
| `equal_to<Type>` | Returns true if the two arguments are equal, and false otherwise. For example, `equal<int> compare;` `bool isEqual = compare(5, 5);` The value of isEqual is true. |
| `not_equal<Type>` | Returns true if the two arguments are not equal, and false otherwise. For example, `not_equal<int> compare;` `bool isNotEqual = compare(5, 6);` The value of isNotEqual is true. |
| `greater<Type>` | Returns true if the first argument is greater than the second argument, and false otherwise. For example, `greater<int> compare;` `bool isGreater = compare(8, 5);` The value of isGreater is true. |
| `greater_equal<Type>` | Returns true if the first argument is greater than or equal to the second argument, and false otherwise. For example, `greater_equal<int> compare;` `bool isGreaterEqual = compare(8, 5);` The value of isGreaterEqual is true. |