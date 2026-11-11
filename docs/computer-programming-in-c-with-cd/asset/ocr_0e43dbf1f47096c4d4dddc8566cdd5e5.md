In Listing 44, NegativeNumberShow is a class that has a friend operator function of the NegativeNumberShow type. The prototype of the operator function is declared in the NegativeNumberShow class, as shown in the following code snippet:

```
Friend NegativeNumberShow operator -(NegativeNumberShow);
```

Note that the argument that is passed in the operator function is NegativeNumberShow and not NegativeNumberShow &. This is because the operator function generates or returns a newly created object using the values of an object, which is passed as an argument. Therefore, the following code snippet assigns the n2 object with all the negative values of the n1 object:

```
n2=-n1;
```

In the preceding code snippet, however, the values stored in the n1 object do not get affected. Moreover, the following code snippet reassigns the n2 object:

```
n2=operator -(n2);
```

# Overloading of Binary Operators

The concept of operator overloading also applies to binary operators. Binary operators work with two operands. In order to understand the overloading of binary operators, these may be classified as follows:

+   - Arithmetic operators, such as `+ - * / %`
+   - Relational operators, such as `< > <= >= != ==`
+   - The assignment operator `=`
+   - Arithmetic assignment operators, such as `+= -= *= /= %=`
+   - The insertion and extraction operators `<< >>`
+   - The subscript operator `[]`
+   - The function call operator `()`
+   - The class member access operator `->`

Overloading a binary operator is similar to overloading a unary operator except that a binary operator requires an additional parameter. Listing 45 shows the overloading of the addition operator in a class as a member function (you can find this example in the AdditionOperatorOverload.cpp file on the CD in the code\\chapter6 folder):

# Listing 45: Overloading of the Addition Operator (+) as a Member Function

```
#include<iostream.h>

class Distance
{
    int i;
public:
```