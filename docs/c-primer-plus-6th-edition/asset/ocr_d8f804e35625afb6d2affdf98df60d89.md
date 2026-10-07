Most of the operators in Table 11.1 can be overloaded by using either member or nonmember functions. However, you can use only member functions to overload the following operators:

| Operator | Description |
| = | Assignment operator |
| () | Function call operator |
| [] | Subscribing operator |
| -> | Class member access by pointer operator |

**Note**nThis chapter does not cover every operator mentioned in the list of restrictions or in Table 11.1. However, Appendix E, "Other Operators," summarizes the operators that are not covered in the main body of this text.

# **Table 11.1 Operators That Can Be Overloaded**

| + | * | ^ |
| & | | ! | < |
| > | += | -= | *= | /= | = |
| &= | *= | << | >> | >= |
| <= | == | != | <= | && |
| || | ++ | -- | |
| () | [] | new delete new [] | delete [] |

In addition to these formal restrictions, you should use restraint when overloading operators. For example, you shouldn't overload the * operator that swaps the data members of two Time objects. Nothing in the notation would suggest what the operator did, so it would be better to define a class method with an explanatory name such as Swap().

# **More Overloaded Operators**

Some operators make sense for the Time class. For example, you might want to subtract one from another or multiply by a factor.This suggests overloading the subtraction and multiplication operators. The technique is the same as for the addition operator: you create operator-() and operator*() methods. That is, you add the following prototypes to the class declaration:

```
Time operator-(const Time & t) const;
Time operator*(double n) const;
```