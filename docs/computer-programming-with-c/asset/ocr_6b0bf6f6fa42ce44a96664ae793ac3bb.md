```
b=-a;
```

![](bbox=[0.72, 0.135, 0.96, 0.22])

The statement b=-a; assigns the negated value of a to the variable b. Hence, the value of variable b is set to -10 as shown in Figure 3.7. Note that, value of variable a will still be +10 because the negated value of a is actually assigned to the variable b and not back to the variable a.

The syntax is such that, we can also use the operator + in a unary form. However, using the operator+ in unary form may not give any useful purpose to the programmer because all the data values are by default considered as positive in C/C++ unless any of the data value is explicitly specified as negative in the program.

# 3.2.2 Example 2: Using the operators +, -, *, / and % in binary form

Figure 3.8 gives the code which creates two variables a and b with values 20 and 5, respectively. The code applies all the binary arithmetic operators on the two variables a and b and stores the result of each of the operations in the variables p, q, r, s, and t.

```
    int a = 10, b = 20;

    int p, q, r, s ,t;

    p = a + b;
    q = a - b;
    r = a * b;
    s = b / a;
    t = b % a;
```

Variable p stores result of addition of
two numbers a and b. Hence, the variable
p will store a value 30

Variable q stores result of subtraction of
two numbers a and b. Hence, the variable
q will store a value -10

Variable r stores result of multiplication of
two numbers a and b. Hence, the variable
r will store a value 200

Variable s stores the quotient of division of
two numbers a and b. Hence, the variable
s will store a value 2 (20/10=2)

Variable t stores the remainder of division of
two numbers a and b. Hence, the variable
t will store a value zero (20%10=0)

Figure 3.8: Binary arithmetic operators in C/C++

# Can we use the remainder operator % with floating point constants?

We cannot use the operator % with the floating point or the double constants. This is because, the float/double constants contain fractional components and hence the result of dividing two floats or two doubles should also contain a fractional component without any remainder. Usage of a % operator with float or double variables will result into an compilation error in the program. Hence, the statement below will give a compilation error:

```
    float a=100.7, b=22.5,c;
    c=a+b; /*compilation ERROR: Illegal usage of float operands*/
```