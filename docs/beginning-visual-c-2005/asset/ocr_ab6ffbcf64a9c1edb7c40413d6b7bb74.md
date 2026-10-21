There are limitations on what types you can supply as a type argument to a generic function. A type argument cannot be a native C++ class type, or a native pointer or reference, or a handle to a value class type such as int^. Thus only value class types such as int or double and tracking handles such as String^ are allowed (but not a handle to a value class type).

Let’s try a working example.

# Try It Out Using a Generic Function

Here’s an example that defines and uses three generic functions:

```
// Ex6_10A.cpp : main project file.
// Defining and using generic functions

#include "stdafx.h"

using namespace System;
```

```
// Generic function to find the maximum element in an array
generic<typename T> where T:IComparable
T MaxElement(array<T>^ x)
{
    T max = x[0];
    for(int i = 1; i < x->Length; i++)
        if(max->CompareTo(x[i]) < 0)
            max = x[i];
    return max;
}
```

```
// Generic function to remove an element from an array
generic<typename T> where T:IComparable
array<T>^ RemoveElement(T element, array<T>^ data)
{
    array<T>^ newData = gcnew array<T>(data->Length - 1);
    int index = 0;                    // Index to elements in newData array
    bool found = false;               // Indicates that the element to remove was found
    for each(T item in data)
    {
        // Check for invalid index or element found
        if((!found) && item->CompareTo(element) == 0)
        {
            found = true;
            continue;
        }
        else
        {
            if(index == newData->Length)
            {
                Console::WriteLine(L"Element to remove not found");
                return data;
            }
            newData[index++] = item;
```