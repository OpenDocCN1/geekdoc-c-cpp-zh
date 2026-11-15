# 2.4 C++ Operators

To perform operations in a program, such as addition, multiplication, and comparison of objects, we use special operators that are defined for the built in data types supported by C++. In this section, we will look at several of these operators.

# Assignment Operator

An assignment statement uses the assignment operator, =, to store the result in the memory location named by the identifier. The general form of the assignment statement is

```
identifier = expression;
```

where an expression can be a constant, another object, or the result of an operation. Consider the following two sets of statements that declare and give values to the objects sum, x1, p1, and ch:

```
// Set One
double sum(10.5);
int x1(3);
Point p1(1.5, -4.7);
char ch('a');
```

```
// Set Two
double sum;
int x1;
Point p1, p2(1.5, -4.7);
char ch;
```

```
sum = 10.5;
x1 = 3;
p1 = p2;
ch = 'a';
```

After either set of statements is executed, the value of sum is 10.5, the value of x1 is 3, the value of p1 is (1.5, -4.7) and the value of ch is 'a', as shown in the following memory snapshot:

![](bbox=[0.2, 0.58, 0.9, 0.63])

The statements in Set One declare and initialize the objects at the same time in the type declaration statement; the assignment statements in Set Two could be used at any point in the program and thus may be used to change (as opposed to initializing) the values of objects that have already been declared. Note that the compiler provides an assignment operator for the Point class. The assignment operator performs a bit-wise copy of the data members from the object on the right-hand side of the assignment operator to the corresponding data members of the object on the left-hand side of the assignment operator.

Multiple assignments are also allowed in C++, as in the following statement, which assigns a value of zero to each of the objects x, y, and z:

```
x = y = z = 0;
```

Multiple assignments are discussed further at the end of this section.