```
```cpp
arra[1]=&e2;
arra[0]->example();
arra[1]->example();
}
```
```

The output of Program 9.14 would be:

C text Book written by Balagurusamy
C++ text Book written by Balagurusamy

# 9.8 Virtual Constructors and Destructors

“A constructor can not be virtual”. There are some valid reasons that justify this statement. First, to create an object the constructor of the object class must be of the same type as the class. But, this is not possible with a virtually implemented constructor. Second, at the time of calling a constructor, the virtual table would not have been created to resolve any virtual function calls. Thus, a virtual constructor itself would not have anywhere to look up to. As a result, it is not possible to declare a constructor as virtual.

A virtual destructor however, is pretty much feasible in C++. In fact, its use is often promoted in certain situations. One such situation is when we need to make sure that the different destructors in an inheritance hierarchy are called in order, particularly when the base class pointer is referring to a derived type object. It must be noted here that the order of calling of destructors in an inheritance hierarchy is opposite to that of constructors.

Consider the following class declarations that make use of destructors:

```
```cpp
class A
{
public:
```
```