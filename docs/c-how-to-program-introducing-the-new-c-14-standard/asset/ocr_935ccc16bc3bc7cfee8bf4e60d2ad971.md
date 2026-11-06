```
```cpp
phone >> cin;
```
```

Such statements would be confusing to most C++ programmers, who are familiar with `cout` and `cin` appearing as the *left* operands of these operators. Overloaded operator functions for binary operators can be member functions only when the *left* operand is an object of the class in which the function is a member.

*Overloaded input and output operators are declared as friends if they need to access non-public class members directly for performance or because the class may not offer appropriate get functions. Also, the* `PhoneNumber` *reference in function* `operator<<`*’s parameter list (Fig. 10.4, line 10) is* `const`*, because the function simply outputs a* `PhoneNumber`*, and the* `PhoneNumber` *reference in function* `operator>>`*’s parameter list (line 20) is non-*`const`*, because the function must modify the* `PhoneNumber` *object to store the telephone number.*

![](bbox=[0.118, 0.624, 0.195, 0.681])

# Software Engineering Observation 10.2

*New input/output capabilities for user-defined types are added to C++ without modifying standard input/output library classes. This is another example of C++’s extensibility.*

The overloaded stream insertion operator (`<<`) is used in an expression in which the left operand has type `ostream&`, as in `cout <<`