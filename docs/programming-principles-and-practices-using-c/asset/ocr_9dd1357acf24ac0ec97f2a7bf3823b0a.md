```
```
        constexpr int c1 = max+7;   // OK: c1 is 107
        constexpr int c2 = n+7;   // error: we don't know the value of c2
          // ...
      }
```
```

To handle cases where the value of a “variable” that is initialized with a value that is not known at compile time but never changes after initialization, C++ offers a second form of constant (a **const**):

```
```
constexpr int max = 100;

void use(int n)
{
      constexpr int c1 = max+7;   // OK: c1 is 107
      const int c2 = n+7;   // OK, but don't try to change the value of c2
      // ...
      c2 = 7;                     // error: c2 is a const
}
```
```

Such “**const** variables” are very common for two reasons:

+   - C++98 did not have **constexpr**, so people used **const**.
- “Variables” that are not constant expressions (their value is not known at compile time) but do not change values after initialization are in themselves widely useful.

# ### 4.3.2 Operators

We just used the simplest operators. However, you will soon need more as you want to express more complex operations. Most operators are conventional, so we’ll just explain them later as needed and you can look up details if and when you find a need. Here is a list of the most common operators:

| Name | Comment |
|---|---|
| **f**(a) | function call | pass a to f as an argument |
| **++lval** | pre-increment | increment and use the incremented value |
| **--lval** | pre-decrement | decrement and use the decremented value |
| **!a** | not | result is bool |
| **-a** | unary minus |
| **a** **\*** **b** | multiply |
| **a/b** | divide |

*\(continues)*