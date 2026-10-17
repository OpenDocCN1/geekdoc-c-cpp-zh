# Classes in C++

# 5.1  Class Making

We talked briefly about what a class is and how in object-oriented programming, we build up from this basic unit. A class is a user-defined data type consisting of methods and data grouped together as members (i.e., encapsulated). A class uses objects that store data and have a defined state and behavior; it is also referred to as an *instance of a class*. A class is like a broad category that encompasses some entities that have similar attributes or features. For example, a cat and a tiger have similarities and belong to the *Felidae* animal family. In this example, *Felidae* is the name of the class and cats and tigers are the class members. The following code shows how we declare and use classes in C++.

# Code: Declaring and Using Classes

```
```cpp
#include <iostream>
using namespace std;
class Felidae
{
        public:
        string cats;
        string tigers;
        void petName()
        {
        std::cout << "\nCat's pet name is: " << cats;

```