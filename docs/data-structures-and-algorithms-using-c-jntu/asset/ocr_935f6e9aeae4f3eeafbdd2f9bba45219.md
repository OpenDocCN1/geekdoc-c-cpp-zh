Program 2.16 is an example for hierarchical inheritance. In this example, Class B and Class C are inherited from the same base Class A. So, Class B will have the members of Class B and the members of Class A and Class C will have the members of Class C and the members of Class A.

# 2.4.2.4 Single-level Inheritance

This inheritance is the same as the single inheritance, the only difference is that in single-level inheritance the derived class cannot be a base class.

# 2.4.2.5 Multi-level Inheritance

If a class is derived from a derived class, then the inheritance type is called multi-level inheritance.

# Example

Class B is derived from Class A and Class C is derived from class B; now Class B is base class to C and derived class for Class A.

The general form of multi-level inheritance is as follows:

```
Class<Derived-Class-NameB>: <Access-Specifier><Base-Class-NameA>
Class<Derived-Class-NameC>: <Access-Specifier><Derived-Class-NameB>
```

![](bbox=[0.3, 0.41, 0.55, 0.56])

# Program 2.17

```
#include<iostream.h>
#include<conio.h>
/*Multi-Level Inheritance*/
class A{
public:
int a;
void setA(int x)
{
a=x;
}
void showA()
{
cout<<"\nA="<<a;
}
};
class B: public A{
public:
int b;
```