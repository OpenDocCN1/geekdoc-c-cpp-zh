# 8.2 Operator Overload

gers, the operators still obey the predefined rules in C++, but they have new functions for operating on complex numbers. Operator "+", when acting on different objects, will have different behaviors, and hence it has polymorphic features.

In this example, temporary objects are created for returning values in the overload functions of "+" and "-":

```
return complex(c.real,c.imag);
```

This statement appears to be "calling constructor function". In reality, this is a temporary object syntax, which means to "create a temporary object and return it". We can also use the following statements to return the function value:

```
complex::operator+(complex c2)
  //implementation of overload operator
{
  complex c(real+c2.real, imag+c2.imag);
  return c;
}
```

The efficiencies of these two methods are different. The latter execution includes the following steps. First a local object c (the constructor is called here) is created, the copy-constructor is called when executing return statement, copy the value of c to a temporary object in main(). When the function operator "+" ends, the destructor is called to destroy object c. The former method is much more efficient, which creates a temporary object in main().

The result of the program is:

```
c1=(5,4)
c2=(2,10)
c3=c1-c2=(3,-6)
c3=c1+c2=(7,14)
```

**Example 8.2:** Overload unary operator ++ as a member function.

This example is to overload unary operator ++ as a member function. Here we use the example of class Clock. The operands of unary operator ++ and postfix ++ are both objects of class Clock. We can overload the operator as a member function of class Clock. For the prefix unary operator, there is no formal argument in the overload function but for the postfix unary operator, there is an integer in the formal argument list.

```
//8_2.cpp
#include<iostream>
using namespace std;
class Clock //define class Clock
(
```