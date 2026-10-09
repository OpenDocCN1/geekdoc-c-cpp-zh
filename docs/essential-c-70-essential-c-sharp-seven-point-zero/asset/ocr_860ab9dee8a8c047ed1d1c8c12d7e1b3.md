# **LISTING 18.29: Dynamic Programming Using Reflection**

```
```csharp
using System;

// ...
dynamic data =
    "Hello! My name is Inigo Montoya";
Console.WriteLine(data);
data = (double)data.Length;
data = data * 3.5 + 28.6;
if (data == 2.4 + 112 + 26.2)
{
    Console.WriteLine(
        $"{ data } makes for a long triathlon.");
}
else
{
    data.NonExistentMethodCallStillCompiles();
}
// ...
```
```

# **OUTPUT 18.10**

```
```plain
Hello! My name is Inigo Montoya
140.6 makes for a long triathlon.
```
```

In this example, there is no explicit code for determining the object type, finding a particular MemberInfo instance, and then invoking it. Instead, data is declared as type dynamic and methods are called against it directly. At compile time, there is no check as to whether the members specified are available or even a check regarding which type underlies the dynamic object. Hence, it is possible at compile time to make any call so long as the syntax is valid. At compile time, it is irrelevant whether there is really a corresponding member.

However, type safety is not abandoned altogether. For standard CLR types (such as those used in Listing 18.29), the same type checker normally used at compile time for non-dynamic types is instead invoked at execution time for the dynamic type. Therefore, at execution time, if no such member is available, the call will result in a Microsoft.CSharp.RuntimeBinder.RuntimeBinderException.

Note that this capability is not nearly as flexible as the reflection described earlier in the chapter, although the API is undoubtedly simpler. The key difference when using a dynamic object is that it is necessary to