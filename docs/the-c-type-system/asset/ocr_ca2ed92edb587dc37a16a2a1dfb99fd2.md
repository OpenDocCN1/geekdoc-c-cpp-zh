# 3

# REFERENCE AND
VALUE PARAMETERS

![](bbox=[0.172, 0.488, 0.354, 0.625])

In this chapter, we’ll look at how method parameters and arguments relate to reference and value types. We’ll revisit the idea that all variables have a value, regardless of their type, and see how to pass values of different types *by value* or *by reference* as arguments for methods.

We’ll explore the following:

+   - How *reference* and *by reference* differ in meaning
+   - Why aliasing and mutability are so closely related
+   - How avoiding side effects can make our code clearer
+   - When to pass values by reference as an optimization

Passing method parameters by value or by reference isn’t the same as those parameters being value or reference types. In other words, the parameter’s type (value or reference) differs from how the method uses that parameter (by value or by reference). *Passing* in this context refers to