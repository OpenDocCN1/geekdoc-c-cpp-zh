# Working with Collections

As with other things we've looked at, there are two kinds of collections in Objective-C: the object-oriented versions and the primitive C types. The former, as usual, is built on top of the latter.

In C, there are two kinds of compound data types: arrays and structures. Arrays are just blocks of memory containing the same sort of data. Structures have a fixed layout and may contain different types as elements.

C composite types are a very thin layer of syntactic sugar on pointer arithmetic. When you access an element in an array, the compiler multiplies the array index by the size of one element and adds this to the pointer to the start of the array. When you access an element in a structure, the compiler adds a fixed offset to the pointer to the start of the structure.