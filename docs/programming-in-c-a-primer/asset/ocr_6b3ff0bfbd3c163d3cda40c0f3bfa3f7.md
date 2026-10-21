# Table 10.2 Some useful stringBuilder methods

| METHOD | OPERATION |
|---|---|
| Append () | Appends a string |
| AppendFormat () | Appends strings using a specific format |
| EnsureCapacity () | Ensures sufficient size |
| Insert () | Inserts a string at a specified position |
| Remove () | Removes the specified characters |
| Replace () | Replaces all instances of a character with a specified one |

C# also supports some special functions known as properties. They are listed in Table 10.3

# Table 10.3 StringBuilder properties

| PROPERTY | PURPOSE |
|---|---|
| Capacity | To retrieve or set the number of characters the object can hold |
| Length | To retrieve or set the length |
| MaxCapacity | To retrieve the maximum capacity of the object |
| [] | To get or set a character at a specified position |

Program 10.3 shows how some of the methods are used for manipulating strings. The program implements the following methods and properties:

+   - Length
+   - Append ()

+   - Indexer []
+   - Insert ()

The System.Text namespace contains the StringBuilder class and therefore we must include the using System.Text directive for creating and manipulating mutable strings.

# Program 10.3 USING STRINGBUILDER METHODS

```
using System.Text; //For using StringBuilder
using System;
class StringBuilderMethod
{
    public static void Main()
    {
        StringBuilder s = new StringBuilder ("Object ");
        Console.WriteLine("Original string : " + s);
        Console.WriteLine("Length : " + s.Length);
        //Appending a string
        s.Append("language ");
        Console.WriteLine("String now : " + s);
        //Inserting a string
        s.Insert(7,"oriented ");
        Console.WriteLine("Modified string : " + s);
        //Setting a character
        int n = s.Length;
```