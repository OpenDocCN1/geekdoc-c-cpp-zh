as:

coin money

We can also declare enumerations with specific enum values:

```
enum coin {penny, nickel, dime, quarter=25, half_dollar, dollar=100};
```

Now:

| penny | 0 |
| nickel | 1 |
| dime | 2 |
| quarter | 25 |
| half-dollar | 26 |
| dollar | 100 |

# Anonymous Enums

An anonymous enum is defined as follows:

```
enum { COLOR = 1 };
```

This is the same as int COLOR = 1; except that the enum COLOR is a constant. An anonymous enum behaves like a const int except that we cannot get the address of the enum. This is very useful when we want to define const integer variables that cannot be addressed through a pointer.

An anonymous enum is effectively a compile-time integer constant.