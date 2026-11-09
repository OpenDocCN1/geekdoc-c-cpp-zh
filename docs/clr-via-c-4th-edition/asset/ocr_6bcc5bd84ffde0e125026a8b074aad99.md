# # Constructing a String Efficiently

Because the String type represents an immutable string, the FCL provides another type, System.Text.StringBuilder, which allows you to perform dynamic operations efficiently with strings and characters to create a String. Think of StringBuilder as a fancy constructor to create a String that can be used with the rest of the framework. In general, you should design methods that take String parameters, not StringBuilder parameters.

Logically, a StringBuilder object contains a field that refers to an array of Char structures. StringBuilder's members allow you to manipulate this character array, effectively shrinking the string or changing the characters in the string. If you grow the string past the allocated array of characters, the StringBuilder automatically allocates a new, larger array, copies the characters, and starts using the new array. The previous array is garbage collected.

When finished using the StringBuilder object to construct your string, "convert" the StringBuilder's character array into a String simply by calling the StringBuilder's ToString method. This creates a new String object in the heap that contains the string that was in the StringBuilder at the time you called ToString. At this point, you can continue to manipulate the string inside the StringBuilder, and later you can call ToString again to convert it into another String object.

# ## Constructing a StringBuilder Object

Unlike with the String class, the CLR has no special information about the StringBuilder class. In addition, most languages (including C#) don't consider the StringBuilder class to be a primitive type. You construct a StringBuilder object as you would any other non-primitive type.

```
```csharp
StringBuilder sb = new StringBuilder();
```
```

The StringBuilder type offers many constructors. The job of each constructor is to allocate and initialize the state maintained by each StringBuilder object:

+   - **Maximum capacity** An Int32 value that specifies the maximum number of characters that can be placed in the string. The default is Int32.MaxValue (approximately 2 billion). It's unusual to change this value. However, you might specify a smaller maximum capacity to ensure that you never create a string over a certain length. Once constructed, a StringBuilder's maximum capacity value can't be changed.
+   - **Capacity** An Int32 value indicating the size of the character array being maintained by the StringBuilder. The default is 16. If you have some idea of how many characters you'll place in the StringBuilder, you should use this number to set the capacity when constructing the StringBuilder object.

When appending characters to the character array, the StringBuilder detects if the array is trying to grow beyond the array's capacity. If it is, the StringBuilder automatically doubles the capacity field, allocates a new array (the size of the new capacity), and copies the characters from the original array into the new array. The original array will be garbage collected