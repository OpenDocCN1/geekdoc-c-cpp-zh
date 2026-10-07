# Chapter 3: More with Data Types

LISTING 3.23: Retrieving the Length of an Array

```
Console.WriteLine(
  "$There are {languages.Length} languages in the array.");
```

Arrays have a fixed length; they are bound such that the length cannot be changed without re-creating the array. Furthermore, the bounds overstepping (or length) of the array will cause the runtime to report an error. This can occur when you attempt to access (either retrieve or assign) the array with an index for which no element exists in the array. Such error frequently occurs when you use the array length index into the array, as shown in Listing 3.24.

LISTING 3.24: Accessing Outside the Bounds of an Array, Throwing an Exception

```
string[] languages = new string[9];
// ...
// RUNTIME ERROR: index out of bounds - should
// be 8 for the last element
languages[4] = languages[9];
```

> NOTE
The Length member returns the number of items in the array, not the highest index. The Length member for the languages variable is 9, but the highest runtime allowable index for the languages variable is 8, because that is how far it is from the start.

# Language Contrast: C++—Buffer Overflow Bugs

Unmanaged C++ does not always check whether you overstep the bounds of an array. Not only can this be difficult to debug, but making this mistake can also result in a potential security vulnerability called a buffer overrun. In contrast, the Common Language Runtime protects all C# (and Managed C++) code from overstepping array bounds, virtually eliminating the possibility of a buffer overflow issue in managed code.