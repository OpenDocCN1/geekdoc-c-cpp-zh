
The prototype of a friend function should be declared in the class if the operator is overloaded as a friend function:

```
friend function type operator operandname (argument list);
```

The function type is the type of return value of the overloaded operator, i.e., the type of the result of the operation. The term operator is the key in defining overload. operandname is the name of the operator to be overloaded. It must refer to an operator that can be overloaded, such as "+", the add sign. The argument list lists the arguments and the types needed for operand. If the operator is overloaded as a friend function, then the key word friend should be declared in the function in the class. The function is implemented outside the class.

If the operator overloaded as a member function, the number of arguments is one less than the number of operands (not applicable to "+" or "-"). If the operator is overloaded as a friend function, then the two numbers are same. The reason is that the operator overloaded as a member function and an object uses the overloaded member function, then the data of the object can be accessed directly, so there is no need to pass it by argument list. The missing operand is the object itself. But when the operator is overloaded as a friend function, and the friend operates on the data of an object, it must work through the object name. The number of operands does not change.

The main advantage of operator overloading is that we can change the operations of existing operators so they can operate on a user-defined class.

## 8.2.2 Operator Overloaded as Member Function

Operator overload is essentially function overload. When an operator is overloaded as a member function, it can freely access data members in the class. We always use an object of the class to access overloaded operators. If it is a binary operator, an operand is the object's data, pointed by this pointer, and the other operand is passed by an argument list of the overloaded function. If the operator is unary, the operand is pointed by this pointer of the object, so it does not require any argument. These two cases are illustrated below.

For binary operator B, if it is overloaded as a member function in order to indicate the expression oprnd1 B oprnd2, where oprnd1 is an object of class A, then B should be overloaded as a member function of A and the class has one formal argument, where type is that of oprnd2. After overloading, expression oprnd1 B oprnd2 is equivalent to calling function oprnd1.operator B oprnd2.

For a prefix operator U, such as "-" (minus sign), if it is to be overloaded as a member function in order to indicate expression U oprnd, where oprnd is an object of class A, then operator U should be overloaded as a member of class A, which has no argument list. After overloading, the expression U oprd is equivalent to calling function oprd.operator U()();

For postfix operators "++" and "--", if they are to be overloaded as member functions in order to indicate expression oprd++ and oprd--, where oprd is an object of class A, then the operator should be overloaded as a member function of class A and the function has an integer (int) as for argument. After overloading, the expressions oprd++ and oprd-- is equivalent to calling function oprd.operator++ (0) and oprd.operator-- (0). Here, the integer argument does not play any useful rules. It is used to differentiate prefix ++, and postfix ++, --.

In UML language, the representations of overloaded operators are similar to other member functions, which is "operatorname (argument list): function type".

Example 8.1: Operator (add and minus) overload for complex number class as member functions.

This is an example of binary operators overloaded as member functions. The rule of addition and subtraction is to separately add and subtract the real part and imaginary part respectively. The operands must be objects of a complex number class. So operators "+" and "-" can be overloaded as member functions. The overloaded function has only one formal argument, an object of a complex number class. In the example, the UML representation of the complex number class with operators overloading is shown in Figure 8.1.

```cpp
//8_1.cpp
#include<iostream>

using namespace std;
class complex            //define complex number class
{
public:
    //external interface
    complex(double r=0.0, double i=0.0){real=r;imag=i}//constructor
    complex operator + (complex c2); //member function to overload operator +
    complex operator - (complex c2); //member function to overload operator -
    void display(); //output the complex number
```

| complex |
| --- |
| - real : double |
| - imag : double |
| + complex(r : double = 0.0, i : double = 0.0) |
| + operator +(c2 : complex) : complex |
| + operator -(c2 : complex) : complex |
| + display() : void |

![](img/5618306d085ac1bac8275d6c4c5bbf2a_336_0.png)

```cpp
private: //private data
double real; //real part of a complex number
double imag; //imaginary part of a complex number
```

```cpp
complex complex::operator +(complex c2)
//implementation of overload function
{
  return complex(real+c2.real, imag+c2.imag);
//create a temporary object to return value
}
```

```cpp
complex complex::operator -(complex c2)
//implementation of overload function
{
  return complex(real-c2.real, imag-c2.imag);
//create a temporary object to return value
}
```

```cpp
void complex::display() {
  cout<<"real"<<","<<imag<<"" << endl;
}
```

```cpp
int main() {
  complex c1(5,4),c2(2,10),c3; //declare objects of class complex
  cout<<"c1="<<c1.display() << endl;
  cout<<"c2="<<c2.display() << endl;

  c3=c1-c2; //complete complex numbers' subtraction by
//operator overload

  cout<<"c3="<<c1-c2<<"" << endl;
  c3.display() << endl;

  cout<<"c3="<<c1+c2<<"" << endl;
  c3.display() << endl; //complete complex numbers' addition by
//operator overload
}
```

In the example, the addition and subtraction of complex numbers are overloaded as member functions of the complex class. We can see that operator member functions are almost the same as ordinary functions except the key word is used in the declaration and implementation. The result of the program is:

```
c1=(5,4)
c2=(2,10)
c3=c1-c2=(3,-6)
c3=c1+c2=(7,14)
```

The efficiencies of these two methods are different. The latter execution includes the following steps. First a local object c (the constructor is called here) is created, the copy-constructor is called when executing return statement, copy the value of c to a temporary object in main(). When the function operator "+" ends, the destructor is called to destroy object c. The former method is much more efficient, which creates a temporary object in main.

This statement appears to be "calling function". In reality, this is a temporary object syntax, which means to "create a temporary object and return it". We can also use the following statements to return the function value:

```cpp
complex::operator+(complex c2)
  //implementation of overload
{
  complex c(real+c2.real, imag+c2.imag);
  return c;
}
```

The operators "+" and "-" still obey the predefined rules in C++, but they have new functions for operating on complex numbers such as int.

## 8.2 Operator Overload

Example 8.2: Overload unary operator ++ as a member function.

This example is to overload unary operator ++ as a member function. Here we use the example of class Clock. The operands of unary operator ++ and postfix ++ are both objects of class Clock. We can overload the operator as a member function of class Clock. For the prefix unary operator, there is no formal argument in the overload function but for the postfix unary operator, there is an integer in the formal argument list.

```cpp
//8_2.cpp
#include<iostream>
using namespace std;
class Clock //define class Clock
(
```
