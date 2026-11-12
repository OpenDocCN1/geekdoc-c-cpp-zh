# FIGURE C2-3 Run-time stack and free store after myBoxPtr points to a MagicBox object and its data member item is set

![](bbox=[0.16, 0.15, 0.73, 0.46])

Unlike variables on the run-time stack, which have their memory allocated and deallocated automatically, variables placed in the free store persist in memory even when the function or method that created them ends. This means that when a programmer allocates memory from the free store for a variable, the programmer has the responsibility to deallocate that memory when the variable is no longer needed. Failure to do so often results in a memory leak. A memory leak is memory that has been allocated for use but is no longer needed and cannot be accessed or deallocated.

> If you allocate memory on the free store, you eventually must deallocate it

To indicate that a variable is a pointer, we place the character * after the type of the data the pointer references. For example, the statement

```
MagicBox<string>* myBoxPtr = new MagicBox<string>();
```

> Indicate a pointer type by writing an asterisk after the data type

creates a MagicBox object in the free store and places the address of the object in the local variable myBoxPtr. We say that myBoxPtr points to a MagicBox object. To call a method of an object that is in the free store, we use the notation ->:

```
string someItem = "Something Free";
myBoxPtr->setItem(someItem);
```

Figure C2-3 shows the state of memory and the local variables after the previous statements execute.

Observe that this newly created object has no programmer-defined name. The only way to access its methods is indirectly via the pointer that new creates, that is, by using myBoxPtr-> as in the previous example. Usually we will simplify the diagrams so that only the object in the free store and its pointer are drawn, as in Figure C2-4.

1 Some programmers place the * next to the name of the variable. The authors of this textbook believe placing the * next to the data type more clearly shows that the variable is of a pointer type.