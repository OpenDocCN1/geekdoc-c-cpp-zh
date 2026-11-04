
![](img/a16f85e62ce9bdc527f4b09dbfe26092_55_0.png)

FIGURE 1.5 Use of the IL disassembler to inspect assemblies.

### NOTE

If you wonder where the application icon of ILDASM comes from, try to remember the initial code name of the CLR that was mentioned earlier in this chapter.

### NOTE

ILDASM has a sister tool called ILASM, the IL assembler. Instead of writing in higher-level languages like C# and VB, you could use this tool to assemble handwritten IL code. However, this is a very extreme approach to managed code development. A slightly more common use of ILASM is to use it in combination with ILDASM to do “IL round-tripping”: Given an input assembly, it's disassembled into IL, tweaked by hand or with some tool, and reassembled. The ILDASM and ILASM tandem has been specifically designed to make such lossless round-tripping possible.

## The Assembly Manifest

To start, there's a manifest that describes the identity of our assembly, its dependencies, and a couple of flags. For our little application, the manifest looks like this (omitting a few irrelevant details):

```
// Metadata version: v4.0.30319
.assembly extern mscorlib
{
.publickeytoken = (B7 7A 5C 56 19 34 E0 89 )
.ver 4:0:0:0
}
.assembly intro
{
.hash algorithm 0x00000004
.ver 0:0:0:0
}
.module intro.exe
.imagebase 0x00400000
.file alignment 0x00000200
.stackreserve 0x00100000
.subsystem 0x0003    // WINDOWS_CUI
.corflags 0x00000001    // ILONLY
```

From the first comment line, we can see the metadata (and hence runtime) version for which this assembly was built.

### .NET FRAMEWORK VERSION HISTORY

Different versions of the CLR have been built over the first decade of the .NET platform's existence. However, not every version of the .NET Framework implies a new version of the underlying runtime. The first release of the .NET Framework came with CLR v1.0.3705 and was quickly updated to v1.1.4322 in the v1.1 release of the framework. A major extension to the runtime, introducing generics, was on the menu for version 2 of the framework with version number v2.0.50727. If you're curious about what the big build number stands for: 2005/07/27.

The next few releases of the .NET Framework, versions 3.0 and 3.5, didn't introduce fundamental changes to the CLR but added lots of libraries such as Windows Presentation Foundation (WPF), Windows Communication Foundation (WCF), Windows Workflow Foundation (WF), and Language Integrated Query (LINQ). In other words, version 3.0 and 3.5 of the .NET Framework came with the v2.0 CLR.

Now, with the fourth version of the framework, a major update to the CLR is shipped as well, primarily improving the runtime services offered by the execution engine. The underlying IL instruction set and metadata formats are kept compatible, though, to ensure a smooth transition to the latest and greatest release of the .NET Framework with binary compatibility for assemblies. For the curious, the full .NET 4 version number is 4.0.30319.

The next entry in the manifest indicates an external assembly reference, which denotes a dependency for our assembly. This assembly, mscorlib, is one of the core parts of the BCL. Notice how version info about the referenced assembly is present; this is one of the keys to eliminating the DLL version hell that existed before the advent of .NET. Besides our own assembly's identity, general information about its characteristics (for example, the fact it's a console user interface, or CUI) is kept in the manifest.

## IL Code

By now we already know the role of IL code as a language-independent format in which to express instructions. However, its generic nature extends in the other direction, too: Being an intermediate representation, it also allows decoupling from the specifics of any

### PROTECTING YOUR INTELLECTUAL PROPERTY

People sometimes worry about how to protect their software's intellectual property (IP) when dealing with managed code, which is easy to inspect and even to decompile with tools like .NET Reflector. The benefits of self-describing assemblies are huge (for example, to aid in debugging scenarios), but concerns like IP are equally important to consider. Luckily, tools exist to obfuscate managed code to make reverse engineering much harder. For example, .NET Reflector itself is protected using such a technique. Visual Studio ships with a community edition of a product called Dotfuscator that's designed to do precisely this.

## Metadata

The last piece in the puzzle to turn assemblies to execution is metadata. It describes all the types contained in the defined assembly in excruciating detail so that the runtime can set up the required infrastructure to make execution possible. Tools also benefit from having self-describing assemblies. The whole metadata system provided by the CLI is in fact much like a relational database of related pieces of data, which makes it possible to query various kinds of relationships. For instance, given a type, it's easy to find all its members, and the reverse relationship is equally easy to traverse. The .NET library that makes introspection of types possible at runtime is called Reflection.

As a developer, you don't have to worry much about metadata. Language compilers on the .NET platform take the responsibility of emitting the necessary metadata details about the types you as a developer define during your day-to-day programming job. However, the flexibility of metadata allows for lots of scenarios that reach beyond the metadata required to describe types. Using a feature called custom attributes, it's possible to tag various entities such as types, members, parameters, and so on with custom metadata. Such metadata can then be consumed at runtime by libraries to facilitate operations such as serialization or exposure of methods through web services.

To illustrate matters, let's take a look at the metadata describing the Calculator class from our example:

```
TypeDef #2 (02000003)
.......................................................
    TypDefName: Calculator  (02000003)
    Flags      : [Public] [AutoLayout] [Class] [AnsiClass] [BeforeFieldInit]
                 (00100101)
    Extends    : 01000001 [TypeRef] System.Object
    Method #1 (06000002)
.......................................................
    MethodName: Add (06000002)
    Flags      : [Public] [HideBySig] [ReuseSlot]    (00000086)
    RVA        : 0x0000209e
    ImplFlags  : [IL] [Managed]      (00000000)
CallConv: [DEFAULT]
hasThis
ReturnType: I4
2 Arguments
    Argument #1: I4
    Argument #2: I4
2 Parameters
    (1) ParamToken : (08000001)
        Name : a
        flags: [none] (00000000)
    (2) ParamToken : (08000002)
        Name : b
        flags: [none] (00000000)

Method #2 (06000003)
--------------------------------------------------
MethodName: .ctor (06000003)
Flags      : [Public] [HideBySig] [ReuseSlot] [SpecialName]
            [RTSpecialName] [.ctor]   (00001886)
RVA        : 0x000020a3
ImplFlags  : [IL] [Managed]   (00000000)
CallConv: [DEFAULT]
hasThis
ReturnType: Void
No arguments.
```

Here, you can observe the names of types and members associated with several flags (for things such as visibility, method table layouts, and so forth). In addition, notice that every piece of metadata has a unique number that allows for other pieces of metadata to cross-reference it.

## Mixing Languages

In the previous discussion, you’ve seen how to use a single language, in our case C#, to build a complete application. This seldom is the case in a real-world environment where libraries from various sources need to be combined to provide an end-to-end solution to the problem at hand. In fact, our use of BCL types like System.Random and System.Console is a good example of such a scenario. Although those happen to be written in C# too, as most of the code in BCL is, that’s not a requirement at all thanks to the cross-language capabilities provided by the CLR. However, consuming libraries is just the tip of the language interoperability iceberg. Richer capabilities, such as extending existing types in a different language than they were initially written in, is also part of the picture.

Let’s explore this angle to the CLR in a more concrete fashion. Instead of compiling our Calculator class as part of an executable assembly, we’ll compile it into a library with a .dll extension. As a matter of fact, the runtime cares little about the file extension to an assembly, apart from the fact that EXE files are supposed to have an entry-point method.
