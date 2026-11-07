![](bbox=[0.294, 0.089, 0.869, 0.319])

# Separate Compilation

We discussed separate compilation before, but it is interesting to see how it works in the case of inheritance, as shown in Figure 11.12.

The figure reveals several points. The *Person* class is compiled and sent to anyone who wants to use only that class. The *Person* and the *Student* classes are compiled by two different entities if the *Student* class has access to the interface file for the *Person* class because the interface file for the *Student* class must include the interface file for the *Person* class.

# An Example Using Separate Compilation

We now give the interface, implementation, and application files for our simple inheritance example with constructors, destructor, and other functions. We have added more data fields, but we have augmented the `set` and `get` functions and used only the `print` function to print the information for a person or a student.

# The Interface and Implementation Files for the Person Class

We first give the interface and implementation files for the *Person* class. This class is independent and can be used in conjunction with an application file. Program 11.2 shows the interface file for the *Person* class.

# **Program 11.2**  File person.h

```
```cpp
/*********************************************************
 * The interface file for the Person class                *
 *********************************************************/

#ifndef PERSON_H
#define PERSON_H
#include <cassert>
#include <iostream>
#include <iomanip>
using namespace std;

class Person
{
```
```

*(continued)*