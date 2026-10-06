# C2.3.3 Avoiding Dangling Pointers

As mentioned earlier, a dangling pointer is a pointer variable that no longer references a valid object. Four situations can cause dangling pointers, but we will cover only three of them because we consider the fourth to be unsafe.

+   * As Section C2.3.1 discusses, if you declare a pointer to nullptr after delete, you leave the dangling pointer.
* Similarly, if you declare a pointer variable but not assign a value to it, the result is a dangling pointer. As with any C variable, when C++ creates a pointer variable, its value is undefined. That is, C++ does not automatically initialize or clear the memory that a variable represents. The compiler and the programmer have no way to check that the value in the pointer variable actually points to the free store. That value might simply be whatever was in the memory when the pointer was created. For example, suppose that you write statements such as

```
MagicBox<int>* myMagicBoxPtr;
MagicBoxPtr->getItem();
```

Here, the variable myMagicBoxPtr is not assigned an object to point to. When the method getItem is called, the program will abort—usually with a segment fault error—because the program tries to access the value in myMagicBoxPtr as the address of a MagicBox<int> object and tries to find the getItem method at address. Since it is very unlikely that the object happens to be at address, the program ends abnormally.

If you need to declare a pointer variable but not have an object for it to point to, you should always set it to nullptr:

```
MagicBox<int>* myMagicBoxPtr = nullptr;
```

Then your code can compare the pointer variable to nullptr to see whether it points to a valid object in the free store, as the following example:

```
if (myMagicBoxPtr != nullptr)
myMagicBoxPtr->getItem();
```

If the pointer is not nullptr, you can use the pointer to call a method.
The third situation that can cause a dangling pointer is deleting the free object, and the best way to guard against it is careful programming. Consider the following statements when we earlier earlier discussing memory leaks:

```
MagicBox<string>* myBoxPtr = new MagicBox<string>();
MagicBox<string>* yourBoxPtr = myBoxPtr;
```

Executing this code in the memory configuration shown in Figure C2-7, where yourBoxPtr and myBoxPtr point to the same object. Wait that yourBoxPtr is an alias of myBoxPtr since they both refer to the same object. There is nothing wrong with this code so far, and it has no memory leaks.

Suppose we execute the following statements:

```
delete myBoxPtr;
myBoxPtr = nullptr;
yourBoxPtr->getItem();
```