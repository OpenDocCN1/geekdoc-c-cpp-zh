# 16.3 string Constructors

Figure 16.1 demonstrates three of class string's constructors.

```
// Fig. 16.1: StringConstructor.cs
// Demonstrating string class constructors.
using System;

class StringConstructor
{
    static void Main()
    {
        // string initialization
        char[] characterArray = {'b', 'i', 'r', 't', 'h', ' ', 'd', 'a', 'y'};
        var originalString = "Welcome to C# programming!";
        var string1 = originalString;
        var string2 = new string(characterArray);
        var string3 = new string(characterArray, 6, 3);
        var string4 = new string('C', 5);

        Console.WriteLine($"string1 = \"{string1}\"\n" +
        $"string2 = \"{string2}\"\n" +
        $"string3 = \"{string3}\"\n" +
        $"string4 = \"{string4}\"\n");
    }
}
```

string1 = "Welcome to C# programming!"
string2 = "birthday"
string3 = "day"
string4 = "CCCCC"

Fig. 16.1 | Demonstrating string class constructors.

Lines 10–11 create the char array characterArray, which contains nine characters. Lines 12–16 declare the strings originalString, string1, string2, string3 and string4. Line 12 assigns string literal "Welcome to C# programming!" to string reference originalString. Line 13 sets string1 to reference the same string literal.

Line 14 assigns to string2 a new string, using the string constructor with a character array argument. The new string contains a copy of the array's characters.

Line 15 assigns to string3 a new string, using the string constructor that takes a char array and two int arguments. The second argument specifies the starting index position (the offset) from which characters in the array are to be copied. The third argument specifies the number of characters (the count) to be copied from the specified starting position in the array. The new string contains a copy of the specified characters in the array. If the specified offset or count indicates that the program should access an element outside the bounds of the character array, an ArgumentOutOfRangeException is thrown.