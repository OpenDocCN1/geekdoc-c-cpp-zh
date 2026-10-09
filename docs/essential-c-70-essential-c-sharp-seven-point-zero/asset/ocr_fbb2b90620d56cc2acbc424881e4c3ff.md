However, sometimes this is not the case. For example, if your code uses classes that have overlapping behavior names, such an Exists() method on a file and an Exists() method on a directory, then perhaps a using static directive would reduce clarity when you invoke Exists(). Similarly, if the class you were writing had its own members with overlapping behavior names—for example, Display() and Write()—then perhaps clarity would be lost to the reader.

This ambiguity would not be allowed by the compiler. If two members with the same signature were available (through either using static directives or separately declared members), any invocation of them that was ambiguous would result in a compile error.

# **Aliasing**

The using directive also allows **aliasing** a namespace or type. An alias is an alternative name that you can use within the text to which the using directive applies. The two most common reasons for aliasing are to disambiguate two types that have the same name and to abbreviate a long name. In Listing 5.10, for example, the CountdownTimer alias is declared as a means of referring to the type System.Timers.Timer. Simply adding a using System.Timers directive will not sufficiently enable the code to avoid fully qualifying the Timer type. The reason is that System.Threading also includes a type called Timer; therefore, using just Timer within the code will be ambiguous.

```
LISTING 5.10: Declaring a Type Alias
using System;
using System.Threading;
using CountdownTimer = System.Timers.Timer;
class HelloWorld
{
    static void Main()
    {
        CountdownTimer timer;
        // ...
    }
}
```

Listing 5.10 uses an entirely new name, CountdownTimer, as the alias. It is possible, however, to specify the alias as Timer, as shown in Listing 5.11.