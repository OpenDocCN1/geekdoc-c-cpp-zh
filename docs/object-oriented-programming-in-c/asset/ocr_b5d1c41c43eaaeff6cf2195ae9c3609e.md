```
vector operator+(vector);                // vector addition
vector operator-();                       // unary minus
friend vector operator+(vector,vector);   // vector addition
friend vector operator-(vector);          // unary minus
vector operator-(vector &a);              // subtraction
int operator==(vector);                   // comparison
friend int operator==(vector,vector)      // comparison
```

**vector** is a data type of **class** and may represent both magnitude and direction (as in physics and engineering) or a series of points called elements (as in mathematics)

The process of overloading involves the following steps:

+   1. Create a class that defines the data type that is to be used in the overloading operaion.
+   2. Declare the operator function **operator** op() in the public part of the class. It may be either a member function or a **friend** function.
+   3. Define the operator function to implement the required operations.

Overloaded operator functions can be invoked by expressions such as

```
op x or x op
```

for unary operators and

```
x op y
```

for binary operators. op x (or x op) would be interpreted as

```
operator op (x)
```

for **friend** functions. Similarly, the expression x op y would be interpreted as either

```
x.operator op (y)
```

in case of member functions, or

```
operator op (x,y)
```

in case of **friend** functions. When both the forms are declared, standard argument matching is applied to resolve any ambiguity.

# 7.3 Overloading Unary Operators

Let us consider the unary minus operator. A minus operator when used as a unary, takes just one operand. We know that this operator changes the sign of an operand when applied to a basic data item. We will see here how to overload this operator so that it can be applied