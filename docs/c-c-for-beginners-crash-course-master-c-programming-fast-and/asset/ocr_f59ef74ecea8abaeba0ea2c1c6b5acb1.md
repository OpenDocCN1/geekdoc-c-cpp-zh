# Class Methods

Methods in a class specify the behavior of the statement. In the above code, **WriteLine** method is used for writing the value in the console. It is defined in the Console class inside the System namespace.

The **Read** method of the Console class is used for waiting till the user hits a key. Thus prevents the screen from closing too quickly.

# Comments

Comments are text useful for providing additional information about the code. The compiler ignores any code that is placed inside a comment block. There are two types of comments; one comment is used for single line entries and the other for multi line entries.

For example:

```
Example 2:
```csharp
using System;
namespace comment
{
    /*It is a simple code
    Used for writing value to the console
    */
    class Demo
    {
        static void Main()
        {
            //It is added inside Main method
            Console.WriteLine("Demonstration of code");
        }
    }
}
```
```