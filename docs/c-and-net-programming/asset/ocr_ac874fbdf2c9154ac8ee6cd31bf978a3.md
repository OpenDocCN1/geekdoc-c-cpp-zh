"APJ Abdul Kalam"
@"Welcome to India"
"HELLO"
"23"
"4"
"a"

```
// C# program showing use of string literals
using System;

class Program
{
    static string  _s1 = "String literal";
    const string  _s2 = "String literal 2";
    const string  _s3 = "String literal 3\r\nAnother line";
    const string  _s4 = @"String literal 4 Another line";
    const string  _s5 = "String literal\t tab";
    const string  _s6 = @"String literal\t tab";

    static void Main()
    {
        // Execution starts here
        string s1 = "String literal \"1\"";
        const string s2 = "String literal 2";
        string s3 = @"String literal ""3""";
        const string s4 = @"String literal 4";
        // Print the string literals.
        Console.WriteLine(
            "{0}\n{1}\n{2}\n{3}\n{4}\n{5}\n{6}\n{7}\n{8}\n{9}",
            _s1, _s2, _s3, _s4, _s5, _s6,
            s1, s2, s3, s4);
    }
}
```

# Output

String literal
String literal 2
String literal 3
Another line
String literal 4
Another line