new structure aren't that different from the old one and everyone, including the newbies, should pick it up pretty quickly. Again, all predefined functions referenced under this new architecture involve an object (class); thus, the procedures for referencing those functions are very similar to what you might expect when referencing a standard C/C++ method (or member function). Now, not all of our user-defined functions are accessed in the same way (this should become apparent with time). Moreover, not even the best of us can truly claim to know them all, but they're now much easier to access, especially when you're using a visual compiler. The next few paragraphs explain some of the most common extensions.

# ## Characters

The first function we'll define is Char.ToUpper, which literally means to make a letter that is lowercase into one that is uppercase. This function also has an antonym named Char.ToLower, which changes uppercase letters into their lowercase counterparts. The ToUpper function is useful when you cannot control the user's input, as we couldn't in Example 2.2. In that example, I had to ask that you limit your responses to uppercase Y. This was necessary at the time, but is no longer the case, since we can easily rewrite this program to use the ToUpper function (see Example 2.27).

# ### Example 2.27. Using ToUpper.

```
```csharp
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            int Response;

            Console.Write("Input <Y> for YES: ");
            Response = Console.Read();
            Response = char.ToUpper((char) Response);

            if (Response == 'Y')
                Console.WriteLine ("\n You typed {0}!\n", (char) Response);
        }
    }
}
```
```