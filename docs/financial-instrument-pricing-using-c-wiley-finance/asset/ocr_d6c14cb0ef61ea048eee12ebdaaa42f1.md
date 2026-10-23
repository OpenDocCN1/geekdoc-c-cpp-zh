A test program is:

```
using namespace System;

#include "Point.hpp"

int main()
{
    Point^ p=gcnew Point(1.0, 3.0);      // Create Point
    // Shape^ s=gcnew Shape();             // can't be created
    Shape^ sp=gcnew Point(4.5, 3.1);

    p->Draw();                            // Prints 'Draw Point(1.0, 3.0)'
    sp->Draw();                            // Prints 'Draw Point(4.5, 3.1)'

    // Casting
    Shape^ sp2 = gcnew Point(1.0, 2.0);
    try
    {
        Point^ pt = safe_cast<Point^>(sp2);
        Console::WriteLine(L"Coordinates: {0},{1} ", pt->X, pt->Y);
    }
    catch (System::InvalidCastException^ e)
    {
        Console::WriteLine("Cast failed");
    }

    return 0;
}
```

This code can be studied, run and generalised to other problems.

# 27.3 TYPES

The *Common Type System* (CTS) is a key component in the *Common Language Runtime* (CLR). It allows developers to create multi-language applications. In particular, it has the following functions:

+   a) An object-oriented data model to support the data types of all .NET programming languages.
+   
+   b) A set of constraints that the data types of a .NET programming language must satisfy in order to interact with other .NET languages.
+   
+   c) A framework to allow .NET languages to interoperate and to ensure data type safety.

The two main data types are the value type and the reference type. *Value types* (such as int, float and double) as well as user-defined value types are stored as the reference type. *Reference types* (such as arrays, classes and handles) are stored on the managed heap as references to the location of the data type.