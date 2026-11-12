
## FIGURE C2-6 (a) Creating the first object; (b) creating the second object; (c) assignment causes an inaccessible object

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_150_0.png)

We have several options to fix this function. The first is to delete the object before the function terminates. We can do this by adding the lines

```
delete someBoxPtr;
someBoxPtr = nullptr;
```

at the end of the function. If the ToyBox object pointed to by someBoxPtr is needed only by this function, a better implementation choice would have been not to allocate memory from the free store, but to use a local variable such as is done in the following statements:

```
ToyBox<double> someBox(); // someBox is not a pointer variable
someBox.setItem(someItem);
```

If the object created in this function is required outside the function, the function can return a pointer to it so that the caller can access the object. To implement this option, we would change the function's return type from void to ToyBox<double>* and return someBoxPtr, which is a pointer to a ToyBox<double> object. The resulting function definition is

```
ToyBox<double>* pluggedLeakyFunction(const double& someItem)
{
    ToyBox<double>* someBoxPtr = new ToyBox<double>();
    someBoxPtr->setItem(someItem);
    return someBoxPtr;
} // end pluggedLeakyFunction
```

You could call this function by writing statements such as

```
double boxValue = 4.321;
ToyBox<double>* toyPtr = pluggedLeakyFunction(boxValue);
```

Now toyPtr points to the object created by the ToyBox constructor in pluggedLeakyFunction. When a function returns a pointer to an object that it created in the free store, the segment of the program using that pointer must take responsibility for deleting the object. Otherwise, a memory leak could still occur. When documenting such a function, you should add comments to indicate this responsibility. For example, you could precede the definition of pluggedLeakyFunction with these comments:

```
/* Creates an object in the free store and returns a pointer
to it. Caller must delete the object when it is no longer
needed. */
```

Of course, this comment does not prevent a memory leak, but it alerts users of your function about the potential for a leak. The function could still be misused and called with a statement such as

```
pluggedLeakyFunction(boxValue); // Misused; returned pointer is lost
```

in which case the returned pointer to the object in the free store is lost and a memory leak occurs.

The best option for preventing a memory leak is to not use a function to return a pointer to a newly created object. Instead, you should define a class that has a method for this task. The class takes responsibility for deleting the object in the free store and ensures that there is no memory leak. At a minimum, such a class will have three parts: a method that creates the object in the free store, a data field that points to the object, and a method—the destructor—that deletes the object when the class instance is no longer needed. Although C++ Interlude 1 introduced class destructors, we must say more about them now.

> To prevent a memory leak, do not use a function to return a pointer to a newly created object

Every C++ class has a destructor that has the same name as the class, but is preceded by the tilde (~) character. For objects that are local variables, the destructor is called when the activation record containing the object is removed from the run-time stack. If the object was created using new and is stored in the free store, the destructor is called when the client uses the operator delete to free the memory allocated to the object.

Often, the compiler-generated destructor is sufficient for a class, but if the class itself creates an object on the free store by using the new operator, it is a safe and secure programming practice to implement a destructor to ensure that the memory for that object is freed.

Listing C2-2 gives the header file for a GoodMemory class that demonstrates how to avoid a memory leak. The pointer variable in our previous function pluggedLeakyFunction is now a data field in GoodMemory. As long as this field points to an existing object in the free store, we will have access to the object.

```
LISTING C2-2 Header file for the class GoodMemory
/** @file GoodMemory.h */
#include <string>
#include "ToyBox.h"
using namespace std;
class GoodMemory
{
(continues)
```

```
private:
ToyBox<string>* someBoxPtr;
public:
GoodMemory(); // Default constructor
~GoodMemory(); // Destructor
void fixedLeak(const double& someItem);
}; // end GoodMemory
```

Because the class GoodMemory has a pointer variable for a data field, we should define a default constructor to initialize the pointer to nullptr. The destructor for this class simply needs to delete the object to which the pointer points. Listing C2-3 shows the implementation file for this class.

```
LISTING C2-3 Implementation file for the class GoodMemory

/* @file GoodMemory.cpp */
#include "GoodMemory.h"

GoodMemory::GoodMemory() : someBoxPtr(nullptr)
{ // end default constructor

GoodMemory::~GoodMemory()
{ delete someBoxPtr;
} // end destructor

void GoodMemory::fixedLeak(const double& someItem)
{ someBoxPtr = new ToyBox<double>();
someBoxPtr->setItem(someItem);
} // end fixedLeak
```

Unlike the original function myLeakyFunction, as presented in Listing C2-1, the following client function uses the class GoodMemory to guarantee that no memory leak occurs:

```
void goodFunction()
{ double boxValue = 4.321; // Original statement
GoodMemory gmObject; // Create a safe memory object
gmObject.fixedLeak(boxValue); // Perform the task
} // end goodFunction
```

The compiler greatly helps us here. First, the compiler can check to ensure that a GoodMemory object has been created before calling the method fixedLeak. This guarantees a safe memory allocation and deallocation. Then, since the variable gmObject is a local variable, the compiler automatically calls the GoodMemory destructor when execution of the function goodFunction ends. Thus, the memory allocated in the free store is freed.

## C2.3.3 Avoiding Dangling Pointers

As mentioned earlier, a dangling pointer is a pointer variable that no longer references a valid object. Four situations can cause dangling pointers, but we will cover only three of them because we consider the fourth one to be an unsafe practice.2

- As Section C2.3.1 discusses, if you do not set a pointer variable to nullptr after using delete, you leave the pointer dangling.

Situations that can cause a dangling pointer

- Similarly, if you declare a pointer variable but do not assign it a value, the result is a dangling pointer. As with any C++ variable, when C++ creates a pointer variable, its value is undefined. That is, C++ does not automatically initialize or clear the memory that a variable represents. The compiler and the programmer have no way to check that the value in the pointer variable actually points to an object in the free store. That value might simply be whatever was in the memory when the pointer was created. For example, suppose that you write statements such as

```
MagicBox<int>* myMagicBoxPtr;
myMagicBoxPtr->getItem();
```

Here, the pointer variable myMagicBoxPtr is not assigned an object to point to. When the method getItem is called, the program will abort—usually with a segment fault error—because the program treats the value in myMagicBoxPtr as the address of a MagicBox<int> object and tries to find the getItem method at that address. Since it is very unlikely that a MagicBox<int> object happens to be there, the program ends abnormally.

If you need to create a pointer variable but do not have an object for it to point to, you should always set it to nullptr:

```
MagicBox<int>* myMagicBoxPtr = nullptr;
```

Then your code can compare the pointer variable to nullptr to see whether it points to a valid object on the free store, as in the following example:

```
if (myMagicBoxPtr != nullptr)
    myMagicBoxPtr->getItem();
```

If the pointer is not nullptr, you can use the pointer to call a method.

- The third situation that can cause a dangling pointer is subtle, and the best way to guard against it is careful programming. Consider the following statements that we saw earlier when discussing memory leaks:

```
MagicBox<string>* myBoxPtr = new MagicBox<string>();
MagicBox<string>* yourBoxPtr = myBoxPtr;
```

Executing this code results in the memory configuration shown in Figure C2-7, where both yourBoxPtr and myBoxPtr point to the same object. We say that yourBoxPtr is an alias of myBoxPtr since they both refer to the same object. There is nothing wrong with this code so far, and it does not have any memory leaks.

Suppose we then execute the following statements:

```
delete myBoxPtr;
myBoxPtr = nullptr;
yourBoxPtr->getItem();
```
