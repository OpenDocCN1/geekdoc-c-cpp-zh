
and Strongly Named Assemblies.” The compiler will scan all of the referenced assemblies looking for the type’s definition. Once the compiler finds the proper assembly, the assembly information and the type information is emitted into the resulting managed module’s metadata. To get the assembly information, you must pass the assembly that defines any referenced types to the compiler. The C# compiler, by default, automatically looks in the MSCorLib.dll assembly even if you don’t explicitly tell it to. The MSCorLib.dll assembly contains the definitions of all of the core Framework Class Library (FCL) types, such as **Object**, **Int32**, **String**, and so on.

As you might imagine, there are some potential problems with the way that compilers treat namespaces: it’s possible to have two (or more) types with the same name in different namespaces. Microsoft strongly recommends that you define unique names for types. However, in some cases, it’s simply not possible. The runtime encourages the reuse of components. Your application might take advantage of a component that Microsoft created and another component that Wintellect created. These two companies might both offer a type called Widget—Microsoft’s Widget does one thing, and Wintellect’s Widget does something entirely different. In this scenario, you had no control over the naming of the types, so you can differentiate between the two widgets by using their fully qualified names when referencing them. To reference Microsoft’s Widget, you would use Microsoft.Widget, and to reference Wintellect’s Widget, you would use Wintellect.Widget. In the following code, the reference to Widget is ambiguous, so the C# compiler generates the following message: `"error CS0104: 'Widget' is an ambiguous reference"`.

```csharp
using Microsoft;   // Try prepending "Microsoft."
using Wintellect;  // Try prepending "Wintellect."

public sealed class Program {
    public static void Main() {
        Widget w = new Widget(); // An ambiguous reference
    }
}
```

To remove the ambiguity, you must explicitly tell the compiler which **Widget** you want to create:

```csharp
using Microsoft;   // Try prepending "Microsoft."
using Wintellect;  // Try prepending "Wintellect."

public sealed class Program {
    public static void Main() {
        Wintellect.Widget w = new Wintellect.Widget(); // Not ambiguous
    }
}
```

There’s another form of the C# **using** directive that allows you to create an alias for a single type or namespace. This is handy if you have just a few types that you use from a namespace and don’t want to pollute the global namespace with all of a namespace’s types. The following code demonstrates another way to solve the ambiguity problem shown in the preceding code:

```csharp
using Microsoft;  // Try prepending "Microsoft."
using Wintellect; // Try prepending "Wintellect."

// Define WintellectWidget symbol as an alias to Wintellect.Widget
using WintellectWidget = Wintellect.Widget;

public sealed class Program {
    public static void Main() {
        WintellectWidget w = new WintellectWidget(); // No error now
    }
}
```

These methods of disambiguating a type are useful, but in some scenarios, you need to go further. Imagine that the Australian Boomerang Company (ABC) and the Alaskan Boat Corporation (ABC) are each creating a type, called **BuyProduct**, which they intend to ship in their respective assemblies. It’s likely that both companies would create a namespace called **ABC** that contains a type called **BuyProduct**. Anyone who tries to develop an application that needs to buy both boomerangs and boats would be in for some trouble unless the programming language provides a way to programmatically distinguish between the assemblies, not just between the namespaces. Fortunately, the C# compiler offers a feature called *extern aliases* that gives you a way to work around this rarely occurring problem. Extern aliases also give you a way to access a single type from two (or more) different versions of the same assembly. For more information about extern aliases, see the C# Language Specification.

In your library, when you’re designing types that you expect third parties to use, you should define these types in a namespace so that compilers can easily disambiguate them. In fact, to reduce the likelihood of conflict, you should use your full company name (not an acronym or abbreviation) to be your top-level namespace name. Referring to the Microsoft .NET Framework SDK documentation, you can see that Microsoft uses a namespace of “Microsoft” for Microsoft-specific types. (See the **Microsoft.CSharp**, **Microsoft.VisualBasic**, and **Microsoft.Win32** namespaces as examples.)

Creating a namespace is simply a matter of writing a namespace declaration into your code as follows (in C#):

```csharp
namespace CompanyName {
    public sealed class A {        // TypeDef: CompanyName.A
    }

    namespace X {
        public sealed class B { ... }  // TypeDef: CompanyName.X.B
    }
}
```

The comment on the right of the class definitions above indicates the real name of the type the compiler will emit into the type definition metadata table; this is the real name of the type from the CLR’s perspective.

Some compilers don’t support namespaces at all, and other compilers are free to define what “namespace” means to a particular language. In C#, the **namespace** directive simply tells the compiler to prefix each type name that appears in source code with the namespace name so that programmers can do less typing.

### How Namespaces and Assemblies Relate

Be aware that a namespace and an assembly (the file that implements a type) aren't necessarily related. In particular, the various types belonging to a single namespace might be implemented in multiple assemblies. For example, the `System.IO.FileStream` type is implemented in the `MSCorLib.dll` assembly, and the `System.IO.FileSystemWatcher` type is implemented in the `System.dll` assembly. In fact, the .NET Framework doesn't even ship a `System.IO.dll` assembly.

A single assembly can contain types in different namespaces. For example, the `System.Int32` and `System.Text.StringBuilder` types are both in the `MSCorLib.dll` assembly.

When you look up a type in the .NET Framework SDK documentation, the documentation will clearly indicate the namespace that the type belongs to and also the assembly that the type is implemented in. In Figure 4-1, you can clearly see (right above the Syntax section) that the `ResXFileRef` type is part of the `System.Resources` namespace and that the type is implemented in the `System.Windows.Forms.dll` assembly. To compile code that references the `ResXFileRef` type, you'd add a `using System.Resources;` directive to your source code, and you'd use the `/r:System.Windows.Forms.dll` compiler switch.

![](img/3c46ff5b170881db4209d365b1f7a808_118_0.png)

**FIGURE 4-1** SDK documentation showing namespace and assembly information for a type

![](img/3c46ff5b170881db4209d365b1f7a808_120_0.png)

**FIGURE 4-3** Allocating M1's local variable on the thread's stack

Then, M1 calls the M2 method, passing in the **name** local variable as an argument. This causes the address in the **name** local variable to be pushed on the stack (see Figure 4-4). Inside the M2 method, the stack location will be identified using the parameter variable named **s**. (Note that some architectures pass arguments via registers to improve performance, but this distinction is not important for this discussion.) Also, when a method is called, the address indicating where the called method should return to in the calling method is pushed on the stack (also shown in Figure 4-4).

![](img/3c46ff5b170881db4209d365b1f7a808_120_1.png)

**FIGURE 4-4** M1 pushes arguments and the return address on the thread's stack when calling M2.

When the M2 method starts to execute, its prologue code allocates memory for the local **length** and **tally** variables from the thread's stack (see Figure 4-5). Then the code inside method M2 executes. Eventually, M2 gets to its return statement, which causes the CPU's instruction pointer to be set to the return address in the stack, and M2's stack frame is unwound so that it looks the way it did in Figure 4-3. At this point, M1 is continuing to execute its code that immediately follows the call to M2, and its stack frame accurately reflects the state needed by M1.
