# Portability Tip 19.1

> Because the size of data items of a particular type is machine dependent, and because storage alignment considerations are machine dependent, so too is the representation of a structure.

# 19.3 Initializing Structures

Structures can be initialized using initializer lists, as is done with arrays. For example, the declaration

```
Card oneCard = { "Three", "Hearts" };
```

creates Card variable oneCard and initializes member face to "Three" and member suit to "Hearts". If there are fewer initializers in the list than members in the structure, the remaining members are initialized to their default values. Structure variables declared outside a function definition (i.e., externally) are initialized to their default values if they are not explicitly initialized in the external declaration. Structure variables may also be set in assignment expressions by assigning a structure variable of the same type or by assigning values to the individual data members of the structure.

# 19.4 Using Structures with Functions

There are two ways to pass the information in structures to functions. You can either pass the entire structure or pass the individual members of a structure. By default, structures are passed by value. Structures and their members can also be passed by reference by passing either references or pointers.

To pass a structure by reference, pass the address of the structure object or a reference to the structure object. Arrays of structures—like all other arrays—are passed by reference.

In Chapter 7, we stated that an array could be passed by value by using a structure. To pass an array by value, create a structure (or a class) with the array as a member, then pass an object of that structure (or class) type to a function by value. Because structure objects are passed by value, the array member, too, is passed by value.

# Performance Tip 19.1

> Passing structures (and especially large structures) by reference is more efficient than passing them by value (which requires the entire structure to be copied).

# 19.5 typedef

Keyword typedef provides a mechanism for creating synonyms (or aliases) for previously defined data types. Names for structure types are often defined with typedef to create shorter, simpler or more readable type names. For example, the statement

```
typedef Card *CardPtr;
```

defines the new type name CardPtr as a synonym for type Card *.

# Good Programming Practice 19.1

> Capitalize typedef names to emphasize that these names are synonyms for other type names.