# Simple Requirements

A simple requirement consists of an arbitrary C++ expression statement and is satisfied if the corresponding expression would compile without errors if it were part of a real, executable code. The following example shows a more complete version of the `RandomAccessIterator<>` concept definition from before:

```
```cpp
template <typename Iter>
concept RandomAccessIterator = BidirectionalIterator<Iter>
  && requires (Iter i, Iter j, int n)
  {
    i + n; i - n; n + i; i += n; i -= n; i[n];
    i < j; i > j; i <= j; i >= j;
  };
```
```

This requires expression consists of ten simple requirements. It evaluates to true if all corresponding expressions are valid. In this example, all expressions apply some operator to two parameter names, but of course any form of expression may be used instead, including literals, function calls, constructor invocations, type conversions, class member accesses, and so on. All variables you use in these expressions must either be global variables or variables introduced in the parameter list. That is, you cannot declare local variables in the usual way as follows:

```
```cpp
requires (Iter i, Iter j)
{
    int n;                         /* Error: not an expression statement */
    i + n; i - n; n + i; i += n; i -= n; i[n]; /* Error: undeclared identifier */
    i < j; i > j; i <= j; i >= j;
}
```
```

> **Tip**  To better express the actual requirements, you should add a `const` qualifier to the type of each parameter of a requires expression that is not used in any expression that effectively requires it to be non-const. If needed, you can introduce both const and non-const variables of the same type. Here is how you could refine the definition of `RandomAccessIterator<>` along these lines:

```
```cpp
template <typename Iter>
concept RandomAccessIterator = BidirectionalIterator<Iter>
  && requires (const Iter i, const Iter j, Iter k, const int n)
  {
    i + n; i - n; n + i; i[n];    // Required to work on const operands
    k += n;                         // Only these (left) operands must be non-const
    i < j; i > j; i <= j; i >= j;  // Required to work on const operands
  };
```
```