# 13.11 Overloading Type Cast Operator

Like any other operators, we can also overload the type cast operator using an `operator` keyword. Figure 13.22 gives the syntax of overloading type cast operator.

![](bbox=[0.193, 0.204, 0.812, 0.368])

**Figure 13.22:** Syntax to overload type cast operator

> **NOTES**
> 
> 1. The return type should not be specified when defining the operator function which overloads the type cast operator. However, there must be a `return` statement within the operator function which returns the value converted to the target type.
> 2. Operator function overloading type cast operator cannot take any arguments.

There are certain user-defined types that could be fully represented using primitive types. Consider class Weight that we have created in section 13.4.1, specifies weight in kilogram and gram. You could also represent this value as a single long number in grams. For example, a Weight object with values as 50 kg and 800 g can be represented as a single long value of 50,800 g as shown in Figure 13.23. This means that there is a scope to cast a weight object into a primitive type. You can overload type cast operator in class Weight if you would want to allow casting objects of weight to a specific type. In this case, we would want to cast a weight

![](bbox=[0.183, 0.705, 0.819, 0.878])

**Figure 13.23:** Boxing and unboxing Weight objects to/from a long value