# 9.1 Function Templates and Class Templates — 357

![](bbox=[0.105, 0.088, 0.73, 0.308])

**Fig. 9.5:** UML of class template Store and concrete classes.

# **Example 9.2:** Example of class template.

In this example, the program declares a class template Store to implement a wrapper to store / load data. The template is instantiated as concrete classes based on the given parameters, which are instantiated as objects S1, S2, S3, and D. However, the instantiation of the class template (as shown in Figure 9.5) is hidden. We call these concrete classes intStore / doubleStore / StudentStore (which do not occur in the program) in order to represent them in the UML graph.

```
//9_2.cpp
#include <iostream>
#include <cstdlib>
using namespace std;

struct Student            //Structure Student
{
    int id;             //Student ID
    float gpa;          //Student GPA
};\ntemplate <class T>      //Class Template: Load/store with any data
class Store
{
    private:
        T item;             //item is used to hold any type of data
        int haveValue;      //haveValue indicates item is holding data
        //or not
```