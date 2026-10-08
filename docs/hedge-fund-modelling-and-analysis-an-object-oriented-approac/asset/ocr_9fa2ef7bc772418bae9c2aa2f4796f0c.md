# SOURCE 1.8: RELATIONAL OPERATORS

```
// ...

cout << "\n" << "4 is greater than 3 = " << (4 > 3) << "\n";
cout << "4 is less than 3 = " << (4 < 3) << "\n";
cout << "4 is equal to 3 = " << (4 == 3) << "\n";
cout << "4 is not equal to 3 = " << (4 != 3) << "\n";

// ..
```

![](bbox=[0.115, 0.323, 0.843, 0.597])

In Source 1.8, the relational expressions are enclosed in parentheses so that C++ evaluates the relationship first and then sends the result to cout. Note that the relation operator to test equality is == and not a single = which instead refer to the assignment of a value to a variable.

# 1.4.4 Logical Operators

In order to test more complex expressions, logical operators can be combined with relational operators. Logical operators are normally associated with Boolean algebra⁴ and as such, produce a Boolean result. The three most common C++ logical operators are shown in Table 1.6.