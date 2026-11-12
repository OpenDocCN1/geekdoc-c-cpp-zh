
PlainBox<string> mySpecialBox = MagicBox<string>();
mySpecialBox.setItem(otherItem);
mySpecialBox.setItem(specialItem); // specialItem is stored!
cout << mySpecialBox.getItem() << endl; // "Riches beyond compare!"

In both situations, the version of setItem that will be called is determined when the program is compiled. In this second case, even though we instantiated a MagicBox object for mySpecialBox, the variable mySpecialBox is of type PlainBox, so the PlainBox version of setItem is called. The same decision logic applies to our function placeInBox.

This code is correct from the compiler's perspective. The compiler assumes it is our intent to have the parameter theBox and the variable mySpecialBox behave as PlainBox objects. We need a way to communicate to the compiler that the code to execute should not be determined until the program is running. This is called **late binding**, which is an aspect of polymorphism. To solve this problem and have both our function and simple-code examples execute as we intend, we need two tools: pointer variables and virtual methods.

VideoNote C++ memory allocation The new operator allocates memory on the free store

## C2.3 Pointers and the Program's Free Store

To take advantage of late binding, we do not want our objects to be in an activation record on the run-time stack. We need another location. When a C++ program begins execution, in addition to the run-time stack, the operating system sets aside memory for the code—called **code storage** or **text stack**—and for any global variables and static variables—called **static storage**. Your program is also given extra memory, called the **heap**, or **free store**, which a programmer can use to store data. Figure C2-2 illustrates these portions of memory.

We allocate memory for a variable on the free store by using the **new operator**. After allocating memory for the variable, the new operator returns the memory address of the variable in the free store so the program can use it. This memory address must be placed in a special type of variable called a **pointer variable**, or simply a **pointer**. A pointer variable contains the location, or address in memory, of a memory cell.

### FIGURE C2-2 Sample program memory layout

![](img/288a0c22d14d2450c1e772f228f867b0_146_0.png)

### FIGURE C2-3 Run-time stack and free store after myBoxPtr points to a MagicBox object and its data member item is set

![](img/288a0c22d14d2450c1e772f228f867b0_147_0.png)

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

### FIGURE C2-4 myBoxPtr and the object to which it points

![](img/288a0c22d14d2450c1e772f228f867b0_148_0.png)

Pointer variables are simply another type of variable and follow the same rules as other variable types. For example, if you declare a pointer variable that points to a ToyBox<string> object, you can have it point only to ToyBox<string> objects, not MagicBox<string> objects or ToyBox<double> objects, as the following statements illustrate:

```
ToyBox<string>* toyPtr = new ToyBox <string>(); // Ok
ToyBox<string>* boxPtr = new MagicBox<string>(); // Error!
ToyBox<string>* somePtr = new ToyBox <double>(); // Error!
```

If you have two pointer variables that can point to the same type of object, you can make them point to the same object by using the assignment operator =. For example, the statement

```
somePtr = toyPtr;
```

makes the variable somePtr point to the same ToyBox object to which toyPtr points. In such cases, it is helpful to think of the assignment operator as copying the value stored within the pointer variable on its right into the pointer variable on its left. Since pointers store addresses of objects, the value copied is the location of an object in the free store. The object itself is not copied. The result is that both pointer variables point to the same object, as shown in Figure C2-5.

If you declare a pointer variable but do not immediately create an object for it to reference, you should set the pointer to nullptr. An assignment like the following one is necessary because C++ does not initialize the pointer for you:

```
ToyBox<int>* myToyPtr = nullptr;
```

### FIGURE C2-5 Two pointer variables that point to the same object

![](img/288a0c22d14d2450c1e772f228f867b0_148_1.png)

### C2.3.1 Deallocating Memory

When the memory to which a pointer variable points is no longer needed, you deallocate it by using the delete operator. You should then set the pointer variable to nullptr as a signal that it no longer references or pointers to an object:

```
delete somePtr;
somePtr = nullptr;
```

If we did not set somePtr to nullptr in this example, somePtr would be an example of a **dangling pointer**, because it would still contain the address of an object that was deallocated. Dangling pointers can be the source of serious errors.

If you use the new operator to allocate memory, you must use the delete operator to deallocate it

Always remember that if a method of a class uses new to create an object, some method of the class must use delete eventually to free the object's memory. It is a characteristic of safe and secure programming that any object allocating memory from the free store also assumes responsibility to deallocate that memory when it is no longer needed.

Pointers give the programmer a great amount of control over how memory is used and when binding occurs, as we will discuss shortly. They also can create severe problems and hard-to-find bugs if not properly used. The two most common errors involving pointers are memory leak and the dangling pointer, as presented in this section. Let's look at how these problems can occur in a program so that you can prevent them in your code.

### C2.3.2 Avoiding Memory Leaks

Memory leaks occur when an object has been created in the free store, but the program no longer has a way to access it. Because the object cannot be accessed, it cannot be deleted and so takes up memory, even though it cannot be used. A program that quickly runs out of memory and crashes if it has several memory leaks. Even a single statement that is called multiple times can cause a memory leak.

Consider the following statements:

```
MagicBox<string>* myBoxPtr = new MagicBox<string>();
MagicBox<string>* yourBoxPtr = new MagicBox<string>();
yourBoxPtr = myBoxPtr; // Results in inaccessible object
```

Figure C2-6 traces the execution of these statements. Eventually, yourBoxPtr points to the same object as myBoxPtr, and so the object to which yourBoxPtr originally pointed is no longer accessible, resulting in the memory leak shown in part c of the figure.

To prevent this leak, we should not create the second object. Instead, either initialize yourBoxPtr to nullptr or simply set it to myBoxPtr:

```
MagicBox<string>* myBoxPtr = new MagicBox<string>();
MagicBox<string>* yourBoxPtr = myBoxPtr;
```

A more subtle memory leak occurs when a function or method creates an object in the free store and loses the pointer to it by either not returning that pointer to the caller or not storing it in a class data member. That is what happens in the function given in Listing C2-1.

```
LISTING C2-1 Poorly written function that allocates memory in the free store

void myLeakyFunction(const double& someItem)
{
    ToyBox<double>* someBoxPtr = new ToyBox<double>();
    someBoxPtr->setItem(someItem);
} // end myLeakyFunction
```

The parameter someItem and the pointer someBoxPtr are both stored in an activation record on the run-time stack and so are automatically destroyed after the function ends. The object created in the free store by new ToyBox<double>(RED) is still in the free store. Since the only reference we had to it was someBoxPtr and that has been destroyed, we no longer have a way to get to that object, and so we have a memory leak.
