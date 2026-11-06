# 12.4.5 `virtual` Functions in the `CommissionEmployee` Hierarchy

Now let’s see how `virtual` functions can enable polymorphic behavior in our employee hierarchy. **Figures 12.4–12.5** are the headers for classes `CommissionEmployee` and `BasePlusCommissionEmployee`, respectively. We’ve modified these to declare each class’s `earnings` and `toString` member functions as `virtual` (lines 28–29 of **Fig. 12.4** and lines 17–18 of **Fig. 12.5**). Because functions `earnings` and `toString` are `virtual` in class `CommissionEmployee`, class `BasePlusCommissionEmployee`’s `earnings` and `toString` functions **override** class `CommissionEmployee`’s. In addition, class `BasePlusCommissionEmployee`’s `earnings` and `toString` functions are declared with C++11’s **override** keyword.

![](bbox=[0.118, 0.66, 0.191, 0.718])

# *Error-Prevention Tip 12.1*

*To help prevent errors, apply C++11’s `override` keyword to the prototype of every derived-class function that overrides a base-class `virtual` function. This enables the compiler to check whether the base class has a `virtual` member function with the same signature. If not, the compiler generates an error. Not only does this ensure that you*