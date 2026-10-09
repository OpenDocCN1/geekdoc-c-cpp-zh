# # The Void Type

Even in the days of Algol 68, the void keyword's meaning had expanded beyond just stating that a function didn't return a value – it had become a type. Rather than being a type that breaks the rules, as in “null and void”, void is a type that is anything. This is a little confusing for the beginner attempting to make sense of void used in a function – does it mean it returns a void type? Only if nothing is the void type and this isn't a good conclusion to draw.

What does void being any type actually mean?

You can't declare a variable of type “anything” because, in C at least, all variables have to have a known type so that the compiler can allocate storage for them. When you use:

```
int myVar;
```

the compiler usually allocates four bytes to the variable, although this is machine-dependent. What would the compiler allocate if you wrote:

```
void myVar;
```

The only sense that a void type can exist is if we can allocate a sensible amount of storage for it. The solution is to use void pointers. As explained in Dive 10, a pointer is a variable that stores the address of another item of data. A pointer always takes the same amount of memory to store, even though it is system-dependent. Of course, what the pointer references can be anything, so:

```
void *myPointer;
```

creates a pointer that can reference anything.

How best to think of a void pointer?

At the lowest level you can think of a void pointer as referencing the start of a block of memory, but this view has a problem. To access parts of the block of memory you would need to do pointer arithmetic. For example, to access the $20^{\text{th}}$ element of the block you might try:

```
myValue=*(myVoidPointer+20);
```

The idea is that the value stored at the address given by myVoidPointer plus 20 is to be retrieved and stored in myValue. The problem here is we don't know what the basic unit of allocation is. In other cases, pointer arithmetic works in units of the basic type being referenced.