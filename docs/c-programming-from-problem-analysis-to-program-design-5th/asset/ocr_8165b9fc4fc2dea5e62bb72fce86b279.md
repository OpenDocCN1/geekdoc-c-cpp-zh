Most of these functions are quite straightforward. Let us explain the functions that overload the conversion constructor, the assignment operator, and the copy constructor.

The **conversion constructor** is a single-parameter function that converts its argument to an object of the constructor's class. In our case, the conversion constructor converts a string to an object of the newString type.

Note that the assignment operator is explicitly overloaded only for objects of the newString type. However, the overloaded assignment operator also works if we want to store a C-string into a newString object. Consider the declaration:

```
```cpp
newString str;
```
```

and the statement:

```
```cpp
str = "Hello there";
```
```

The compiler translates this statement into:

```
```cpp
str.operator=("Hello there");
```
```

+   1. First, the compiler automatically invokes the conversion constructor
+      to create an object of the newString type to temporarily store the
+      string "Hello there".
+   2. Second, the compiler invokes the overloaded assignment operator to
+      assign the temporary newString object to the object str.

Hence, it is not necessary to explicitly overload the assignment operator to store a C-string into an object of type newString.

Next, we write a C++ program that tests some of the operations of the class newString.

```
```cpp
//********************************************************
// Author: D.S. Malik
//
// This program shows how to use the class newString.
//********************************************************

#include <iostream>
#include "myString.h"

using namespace std;

int main()
{
    newString str1 = "Sunny";        //initialize str1 using
                                     //the assignment operator
    const newString str2("Warm");    //initialize str2 using the
                                     //conversion constructor
```
```