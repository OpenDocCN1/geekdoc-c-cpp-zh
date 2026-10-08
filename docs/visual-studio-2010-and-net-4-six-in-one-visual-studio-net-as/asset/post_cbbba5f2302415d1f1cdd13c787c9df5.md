
The C# 4.0 language specification calls these invalid type parameters output-unsafe and input-unsafe types, which precisely defines the they are unsafe within. With the introduction of variant type parameters, the type inference algorithm used by the compiler has been modified.

## Variance and Reflection

The .NET Framework's reflection model can be used to obtain information about the variance of a type parameter. In Listing 24-10, we have a simple application's Program.cs file demonstrating the reflection model to query variance information.

+ LISTING 24-10: Program.cs to query reflection about variance

```csharp
using System;
using System.Reflection;
using System.Collections.Generic;
using System.Linq;

namespace VarianceAndReflection
{
    class Program
{
        static void Main(string[] args)
        {
            var asm = typeof(IEnumerable<>>).Assembly;

            var genericTypes = from type in asm.GetTypes()
                               where type.IsGenericTypeDefinition && type.IsPublic
                               select type;

            foreach (var type in genericTypes)
            {
                Console.WriteLine("*", type.Name);
                foreach (var param in type.GetGenericArguments())
                {
                    var variance = type.GenericParameterAttributes & 
                                   GenericParameterAttributes.VarianceMask;
                    if ((variance & GenericParameterAttributes.Covariant) != 0)
                        Console.WriteLine("*(0): covariant", param.Name);
                    else if ((variance & GenericParameterAttributes.Contravariant) != 0)
                        Console.WriteLine("*(0): contravariant", param.Name);
                    else
                        Console.WriteLine("*(0): invariant", param.Name);
                }
            }
        }
    }
}
```

Code file [Program.cs] available for download at Wrox.com

This code iterates through all generic types in the System assembly and writes out their parameter information. The nested foreach cycle goes through the type parameters, and uses the GenericParameterAttributes property of System.Type to obtain information about variance. This property's value is a GenericParameterAttributes enumeration with flags. The VarianceMask of the enumeration can be used to separate the flags indicating variance from the ones describing type constraints. Covariant and Contravariant flags define the parameter behavior. If neither is set, the type parameter is invariant.

## SUMMARY

The major theme for C# 4.0 is dynamic programming. You have a new featured dynamic lookup to bypass the C# compile-time static type checking. Utilizing the new dynamic type operations on this type's instances will get resolved at run-time with the help of Dynamic Language-Runtime (DLR).

Some APIs (most notably COM interfaces such as the Microsoft Office and Visual Studio automation APIs) are written specifically with named and optional parameters in mind. Up until now, it has been very painful to call these APIs from C#. With named and optional parameters introduced in C# 4.0, this kind of discommodity has been finally removed from the language.

The C# design team felt that they should complete the COM interoperability picture in version 4.0, and they added COM-specific features to the language, as COM type import with the dynamic type, simplified syntax for indexed properties, automatic code generation for omitted ref parameters, and support for the no-PIA compliance.

C# 4.0 introduced new forms of variance. With type parameters of generic interfaces and delegates signified as covariant or contravariant, from now on, the programming language has a much more flexible substitution model ever before.

Chapter 25 provides an overview of other .NET languages, such as F#, IronPython, and IronRuby. You can learn the importance of functional programming through the great features of the F# language, and the chapter will also teach you to use F# with Visual Studio.

# PART VI

# F#

+ ▶ CHAPTER 25: Visual F# and the Other .NET Languages

## Visual F# and the Other .NET Languages

One of the most exciting changes in Visual Studio 2010 is the inclusion of F# as a standard front end, bringing a true functional programming language into the .NET language ecosystem.

The importance of functional programming cannot be underestimated. Throughout this book, you have seen many of the various enhancements to C# and Visual Basic (VB) are mostly about bringing functional programming concepts into those languages. This chapter will provide you with a basic understanding of better functional programming, as well as an introduction to the F# language, a foundation that you can build on to better understand F# programs and write them yourself. By the end of this chapter, you will be familiar with the following:

- A brief history of the F# programming language.
- The core functional programming concepts from a pragmatic viewpoint — why they matter and how you can become a better programmer by using functional ideas.
- How you can get started with developing F# programs in Visual Studio, and try them interactively as you are developing them with F# Interactive.
- An overview of the F# language — basic syntax, major features (including pattern matching, active patterns, quotations, computation expressions (workflows), asynchronous computations, and units of measure), and how to use them to get the most of the language.
- How you can develop a set of modules that you can use with F# Interactive to draw mathematical plots from your development session.
- A brief look at a couple of other .NET languages, IronRuby and IronPython.

## A BRIEF functional HISTORY of F#

F# is a functional programming language that grew out of the work of Don Symme and his team at Microsoft Research (MSR) in Cambridge, United Kingdom. Symme and his team set out to implement a .NET front for a functional programming language similar to OCaml. In fact, the initial goal of F# was to port OCaml to .NET, which, in turn, had identified many of the weaknesses of the early .NET 1.1 Common Type System (CTS).

One of the key features that OCaml and the .NET languages at the time lacked was OCaml's mature type system. In particular, the type system of .NET 1.1 was unable to express what is called parametric polymorphism, a key feature of many functional programming languages. This was eventually added to .NET 2.0 as Generics by others, Don Symme and Andrew Kennedy, making it possible to implement the first port of a functional programming language of .NET.

Although F# had some beginnings around 2002, crowds didn't start building around 2004–2005. These were silent but very productive releases from Don Symme's team (which included original member James Marsden) some impressive batches of new features drawing more and more people's attention to F#. The community started to shape, and many initiatives took off, including theF# (https://cs.ffs.net), a community site that aimed to be the primary place for F# enthusiasts — now numbering more than 16,000 members as of January 2010.

The first books on F# appeared in 2007 — Robert Pickering's Foundations of F# (New York: Apprentice) and Don Symme's Expert F# (New York: Apprentice). These books helped introduce F# to a multitude of developers, and the language gradually became well known in professional .NET programming camps.

Undoubtedly, the growing interest in the functional paradigm, and the expressive coding that F# delivers, helped F# make up to the strategic plans of Microsoft. Microsoft quickly realized the potential behind the language, and the project was promptly transferred from MSR Cambridge to Redmond, where it now resides with the other Visual Studio and programming languages teams.

This was followed by public announcements at the end of 2007 — the most notable one being that by Microsoft Division Chief Somaraj, spoke on his blog emphasizing the company's strength to continue the flow of good ideas from functional programming world into mainstream development, and the importance of technology transfer from research to products to “productize” great ideas.

As time has since 2007, F# is much more than a simple product glued together from a set of ideas from functional programming. It is a unique and amazingly effective combination of brevity and productivity, of imperative, object-oriented and mainly functional paradigms, and a mind-changer that offers a truly undeveloped developer experience.
