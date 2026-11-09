
```csharp
namespace CompanyA {
    public class Phone {
        public void Dial() {
            Console.WriteLine("Phone.Dial");
            EstablishConnection();
            // Do work to dial the phone here.
        }

        protected virtual void EstablishConnection() {
            Console.WriteLine("Phone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```

Now when CompanyB compiles its **BetterPhone** type (derived from this new version of CompanyA's **Phone**), the compiler issues this message: "warning CS0114: 'CompanyB.BetterPhone.EstablishConnection()' hides inherited member 'CompanyA.Phone.EstablishConnection()'. To make the current member override that implementation, add the override keyword. Otherwise, add the new keyword."

The compiler is alerting you to the fact that both **Phone** and **BetterPhone** offer an **EstablishConnection** method and that the semantics of both might not be identical; simply recompiling **BetterPhone** can no longer give the same behavior as it did when using the first version of the **Phone** type.

If CompanyB decides that the **EstablishConnection** methods are not semantically identical in both types, CompanyB can tell the compiler that the **Dial** and **EstablishConnection** method defined in **BetterPhone** is the correct method to use and that it has no relationship with the **EstablishConnection** method defined in the **Phone** base type. CompanyB informs the compiler of this by adding the **new** keyword to the **EstablishConnection** method:

```csharp
namespace CompanyB {
    public class BetterPhone : CompanyA.Phone {

        // Keep 'new' to mark this method as having no
        // relationship to the base type's Dial method.
        public new void Dial() {
            Console.WriteLine("BetterPhone.Dial");
            EstablishConnection();
            base.Dial();
        }

        // Add 'new' to mark this method as having no
        // relationship to the base type's EstablishConnection method.
        protected new virtual void EstablishConnection() {
            Console.WriteLine("BetterPhone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```

In this code, the **new** keyword tells the compiler to emit metadata, making it clear to the CLR that **BetterPhone**'s **EstablishConnection** method is intended to be treated as a new function that is introduced by the **BetterPhone** type. The CLR will know that there is no relationship between **Phone**'s and **BetterPhone**'s methods.

When the same application code (in the **Main** method) executes, the output is as follows:

```
BetterPhone.Dial
BetterPhone.EstablishConnection
Phone.Dial
Phone.EstablishConnection
```

This output shows that **Main**'s call to **Dial** calls the new **Dial** method defined by **BetterPhone.Dial**, which in turn calls the virtual **EstablishConnection** method that is also defined by **BetterPhone**. When **BetterPhone**'s **EstablishConnection** method returns, **Phone**'s **Dial** method is called. **Phone**'s **Dial** method calls **EstablishConnection**, but because **BetterPhone**'s **EstablishConnection** is marked with **new**, **BetterPhone**'s **EstablishConnection** method isn't considered an override of **Phone**'s virtual **EstablishConnection** method. As a result, **Phone**'s **Dial** method calls **Phone**'s **EstablishConnection** method—this is the expected behavior.

> **Note** If the compiler treated methods as overrides by default (as a native C++ compiler does), the developer of **BetterPhone** couldn't use the method names **Dial** and **EstablishConnection**. This would most likely cause a ripple effect of changes throughout the entire source code base, breaking source and binary compatibility. This type of pervasive change is undesirable, especially in any moderate-to-large project. However, if changing the method name causes only moderate updates in the source code, you should change the name of the methods so the two different meanings of **Dial** and **EstablishConnection** don't confuse other developers.

Alternatively, CompanyB could have gotten the new version of CompanyA's **Phone** type and decided that **Phone**'s semantics of **Dial** and **EstablishConnection** are exactly what it's been looking for. In this case, CompanyB would modify its **BetterPhone** type by removing its **Dial** method entirely. In addition, because CompanyB now wants to tell the compiler that **BetterPhone**'s **EstablishConnection** method is related to **Phone**'s **EstablishConnection** method, the **new** keyword must be removed. Simply removing the **new** keyword isn't enough, though, because now the compiler can't tell exactly what the intention is of **BetterPhone**'s **EstablishConnection** method. To express his intent exactly, the CompanyB developer must also change **BetterPhone**'s **EstablishConnection** method from **virtual** to **override**. The following code shows the new version of **BetterPhone**:

```csharp
namespace CompanyB {
    public class BetterPhone : CompanyA.Phone {

        // Delete the Dial method (inherit Dial from base).

        // Remove 'new' and change 'virtual' to 'override' to
        // mark this method as having a relationship to the base
        // type's EstablishConnection method.
        protected override void EstablishConnection() {
            Console.WriteLine("BetterPhone.EstablishConnection");
            // Do work to establish the connection.
        }
    }
}
```

Now when the same application code (in the **Main** method) executes, the output is as follows:

```
Phone.Dial
BetterPhone.EstablishConnection
```

This output shows that **Main's** call to **Dial** calls the **Dial** method defined by **Phone** and inherited by **BetterPhone**. Then when **Phone's** **Dial** method calls the virtual **EstablishConnection** method, **BetterPhone's** **EstablishConnection** method is called because it overrides the virtual **EstablishConnection** method defined by **Phone**.

## Chapter 7: Constants and Fields

| In this chapter: |  |
| --- | --- |
| Constants | 181 |
| Fields | 183 |

In this chapter, I'll show you how to add data members to a type. Specifically, we'll look at constants and fields.

### Constants

A *constant* is a symbol that has a never-changing value. When defining a constant symbol, its value must be determinable at compile time. The compiler then saves the constant's value in the assembly's metadata. This means that you can define a constant only for types that your compiler considers primitive types. In C#, the following types are primitives and can be used to define constants: **Boolean**, **Char**, **Byte**, **SByte**, **Int16**, **UInt16**, **Int32**, **UInt32**, **Int64**, **UInt64**, **Single**, **Double**, **Decimal**, and **String**. However, C# also allows you to define a constant variable of a non-primitive type if you set the value to `null`:

```csharp
using System;

public sealed class SomeType {
    // SomeType is not a primitive type but C# does allow
    // a constant variable of this type to be set to 'null'.
    public const SomeType Empty = null;
}
```

Because a constant value never changes, constants are always considered to be part of the defining type. In other words, constants are always considered to be static members, not instance members. Defining a constant causes the creation of metadata.

When code refers to a constant symbol, compilers look up the symbol in the metadata of the assembly that defines the constant, extract the constant's value, and embed the value in the emitted Intermediate Language (IL) code. Because a constant's value is embedded directly in code, constants don't require any memory to be allocated for them at runtime. In addition, you can't get the address of a constant and you can't pass a constant by reference. These constants also mean that constants don't have a good cross-assembly versioning story, so you should use them only when you know that the value of a symbol will never change.
