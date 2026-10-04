In order TeamB's assembly to use TeamA, TeamA must define all of their types as public. However, this means their types are publicly visible to any and all assemblies; developers in another company could write code that uses the public types, and this is not desirable. Maybe the utility makes certain assumptions that TeamB ensures when they write code that uses TeamA's types. What we'd like is have a way for TeamA to define their types as internal while allowing TeamB to access them. The CLR and C# support this via friend assemblies. This friend feature is also useful when you want to have one assembly containing code that performs tests against the internal types within another assembly.

When an assembly is built, it can indicate other assemblies as "friend" using the InternalVisibleTo attribute defined in the System.Runtime.CompilerServices namespace. The attribute has a string parameter that identifies the friend assembly's name and public key (the string you pass to the attribute must not include a version, culture, or processor architecture). Note that friend assemblies can access all of an assembly's internal types as well as its members. Here is an example of how an assembly can specify two strongly named assemblies named "Wintellect" and "Microsoft" as its friend assemblies.

```
using System;
using System.Runtime.CompilerServices; // For InternalVisibleTo attribute
```

```
// This internal types can be accessed by any code written
// in the following assemblies (regardless of version or culture):
[assembly:InternalVisibleTo("Wintellect", PublicKey=12345678...90abcdef")
[assembly:InternalVisibleTo("Microsoft", PublicKey=b77a5c56...1934e089")]
```

```
internal sealed class SomeInternalType {}
internal sealed class AnotherInternalType {}\ }
```

Accessing the above assembly's internal types from a friend assembly is trivial. For example,
here's how friend assembly called "Wintellect" with a public key of "12345678...90abcdef" can access
the internal type SomeInternalType in the preceding assembly.

```
using System;

internal sealed class Foo {
    private static Object SomeMethod() {
        // This "Wintellect" accesses the other assembly's
        // internal type as if it were a public type
        SomeInternalType sit = new SomeInternalType();
        return sit;
}
```

Because the internal members of the types in an assembly become accessible, you should think carefully about accessibility you specify for your type's members andnwhich assemblies you declare as your friends. Note that the C# compiler requires you to use
t /out:<file> switch when compiling the friend assembly (the assembly that does not contain
the InternalVisibleTo attribute). The switch is required because the compiler needs to know
the name of the assembly being compiled in order to determine if the result should be