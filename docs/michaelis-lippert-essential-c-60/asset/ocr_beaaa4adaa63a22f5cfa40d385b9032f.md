Conversion from a string to an enum is a little more difficult to achieve, because it involves a static method on the System.Enum base class. Listing 8.13 provides an example of how to do it without generics (see Chapter 11), and Output 8.4 shows the results.

# LISTING 8.13: Converting a String to an Enum Using Enum.Parse()

```
ThreadPriorityLevel priority = (ThreadPriorityLevel)Enum.Parse(
    typeof(ThreadPriorityLevel), "Idle");
Console.WriteLine(priority);
```

# OUTPUT 8.4

```
Idle
```

In this code, the first parameter to Enum.Parse() is the type, which you specify using the keyword typeof(). This example depicts a compile-time way of identifying the type, like a literal for the type value (see Chapter 17).

Until .NET Framework 4, there was no TryParse() method, so code written to target prior versions needs to include appropriate exception handling if there is a chance the string will not correspond to an enum value identifier. .NET Framework 4’s TryParse<T>() method uses generics, but the type parameters can be inferred, resulting in the to-enum conversion behavior shown in Listing 8.14.

# LISTING 8.14: Converting a String to an Enum Using Enum.TryParse<T>()

```
System.Diagnostics.ThreadPriorityLevel priority;
if(Enum.TryParse("Idle", out priority))
{
    Console.WriteLine(priority);
}
```

This technique eliminates the need to use exception handling if the string might not convert successfully. Instead, code can check the Boolean result returned from the call to TryParse<T>().

Regardless of whether the code uses the “Parse” or “TryParse” approach, the key caution about converting from a string to an enum is that such a cast is not localizable. Therefore, developers should use this type of cast only for messages that are not exposed to users (assuming localization is a requirement).