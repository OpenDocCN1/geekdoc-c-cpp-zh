as that of primitive types like integers, floats, and so on. We will reuse the class `Point` from Chapter 11 which contains two integer members `x` and `y`, thereby storing the x and y coordinate values for each of the `Point` objects. To perform addition and subtraction of `Point` objects, we have included two operator functions `operator+` and `operator-`, as member functions of class `Point`. Let us concentrate on addition of `Point` objects, subtraction can be understood similarly.

Overloading operator + will give us an ability to perform addition of `Point` objects P1 and P2 using the following statement:

```
P3 = P1 + P2;
```

The point object P3 will be the resultant point in the Cartesian coordinate system obtained by adding points P1 and P2.

When compiling the statement P3 = P1 + P2, the compiler follows the following rules to invoke the operator function defined in class Point:

+   1. The operator function is invoked using the object that is written on the left hand side of the operator. In this case, object P1 is present on the left hand side of + hence the function `operator+` will be invoked using object P1.
+   2. The object written on the right hand side of the operator is passed as an argument to the operator function. In this case, object P2 is written on the right hand side of the operator + and hence P2 is passed as an argument to the operator function. This means that the signature of the operator function should be written such that it takes one argument of type Point as shown in Figure 13.7.

![](bbox=[0.143, 0.575, 0.849, 0.889])