**Table 13.8  Unary operator plus or minus**

```cpp
// Declarations
const Fraction operator+() const;
const Fraction operator-() const;

// Definition of plus operator
const Fraction Fraction::operator+() const
{
    Fraction temp (+numer, denom);       // a new object
    return temp;
}

// Definition of minus operator
const Fraction Fraction::operator-() const
{
    Fraction temp (-numer, denom);       // a new object
    return temp;
}
```

does not exist when the function terminates (we cannot return it as a reference). We also return the object with a constant modifier because the returning object can only be used as an *rvalue* (we cannot use it as an *lvalue* such as at the left-hand side of the assignment operator). An object with a constant modifier cannot be chained either.

# Pre-Increment and Pre-Decrement Operators

We now overload the pre-increment and the pre-decrement operators. Each operator has a side effect that changes its operand; the returned object is a copy of the changed object. C++ allows the chaining of these two operators, which means that we can have `++++x` or `----x`. This means that the returned value must be an *lvalue* (Figure 13.4).

Based on the checklist in Figure 13.4, we can define the declaration and the definition of the pre-increment/pre-decrement overloaded operators for our `Fraction` class in Table 13.9. Each of these two operators has two tasks to perform. The operator must change

![](bbox=[0.297, 0.764, 0.713, 0.906])

**Figure 13.4**  Overloading the pre-increment and the pre-decrement operators