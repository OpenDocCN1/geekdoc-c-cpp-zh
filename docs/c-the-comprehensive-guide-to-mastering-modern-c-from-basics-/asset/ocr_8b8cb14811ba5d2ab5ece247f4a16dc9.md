With C++20, you can define greater, smaller, equal, smaller-equal, and so on for custom types without overloading a bunch of operators and potentially making mistakes. Simply define the operator<==, and your data type will support the complete set of operators, especially < and ==, to be used in ordered containers.

If you insert the following definition for a custom data type, the compiler generates operator<=> such that the elements are compared in the order <=> in which they are defined in the class:

```
auto operator<=>(const X& other) const = default;
```

If you desire different behavior, then implement the operator yourself.

> A Custom-Defined operator<=> Also Requires a Custom-Defined operator====

If you define operator<=> yourself, you should also define operator== yourself. This is because you let the compiler generate operator<=> = default, then operator== will not be generated automatically. It will be missing, and you will not be able to use == for your type.

The reason is that the result of the == check can often be computed faster than the result of <=, which covers the three <, ==, and > operators. So the compiler assumes that you have a better implementation for operator== if you already know