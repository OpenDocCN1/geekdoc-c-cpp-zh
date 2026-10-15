# System.ObsoleteAttribute

As mentioned earlier, predefined attributes affect the compiler’s and/or the runtime’s behavior. ObsoleteAttribute provides another example of attributes affecting the compiler’s behavior. Its purpose is to help with the versioning of code, providing a means of indicating to callers that a particular member or type is no longer current. Listing 17.24 is an example of ObsoleteAttribute usage. As Output 17.8 shows, any callers that compile code that invokes a member marked with ObsoleteAttribute will cause a compile-time warning, optionally an error.

# LISTING 17.24: Using ObsoleteAttribute

```
class Program
{
    public static void Main()
    {
        ObsoleteMethod();
    }

    [Obsolete]
    public static void ObsoleteMethod()
    {
    }
}
```

# OUTPUT 17.8

```
c:\Sample\Code\obsoleteAttributeTest.cs(24,1): warning CS0612:
Program.ObsoleteMethod()' is obsolete
```

In this case, ObsoleteAttribute simply displays a warning. However, there are two additional constructors on the attribute. One of them, ObsoleteAttribute(string message), appends the additional message argument to the compiler’s obsolete message. The best practice for this message is to provide direction on what replaces the obsolete code. The second constructor is a bool error parameter that forces the warning to be recorded as an error instead.

ObsoleteAttribute allows third parties to notify developers of deprecated APIs. The warning (not an error) allows the original API to continue to work until the developer is able to update the calling code.