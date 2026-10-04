
# Constructing a String Efficiently

The String type represents an immutable string, the FCL provides another type, System.Text.StringBuilder, which allows you to perform dynamic operations efficiently with strings and characters to create a String. Think of StringBuilder as a fancy constructor to create a String that can be used with the rest of the framework. In general, you design methods that take String parameters, not StringBuilder parameters.

Logically, a StringBuilder object contains a field that refers to an array of Char structures. StringBuilder's members allow you to manipulate this character array, effectively shrinking the string or changing the characters in the string. If you grow the string past the allocated array of characters, the StringBuilder automatically allocates a new, larger array, copies the characters, and starts using the new array. The previous array is garbage collected.

When finished using the StringBuilder object to construct your string, "convert" the StringBuilder's character array into a String simply by calling the StringBuilder's ToString method. This creates a new object in the heap that the string was in the StringBuilder at the time you called ToString. At this point, you can continue to manipulate the string inside the StringBuilder, and you can later call ToString again to convert it into another String object.

# Constructing a StringBuilder Object

Unlike with the String class, the CLR has no special information about the StringBuilder class. In addition, most languages (including C#) do not consider the StringBuilder class to be a primitive type. You construct a StringBuilder object as you would any other primitive type.

```
StringBuilder sb = new StringBuilder();
```

The StringBuilder offers many constructors. The job of each constructor is to allocate and initialize the state maintained by each StringBuilder object:

- **Maximum capacity** An Int32 value that specifies the maximum number of characters that can be placed in the string. The default is Int32. MaxValue (approximately 2 billion). It's unusual to change this value. However, you might specify a smaller maximum capacity to ensure that you never create a string over a certain length. Once constructed, a StringBuilder's maximum capacity value can't be changed.

- **Capacity** An Int32 value indicating the size of character array being maintained by the StringBuilder. The default is 16. If you have some idea of how many characters you'll place in the String, you should use this number to set the capacity when constructing the StringBuilder object.

When appending characters to the character array, the StringBuilder detects if the array is trying to grow beyond its capacity. If it is, the StringBuilder automatically doubles the capacity field (the size of the new capacity), and copies the characters from the original array into the new array. The original array will be garbage collected in the future. Dynamically growing the array hurts performance; avoid this by setting a good initial capacity.

- **Character array** An array of Char structures that maintains the set of characters in the "string". The number of characters is always less than equal to the capacity and maximum capacity values. You can use the StringBuilder's Length property to obtain the number of characters used in the array. The Length is always less than or equal to the StringBuilder's capacity value. When constructing a StringBuilder, you can pass a String to initialize the character array. If you do not specify a string, the array initially contains no characters—that is, the Length returns 0.

# StringBuilder Members

Unlike a String, a StringBuilder represents a mutable string. This means that most of StringBuilder's members change the contents in the array of characters and don't cause new objects to be allocated on the managed heap. A StringBuilder allocates a new object only on occasions:

- You dynamically build a string whose length is longer than the capacity you've set.
- You call StringBuilder's ToString method.

Table 14-2 summarizes StringBuilder's members.

| Member | Member Type | Description |
|---|---|---|
| MaxCapacity | Read-only property | Returns the largest number of characters that can be placed in the string. |
| Capacity | Read/write property | Gets or sets the size of the character array. Trying to set the capacity smaller than the string's length or bigger than MaxCapacity throws an ArgumentOutOfRangeException. |
| EnsureCapacity | Method | Guarantees that the character array is at least the size specified. If the value passed is larger than the StringBuilder's current capacity, the current capacity increases. If the current capacity is already larger than the value passed to this method, no change occurs. |
| Length | Read/write property | Gets or sets the number of characters in the "string". This will likely be smaller than the character array's current capacity. Setting this property to 0 resets the StringBuilder's contents to an empty string. |
| ToString | Method | Theless version of this method returns a String representing the StringBuilder's character array. |
| Chars | Read/write indexer property | Gets or sets the character at the specified index into the array. In C#, this is an indexer (parametric property) that you can access using array syntax (). |
| Clear | Method | Clears the contents of the StringBuilder object, as setting its Length property to 0. |

| Member | Member Type | Description |
|---|---|---|
| Append | Method | Appends a single object to the end of the character array, growing the array if necessary. The object is converted to a string using the general format and the culture associated with the calling thread. |
| Insert | Method | Inserts a single object into the character array, growing the array if necessary. The object is converted to a string by using the general format and the culture with the calling thread. |
| AppendFormat | Method | Appends the specified objects to the end of the character array growing the array if necessary. The objects are converted to strings using the formatting and culture provided by the caller. AppendFormat is one of the most common methods used with StringBuilder. |
| AppendLine | Method | Appends a blank line or a string with a blank line to the end of the character array, increasing the capacity of the array if necessary. |
| Replace | Method | Replaces one character with another or string from the character array. |
| Remove | Method | Removes a range of characters from the character array. |
| Equals | Method | Returns true only if both StringBuilder objects have the same capacity, and characters in the array. |
| CopyTo | Method | Copies a subset of the StringBuilder's characters to a Char array. |

One thing to note about StringBuilder methods is that they often return a reference to the same StringBuilder object. This allows a convenient syntax to chain several operations together.

```
StringBuilder sb = new StringBuilder();
String s = sb.AppendFormat("{0} {1}", "Jeffrey", "Richter").Replace(" ", "").Replace(4, 3).ToString();
Console.WriteLine(s); // Jeff-Richter
```

You'll notice that the String and StringBuilder classes don't have full method parity; is, String has ToLower, ToUpper, EndWith, PadLeft, PadRight, Trim, and so on. On the other hand, the StringBuilder class offers a Replace method that allows you to replace characters or strings in a portion (not the whole string). It's unfortunate that there isn't complete parity between these two classes because now you must convert between String and StringBuilder to accomplish certain tasks. For to build a string, convert all characters to uppercase, and then insert a string requires like the following:

```
// Construct a StringBuilder to perform string manipulations.
StringBuilder sb = new StringBuilder();

// Perform some string manipulations using the StringBuilder.
sb.AppendFormat("{0} {1}", "Jeffrey", "Richter").Replace(" ", "-");

// Convert the StringBuilder to a String in
// order to uppercase all the characters.
String s = sb.ToString().ToUpper();
```
