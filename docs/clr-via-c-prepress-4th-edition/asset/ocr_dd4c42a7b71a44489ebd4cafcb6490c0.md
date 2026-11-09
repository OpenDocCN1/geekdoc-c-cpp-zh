value of a symbol will never change. (Defining MaxInt16 as 32767 is a good example.) Let me demonstrate exactly what I mean. First, take the following code and compile it into a DLL assembly:

```
```csharp
using System;

public sealed class SomeLibraryType {
   // NOTE: C# doesn't allow you to specify static for constants
   // because constants are always implicitly static.
   public const Int32 MaxEntriesInList = 50;
}
```
```

Then use the following code to build an application assembly:

```
```csharp
using System;

public sealed class Program {
   public static void Main() {
      Console.WriteLine("Max entries supported in list: "
         + SomeLibraryType.MaxEntriesInList);
   }
}
```
```

You'll notice that this application code references the MaxEntriesInList constant defined in the SomeLibraryType class. When the compiler builds the application code, it sees that MaxEntriesInList is a constant literal with a value of 50 and embeds the Int32 value of 50 right inside the application's IL code, as you can see in the IL code shown below. In fact, after building the application assembly, the DLL assembly isn't even loaded at runtime and can be deleted from the disk because the compiler does not even add a reference to the DLL assembly in the application's metadata.

```
```
.method public hidebysig static void Main() cil managed
{
   .entrypoint
   // Code size       25 (0x19)

   .maxstack  8
   IL_0000:  nop
   IL_0001:  ldstr      "Max entries supported in list: "
   IL_0006:  ldc.i4.s   50
   IL_0008:  box        [mscorlib]System.Int32
   IL_000d:  call       string [mscorlib]System.String::Concat(object, object)
   IL_0012:  call       void [mscorlib]System.Console::WriteLine(string)
   IL_0017:  nop
   IL_0018:  ret
} // end of method Program::Main
```
```

This example should make the versioning problem obvious to you. If the developer changes the MaxEntriesInList constant to 1000 and only rebuilds the DLL assembly, the application assembly is not affected. For the application to pick up the new value, it will have to be recompiled as well. You can't use constants if you need to have a value in one assembly picked up by another assembly at runtime (instead of compile time). Instead, you can use readonly fields, which I'll discuss next.