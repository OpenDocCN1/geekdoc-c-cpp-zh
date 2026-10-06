# 5.3 Static Members of Class 165

while the attribute value of each object can be different. This kind of attribute is called “instance attribute” in the object-oriented method, and is represented by a nonstatic data member of class in C++ programs. For example, the EmpNo, ID, and name of class employee in the object above are all instance attributes represented by nonstatic data members. Nonstatic data members have a copy in every object of the class, by which an object differs from other objects of the same class. If there is a concept “class attribute” in the object-oriented method, an attribute that belongs to the whole class and does not belong to any specific object, we can use the keyword static to declare it a static member. A static member has only one copy in a class, and it is protected and used by all the objects of the class, to achieve data sharing among different objects of the same class. Class attribute is a data item that represents the common characteristic of all objects of one class. Its attribute value is the same to all object instances. In short, if we compare a “class” to a factory, and to the products made by the factory, static members would be stored in the factory and belong to the factory, and they would not belong to each product.

A static data member has a static lifetime. Because static data does not belong to any object, we can only access it through a class name, and the general way is “class name::identifier”. We only perform a referential declaration of a static data member in the definition of its, while the definitive declaration must be done using the class name qualification at someplace in the file scope, and the initialization can also be done during the definitive declaration. UML language underlines the data member to represent a static data member. We can find out the usage of static data members in the following example.

Example 5.4: Class Point with static data members.

This program is modified from the class Point in Chapter 4. It brings in a static data member countP to count the number of object Point. The UML diagram of class Point that includes static data member countP is as shown in Figure 5.2.

| Point |
| - X : int |
| Y : int |
| - countP : int = 0 |
| +Point(xx : int = 0, yy : int = 0) |
| + GetX() : int |
| + GetY() : int |
| + Point(p : Point &) |
| + GetC() : void |

> Fig. 5.2: UML diagram of class Point that includes static data member.

```
//5_4.cpp
#include <iostream>
using namespace std;
```