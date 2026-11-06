```
E.
```cpp
{
    for (unsigned int x = 1; x <= 20; ++x) {
        if (x % 5 == 0)
            cout << x << endl;
        else {
            cout << x << '\t';
        }
    }
}
```
```

# 4. 5.4

A. *Error:* The semicolon after the `while` header causes an infinite loop.

*Correction:* Delete the semicolon after the `while` header.

B. *Error:* Using a floating-point number to control a `for` iteration statement.

*Correction:* Use an `unsigned int` and perform the proper calculation to get the values.

```
```cpp
{
    for (unsigned int y = 1; y != 10; ++y) {
        cout << (static_cast<double>(y) / 10) << endl;
    }
}
```
```

C. *Error:* Missing `break` statement in the first `case`.