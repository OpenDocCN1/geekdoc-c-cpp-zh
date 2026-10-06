# Pointers and the Program's Free Store 125

You could call boxValue by writing statements such as

```
double boxValue = 4.321;
ToyBox<double> *toyPtr = pluggedLeakyFunction(boxValue);
```

When nowToyPtr points to an object that it created in pluggedLeakyFunction. When a function returns a pointer to an object that it created in the free store, the memory of the program using that pointer must take responsibility for deleting the object. Otherwise, a memory leak could still occur. When documenting such a function, you should add comments to indicate this responsibility. For example, you could precede the definition of pluggedLeakyFunction with these comments:

```
/* Creates an object in the free store and returns a pointer
to it. Caller must delete the object when it is no longer
needed. */
```

Of course, this comment does not prevent a memory leak, but it alerts users of your function about the potential for a leak. The function could still be misused and called with a statement such as
puggedLeakyFunction(boxValue); // Misused: returned pointer is lost

In which case the best option for avoiding a memory leak is not to use a function to return a pointer to a newly created object. Instead, you should define a class that has a method for this task. This class takes responsibility for deleting the object in the free store and ensures there is no memory leak. At a minimum, a class will have three parts: a method that creates the object in the free store, a data field that points to the object, and a method—the destructor—that deletes the object when the instance is no longer needed. Although C++ introduced class destructors, we must define our own.

Every C++ class has a destructor that has the same name as the class, but it is preceded by the t character. For objects that are local variables, the destructor is called when the activation record is removed from the run-time stack. If the object was created new and is stored in the free store, the destructor is called when the client uses the operator delete to free the memory allocated to the object.

Often, the compiler-generated destructor is sufficient for a class, but if the class creates an object on the new operator, it is a safe and secure programming practice to implement a destructor to ensure the memory for that object is freed.

Listing C2-2 gives the header file for a GoodMemory class that demonstrates how to avoid a memory leak. The pointer variable in our previous function pluggedLeakyFunction is now a data field in GoodMemory. As long as this pointer points to an object created in the free store, we will have access to the object.

LISTING C2-2 Header file for the class GoodMemory
/* @file GoodMemory.h */
#include <string>
#include "ToyBox.h"
using namespace std;
class GoodMemory
{
}
(continues)