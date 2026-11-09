When this code is built, the compiler automatically generates a type constructor for SomeType. It's as if the source code had originally been written as follows.

```
internal sealed class SomeType {
   private static Int32 s_x;
   static SomeType() { s_x = 5; }
}
```

Using ILDasm.exe, it's easy to verify what the compiler actually produced by examining the IL for the type constructor. Type constructor methods are always called .cctor (for class constructor) in a method definition metadata table.

In the code below, you see that the .cctor method is private and static. In addition, notice that the code in the method does in fact load a 5 into the static field s_x.

```
.method private hidebysig specialname rtspecialname static
    void .cctor() cil managed
{
   // Code size       7 (0x7)
   .maxstack  8
   IL_0000:  ldc.i4.5
   IL_0001:  stsfld     int32 SomeType::s_x
   IL_0006:  ret
} // end of method SomeType::.cctor
```

Type constructors shouldn't call a base type's type constructor. Such a call isn't necessary because none of a type's static fields are shared or inherited from its base type.

> **Note** Some languages, such as Java, expect that accessing a type causes its type constructor and all of its base type's type constructors to be called. In addition, interfaces implemented by the types must also have their type constructors called. The CLR doesn't offer this behavior. However, the CLR does offer compilers and developers the ability to provide this behavior via the RunClassConstructor method offered by the System.Runtime.CompilerServices.RuntimeHelpers type. Any language that requires this behavior would have its compiler emit code into a type's type constructor that calls this method for all base types. When using the RunClassConstructor method to call a type constructor, the CLR knows if the type constructor has executed previously and, if it has, the CLR won't call it again.

Finally, assume that you have this code.

```
internal sealed class SomeType {
   private static Int32 s_x = 5;

   static SomeType() {
      s_x = 10;
   }
}
```