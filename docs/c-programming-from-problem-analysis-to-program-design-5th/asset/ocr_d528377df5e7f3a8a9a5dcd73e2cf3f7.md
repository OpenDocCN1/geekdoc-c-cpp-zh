# # Address of Operator and Classes

This chapter has used the address of operator, &, to store the address of a variable into a pointer variable. The address of operator is also used to create aliases to an object. Consider the following statements:

```
```
int x;
int &y = x;
```
```

The first statement declares x to be an int variable, and the second statement declares y to be an alias of x. That is, both x and y refer to the same memory location. Thus, y is like a constant pointer variable. The statement:

```
```
y = 25;
```
```

sets the value of y and, hence, the value of x to 25. Similarly, the statement:

```
```
x = 2 * x + 30;
```
```

updates the value of x and, hence, the value of y.

The address of operator can also be used to return the address of a private member variable of a class. However, if you are not careful, this operation can result in serious errors in the program. The following example helps illustrate this idea.

Consider the following class definition:

```
```
//header file testadd.h
```
```

```
```cpp
#ifndef H_testAdd
#define H_testAdd

class testAddress
{
public:
    void setX(int);
    void printX() const;
    int& addressOfX();    //this function returns the address
                          //of the x
private:
    int x;
};

#endif
```
```

The definitions of the functions to implement the member functions are as follows:

```
```
//Implementation file testAdd.cpp
```
```

```
```cpp
#include <iostream>
#include "testAdd.h"
```
```