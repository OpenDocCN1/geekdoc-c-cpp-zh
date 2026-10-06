# FIGURE C2-3 Run-time stack and free store after myboxPtr points to a MagicBox object and its data member is set

Creates variables on the run-time stack Creates an object in the free store

```
MagicBox<string>* myboxPtr = new MagicBox<string>();
string someItem = "Something"
```

Sets the value of the field item

![](bbox=[0.145, 0.246, 0.693, 0.439])

Unlike variables on the run-time stack, which have their memory allocated and deallocated automatically, variables in the free store persist in memory even when the function or method that created them ends. This means that when a programmer allocates memory from the free store for a variable, the programmer has the responsibility to deallocate that memory when the variable is no longer needed. Failure to do so results in a memory leak. A memory leak is memory that is allocated but no longer needed and cannot be accessed or deallocated.

If you allocate memory on the free store, you must deallocate it

To indicate that a variable is a pointer, we place the asterisk * after the type of the data it references. For example, the statement

Indicate a pointer type by writing an asterisk after the data type

```
MagicBox<string>* myboxPtr = new MagicBox<string>();
```

creates a MagicBox object in the free store and stores the address of the object in the local variable myboxPtr. We say that myboxPtr points to a MagicBox object. To call a method of an object that is in the free store, we use the operator ->

```
string someItem = "Something Free";nmyboxPtr->setItem(someItem);
```

Figure C2-3 shows the state of memory and the local variables after the previous statements execute.

Observe that this newly created object has no programmer-defined name. The only way to access its methods is directly via the pointer that we create, by using myboxPtr-> in the previous example. We usually simplify the diagrams to show that only the object in the free store and its pointers are drawn, as in Figure C2-4.

Some programmers place the * next to the name of the variable. The authors of this textbook believe this clearly shows that the variable is of a pointer type.