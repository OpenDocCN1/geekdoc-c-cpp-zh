# 7.3 Type Compatible Rule 275

Thanks to the type compatible rule, we can use the same functions to process objects of the base class and objects of the publicly derived class (because a formal argument of a function is object of the base class, the actual argument can be object of the derived class). Since there is no need to design specific modules for every class, i.e., the program efficiency is greatly improved. This is another important feature of C++, i.e., polymorphism, which will be discussed in the next chapter. We can say that the type compatible rule is one of the important foundations of the polymorphism. In the following example, we use the same function to deal with objects in the same class family.

**Example 7.4:** Example of type compatible rule.

Class B1 is publicly derived from the base class BO, and class DI is in turn derived from class B1. The member function display() in base class BO is overridden in the derived classes. The derivation relations among these classes are shown in Figure 7.5.

The program is:

```
//7_4.cpp
#include <iostream>
using namespace std;
class B0
//define base class B0
public:
    void display(){cout<<B0::display()<<endl;}
    //public member function
class B1: public B0
//define publicly derived class B1
public:
    void display(){cout<<B1::display()<<endl;}
    //public member function
```

| B0 |
| display() : void |
| B1 |
| display() : void |
| D1 |
| display() : void |

Fig. 7.5: UML of the derivation relations among the classes.