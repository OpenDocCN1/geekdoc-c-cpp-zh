```
```csharp
public sealed class BitArray {

    // This is the indexer's get accessor method.
    public Boolean get_Item(Int32 bitPos) { /* ... */ }

    // This is the indexer's set accessor method.
    public void set_Item(Int32 bitPos, Boolean value) { /* ... */ }
}
```
```

The compiler automatically generates names for these methods by prepending `get_` and `set_` to the indexer name. Because the C# syntax for an indexer doesn’t allow the developer to specify an *indexer name*, the C# compiler team had to choose a default name to use for these accessor methods; they chose `Item`. Therefore, the method names emitted by the compiler are `get_Item` and `set_Item`.

When examining the .NET Framework Reference documentation, you can tell if a type offers an indexer by looking for a property named `Item`. For example, the `System.Collections.Generic.List` type offers a public instance property named `Item`; this property is List’s indexer.

When you program in C#, you never see the name of `Item`, so you don’t normally care that the compiler has chosen this name for you. However, if you’re designing an indexer for a type that code written in other programming languages will be accessing, you might want to change the default name, `Item`, given to your indexer’s get and set accessor methods. C# allows you to rename these methods by applying the `System.Runtime.CompilerServices.IndexerNameAttribute` custom attribute to the indexer. The following code demonstrates how to do this:

```
```csharp
using System;
using System.Runtime.CompilerServices;

public sealed class BitArray {

    [IndexerName("Bit")]
    public Boolean this[Int32 bitPos] {
        // At least one accessor method is defined here
    }
}
```
```

Now the compiler will emit methods called `get_Bit` and `set_Bit` instead of `get_Item` and `set_Item`. When compiling, the C# compiler sees the IndexerName attribute, and this tells the compiler how to name the methods and the property metadata; the attribute itself is not emitted into the assembly’s metadata.⁷

Here’s some Visual Basic code that demonstrates how to access this C# indexer:

```
```vb
' Construct an instance of the BitArray type.
```
```

⁷ For this reason, the `IndexerNameAttribute` class is not part of the ECMA standardization of the CLI and the C# language.