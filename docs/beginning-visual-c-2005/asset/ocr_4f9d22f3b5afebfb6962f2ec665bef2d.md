the object will be executed, and these operations also suppress the execution of the finalizers for the objects. The object referenced by obj3 is destroyed by the garbage collector when the program ends so the finalizer gets called to clean up any non-managed resources.

Thus, if a class has a finalizer and a destructor, only one of these is called when the object is destroyed, the destructor is called if you programmatically destroy the object, and the finalizer is called if it dies naturally by going out of scope. You can also deduce from this that if you rely on a finalizer to clean up after your objects have been destroyed, you should not explicitly delete the objects.

If you comment out the statements in main() that destroy obj1 and obj2, you will see that the finalizers for these objects are called by the garbage collector when the program ends. On the other hand, if you comment out the finalizer from MyClass, you will see that the destructor for obj3 does not get called by the garbage collector so no clean up occurs. You can conclude that if you want to be sure that unmanaged resources used by an object are taken care of regardless of how an object is terminated, you should implement both a destructor and a finalizer in the class.

# Generic Classes

C++/CLI provides you with the capability for defining generic classes where a specific class is instantiated from the generic class type at run-time. You can define generic value classes, generic reference classes, generic interface classes, and generic delegates. You define a generic class using one or more type parameters in a similar way to generic functions that you saw in Chapter 6.

For example, here’s how you could define a generic version of the Stack class you saw in Ex9_14:

```
// Stack.h for Ex9_21
// A generic pushdown stack

generic<typename T> ref class Stack
{
private:
    // Defines items to store in the stack
    ref struct Item
    {
        T Obj;                  // Handle for the object in this item
        Item^ Next;             // Handle for next item in the stack or nullptr

        // Constructor
        Item(T obj, Item^ next) : Obj(obj), Next(next) {}
    };

    Item^ Top;                  // Handle for item that is at the top

public:
    // Push an object on to the stack
    void Push(T obj)
    {
        Top = gcnew Item(obj, Top);  // Create new item and make it the top
    }

    // Pop an  object off the stack
```