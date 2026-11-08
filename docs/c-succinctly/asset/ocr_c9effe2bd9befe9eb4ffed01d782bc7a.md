> > **Note:** An exception to this style is where a programmer is writing code that is meant to be used in both C and C++. Since C does not have a class type, the structure type might instead be used in ways similar to how you would use a class in C++. I'm not going to cover writing C-compatible C++ in this book. To do so, you would need to be familiar with the C language and the differences between it and C++. Instead, we are focusing on writing clean, modern C++ code.

In Windows Runtime (“WinRT”) programming, a public structure can only have data members (no properties or functions). Those data members can only be made up of fundamental data types and other public structures—which, of course, have the same data-only, fundamental, and public-structures-only restrictions. Keep this in mind if you are working on any Metro-style apps for Windows 8 using C++.

You will sometimes see the `friend` keyword used within a class definition. It is followed by either a class name or a function declaration. What this code construct does is give that class or function access to the non-public member data and functions of the class. Typically, you’ll want to avoid this since your class should normally expose everything you want to expose through its public interface. But in those rare instances where you do not wish to publicly expose certain data members or member functions, but do want one or more classes or functions to have access to it, you can use the `friend` keyword to accomplish this.

As classes are a very important part of C++ programming, we will explore them in much more detail later in the book.

# Unions

The union type is a bit odd, but it has its uses. You will encounter it from time to time. A union is a data structure appearing to hold many data members, but only allowing you to use one of its data members at any one time. The end-result is a data structure that gives you many possible uses without wasting memory. The size of the union is required to be large enough only to contain the largest member of the union. In practice, this means the data members overlap each other in memory (hence, you can only use one at a time). This also means you have no way of knowing what the active member of a union is unless you keep track of it somehow. There are many ways you could do that, but putting a union and an enum in a structure is a good, simple, tidy way of doing it. Here's an example.

**Sample: UnionSample\UnionSample.cpp**

```
```cpp
#include <iostream>
#include <sstream>
#include "../pchard.h"

enum class SomeValueDataType
{
        Int = 0,
        Float = 1,
        Double = 2
};

struct SomeData
{
        SomeValueDataType Type;
        union
        {
                int iData;
                float fData;
                double dData;
        } Value;
};
```
```