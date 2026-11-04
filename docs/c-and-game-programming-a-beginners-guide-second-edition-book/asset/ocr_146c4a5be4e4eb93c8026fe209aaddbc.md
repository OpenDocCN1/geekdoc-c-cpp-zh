# ### Example 1.15. Naming variables.

```
```csharp
using System;

namespace Chapter1 {
    class Class1 {
        static void Main() {
            int OurVariable; // an integer data type.
            OurVariable = 1; // we can assign the value 1 to the variable
            Console.WriteLine("The number is " + OurVariable);
        }
    }
}
```
```

Remember that if you change the name in the declaring line, you’ll also have to change it in the assigning and referencing lines.

| Other possible variable names include: |  |  |  |  |
|---|---|---|---|---|
|  | Number | integer | whole_number | computer_data |
| - | Lives | game_lives | deaths | bombs_on_ship |

# ## Declaring Variables and the Integer Data Types

There are five basic data types: integer (int), float, double, character (char), and void. Each of these has a specific purpose, but to apply these variables properly we must first learn how to declare them. An integer is any positive or negative whole number (see Example 1.16). To declare an integer, use the keyword int, followed by the variable name and a semicolon (Remember the semicolon ends the command line.). We can declare data types using either the common method or by expressly stating their CTS type. We can also declare multiple variables in one program by either repeating the int keyword or adding additional variables to the line as is implied by the use of the comma operator (see Examples 1.17 and 1.18).

# ### Example 1.16. A number line of integers.

-10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10...