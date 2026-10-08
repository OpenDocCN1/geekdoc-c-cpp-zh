# 16.12 Class StringBuilder

# 16.12 Append and AppendFormat Methods of Class StringBuilder

Class StringBuilder provides overloaded Append methods that allow various types of values to be added to the end of a StringBuilder. The Framework Library provides versions for each simple type and for character arrays, strings and objects. (Remember that methodToString produces a string representation of any object.) Each method takes an argument, converts it to a string and appends it to the StringBuilder. Figure 16.11 uses several Append methods (lines 22–40) to attach the variables' string representations in lines 10–18 of the StringBuilder.

```
// Fig. 16.11: StringBuilderAppend.cs
// Demonstrating StringBuilder Append methods.
using System;
using System.Text;
class StringBuilderAppend{
    static void Main()
{
        object objectValue = "hello";
        var stringValue = "good bye";
        char[]' = {'a', 'b', 'c', 'd', 'e', 'f'};
        var booleanValue = true;
        var charValue = 'Z';
        var integerValue = 7;
        var longValue = 1000000; // L suffix indicates a long literal
        var floatValue = 2.5F; // F suffix indicates a float literal
        var doubleValue = 33.333;
        var buffer = new StringBuilder();

        // use Append method to append values to buffer
        buffer.append(objectValue);
        buffer.append(" ");
        buffer.append(stringValue);
        buffer.append(" ");
        buffer.append(charArray);
        buffer.append(" ");
        buffer.append(characterArray, 0, 3);
        buffer.append(" ");
        buffer.append(booleanValue);
        buffer.append(" ");
        buffer.append(characterValue);
        buffer.append(" ");
        buffer.append(integerValue);
        buffer.append(" ");
        buffer.append(longValue);
        buffer.append(" ");
        buffer.append(floatValue);
        buffer.append(" ");
        buffer.append(doubleValue);
    }
```

Fig. 16.11 | Demonstrating StringBuilder Append methods. (Part 1 of 2)