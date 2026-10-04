| Member | Member Type | Description |
|---|---|--|
| Append | Method | Appends a single object to the end of the character array, growing the array if necessary. The object is converted to a string using the general format and the culture associated with the calling thread. |
| Insert | Method | Inserts a single object into the character array, growing the array if necessary. The object is converted to a string by using the general format and the culture with the calling thread. |
| AppendFormat | Method | Appends the specified objects to the end of the character array growing the array if necessary. The objects are converted to strings using the formatting and culture information provided by the caller. AppendFormat is one of the most common methods used with StringBuilder objects. |
| AppendLine | Method | Appends a blank line or a string with a blank line to the end of the character array, increasing the capacity of the array if necessary. |
| Replace | Method | Replaces one character with another or string from the character array. |
| Remove | Method | Removes a range of characters from the character array. |
| Equals | Method | Returns true only if both StringBuilder objects have the same capacity, and characters in the array. |
| CopyTo | Method | Copies a subset of the StringBuilder's characters to a Char array. |

One thing to note about StringBuilder methods is that they often return a reference to the same StringBuilder object. This allows a convenient syntax to chain several operations together.

```
StringBuilder sb = new StringBuilder();
String s = sb.AppendFormat("{0} {1}", "Jeffrey", "Richter").
Replace(\' ', "").Replace(4, 3).ToString();
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