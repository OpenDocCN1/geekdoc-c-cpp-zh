```
public class ThisIsAPublicType { ... }

// The type below has internal visibility and can be accessed by code
// in this assembly only.
internal class ThisIsAnInternalType { ... }

// The type below is internal because public/internal
// was not explicitly stated
class ThisIsAlsoAnInternalType { ... }
```

# Friend Assemblies

Imagine the following scenario: A company has one team, TeamA, that is defining a bunch of utility types in one assembly, and they expect these types to be used by members in another team, TeamB. For various reasons such as time schedules or geographical location, or perhaps different cost centers or reporting structures, these two teams cannot build all of their types into a single assembly; instead, each team produces its own assembly file.

In order for TeamB’s assembly to use TeamA’s types, TeamA must define all of their utility types as public. However, this means that their types are publicly visible to any and all assemblies; developers in another company could write code that uses the public utility types, and this is not desirable. Maybe the utility types make certain assumptions that TeamB assumes when they write code that uses TeamA’s types. What we’d like to have is a way for TeamA to define their types as internal while still allowing TeamB to access the types. The CLR and C# support this via friend assemblies. This friend assembly feature is also useful when you want to have one assembly containing code that performs unit tests against the internal types within another assembly.

When an assembly is built, it can indicate other assemblies it considers “friends” by using the InternalsVisibleTo attribute defined in the System.Runtime.CompilerServices namespace. The attribute has a string parameter that identifies the friend assembly’s name and public key (the string you pass to the attribute must not include a version, culture, or processor architecture). Note that friend assemblies can access all of an assembly’s internal types as well as these type’s internal members. Here is an example of how an assembly can specify two other strongly named assemblies named “Wintellect” and “Microsoft” as its friend assemblies:

```
using System;
using System.Runtime.CompilerServices; // For InternalsVisibleTo attribute

// This assembly's internal types can be accessed by any code written
// in the following two assemblies (regardless of version or culture):
[assembly:InternalsVisibleTo("Wintellect, PublicKey=12345678...90abcdef")]
[assembly:InternalsVisibleTo("Microsoft, PublicKey=b77a5c56...1934e089")]

internal sealed class SomeInternalType { ... }
internal sealed class AnotherInternalType { ... }
```

Accessing the above assembly’s internal types from a friend assembly is trivial. For example, here’s how a friend assembly called “Wintellect” with a public key of “12345678...90abcdef” can access