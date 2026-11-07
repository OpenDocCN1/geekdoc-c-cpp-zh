in this case `TA` class inherits from `StdType` and `PrfType`, but there is no common base class and `StdType` and `PrfType` are not instantiated to create the problem we mentioned for multiple inheritance.

An analogy may help here. Consider an ice cream parlor that sells one type of ice cream and that allows customers to buy up to two extra toppings. A person object gets no topping, a student or a professor object gets one topping, and a teaching assistant object gets two toppings. We assume toppings are not sold without ice cream.

# EXAMPLE 12.5

In this example we develop the code for the mixin classes shown in Figure 12.10. We give the code for five interface files, three implementation files, and one application file. Note that the mixin classes are abstract classes (interfaces) and have no implementations. Program 12.31 shows the interface file the StdType class.

Program 12.32 shows the interface file the PrfType class.

**Program 12.31**  File stdtype.h

```
```cpp
/************************************************************
 * The interface file for StdType abstract class             *
 ************************************************************/
#ifndef STDTYPE_H
#define STDTYPE_H
#include <iostream>
using namespace std;

class StdType
{
protected:
    double gpa;
public:
    virtual void printGPA() = 0 ;
};
#endif
```
```

**Program 12.32**  File prftype.h

```
```cpp
/************************************************************
 * The interface file for PrfType abstract class             *
 ************************************************************/
#ifndef PRFTYPE_H
#define PRFTYPE_H
#include <iostream>
using namespace std;

class PrfType
{
```
```