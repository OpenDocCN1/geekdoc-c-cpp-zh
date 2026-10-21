# Chapter 9

```
{
    if(Top == nullptr)                // If the stack is empty
        return nullptr;                // return nullptr

    Object^ obj = Top->Obj;            // Get box from item
    Top = Top->Next;                   // Make next item the top
    return obj;
}
};
}
```

The IContainer interface class, the Box class, and the Stack class are now in this library. The changes to the original definitions for these classes are shaded. Each class is now public, which makes them accessible from an external assembly. The fields in the Box class are public protected, which means that they are inherited in a derived class as protected fields but are public so far as classes within the parent assembly are concerned. You don’t actually refer to these fields from other classes within the parent assembly so you could have left the fields in the Box class as protected in this case.

When you have built this project successfully, the assembly containing the class library is in a file Ex9_16lib.dll that is in the debug subdirectory to the project directory if you built a debug version of the project or in a release subdirectory if you built the release version. The .dll extension means that this is a dynamic link library or DLL. You now need another project that uses your class library.

# Try It Out    Using a Class Library

Add a new CLR console project with the name Ex9_16 in its own solution as always. You can then modify Ex9_16.cpp as follows:

```
// Ex9_16.cpp : main project file.
// Using a class library in a separate assembly

#include "stdafx.h"
#include "GlassBox.h"
#using <Ex9_16lib.dll>

using namespace System;
using namespace Ex9_16lib;

int main(array<System::String ^> ^args)
{
    array<IContainer^>^ containers = { gcnew Box(2.0, 3.0, 4.0),
                                       gcnew GlassBox(2.0, 3.0, 4.0),
                                       gcnew Box(4.0, 5.0, 6.0),
                                       gcnew GlassBox(4.0, 5.0, 6.0)
                                     };

    Console::WriteLine(L"The array of containers have the following volumes:");
    for each(IContainer^ container in containers)
        container->ShowVolume();        // Output the volume of a box

    Console::WriteLine(L"\nNow pushing the containers on the stack...");

    Stack^ stack = gcnew Stack;        // Create the stack
```