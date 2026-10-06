# 120 C++ INTERLUDE 2 Pointers, Polymorphism, mySpecialBox

PlainBox<string> = MagicBox<string>();
mySpecialBox.setItem(otherItem);
mySpecialBox.setItem(specialItem); // specialItem is stored!
cout << mySpecialBox.getItem() << endl; // "Riches beyond compare!"

In both situations, the version of setItem will be determined when the program is running. In this second case, even if we instantiated a MagicBox for mySpecialBox, the variable mySpecialBox is of type PlainBox, so the PlainBox version of setItem is called. The same decision logic could apply to our function placeInBox.

This code is from the compiler's perspective. The compiler assumes it is intent to have the parameter this and the variable mySpecialBox behave as PlainBox objects. We need a way to communicate with the compiler that the code to execute should not be determined until the program is running. This is called late binding, which is an aspect of polymorphism. To solve this problem we have both function and simple-code examples as we intend, we need two tools: pointer variables and virtual methods.

# C2.3 Pointers and the Program's Free Store

To take advantage of late binding, we do not want our objects to be in an activation record on the runtime stack. We need another location. When a C++ program begins execution, in addition to the runtime stack, the operating system sets aside memory for the code—called code storage or text storage—and for any global and static variables—called static storage. Your program is also given extra memory, called the heap, or free store, which a programmer can use to store data. Figure C-2 illustrates these portions of memory.

We allocate a variable on the free store by using the new operator. After allocating memory for the variable, the new operator returns the memory address of the variable in the free store so the program can use it. This memory address must be placed in a special type of variable called a pointer variable, or simply a pointer. A pointer variable contains the location, or address in memory of a cell.

![](bbox=[0.07, 0.373, 0.215, 0.453])

The new operator allocates memory on the free store

# FIGURE C-2 Sample program memory layout

| Run-time stack |
| Free store (Heap) |
| Static storage |
| Code storage |