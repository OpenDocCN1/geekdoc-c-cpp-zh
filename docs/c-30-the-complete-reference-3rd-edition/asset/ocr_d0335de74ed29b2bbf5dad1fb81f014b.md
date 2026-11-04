Both house and office were initialized by the Building() constructor when they were created. Each object is initialized as specified in the parameters to its constructor. For example, in the following line,

```
Building house = new Building(2, 2500, 4);
```

the values 2, 2500, and 4 are passed to the Building() constructor when new creates the object. Thus, house’s copy of Floors, Area, and Occupants will contain the values 2, 2500, and 4, respectively.

# The new Operator Revisited

Now that you know more about classes and their constructors, let’s take a closer look at the new operator. As it relates to classes, the new operator has this general form:

```
new class-name(arg-list)
```

Here, class-name is the name of the class that is being instantiated. The class name followed by parentheses specifies the constructor for the class. If a class does not define its own constructor, new will use the default constructor supplied by C#. Thus, new can be used to create an object of any class type.

Since memory is finite, it is possible that new will not be able to allocate memory for an object because insufficient memory exists. If this happens, a runtime exception will occur. (You will learn how to handle exceptions in Chapter 13.) For the sample programs in this book, you won’t need to worry about running out of memory, but you may need to consider this possibility in real-world programs that you write.

# Using new with Value Types

At this point, you might be asking why you don’t need to use new for variables of the value types, such as int or float? In C#, a variable of a value type contains its own value. Memory to hold this value is automatically provided when the program is run. Thus, there is no need to explicitly allocate this memory using new. Conversely, a reference variable stores a reference to an object. The memory to hold this object must be allocated dynamically, during execution.

Not making the fundamental types, such int or char, into reference types greatly improves your program’s performance. When using a reference type, there is a layer of indirection that adds overhead to each object access. This layer of indirection is avoided by a value type.

As a point of interest, it is permitted to use new with the value types, as shown here:

```
int i = new int();
```

Doing so invokes the default constructor for type int, which initializes i to zero. For example:

```
// Use new with a value type.
using System;
class NewValue {
    static void Main() {
        int i = new int(); // initialize i to zero
```