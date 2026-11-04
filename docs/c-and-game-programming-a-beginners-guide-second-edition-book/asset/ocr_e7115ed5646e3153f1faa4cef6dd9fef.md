# Example 1.49. Using and namespace.

```
using sys = System;

namespace Chapter1 {
    class Class1 {
        static void Main() {
            sys.Console.WriteLine("Hello, world!");
        }
    }
}
```

# Hungarian Notation

Hungarian notation, named for the ethnicity of its developer Charles Simonyi, is Microsoft's formal way of identifying variables based on their data types. This notation is used by many programmers, especially those who work for Microsoft, and it is not limited to the C++ language. The notation uses prefixes attached to variables that are always written in lowercase. For example, the prefix that identifies a character is simply the letter c, thus, a declaration of a character can be as simple as (char cVariable:). The integer data type is identified with the letter i, the letter n identifies a short integer, and l indicates a long integer (e.g., int ipassword; short nID; and lAccount). (Note: While there is less of a need for such notation, we still use Pascal/Camel Notation as part of our C# references—see Table 1.6).

![](bbox=[0.12, 0.73, 0.22, 0.85])

> Hungarian notation does not include prefixes for the data types float, double, or decimal. This makes sense, since they're all floating point variables and the lack of notation is in essence a form of notation.

We might also consider the reasoning that floating point variables should always reflect their data requirements, and should only be converted or declared using higher precision data types in order to avoid data loss.