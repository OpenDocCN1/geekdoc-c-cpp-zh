
programming language (ECMA-334), and the C++/CLI programming language. For information about these industry standards, please go to the ECMA Web site that pertains to Technical Committee 39: http://www.ecma-international.org/. You can also refer to Microsoft’s own Web site: http://msdn.microsoft.com/en-us/netframework/a569283.aspx. In addition, Microsoft has applied their Community Promise to the ECMA-334 and ECMA-335 specifications. For more information about this, see http://www.microsoft.com/openspecifications/en/us/programs/community-promise/default.aspx.

The CTS specification states that a type can contain zero or more members. In Part II, “Designing Types,” I’ll cover all of these members in great detail. For now, I just want to give you a brief introduction to them:

- **Field**  A data variable that is part of the object’s state. Fields are identified by their name and type.
- **Method**  A function that performs an operation on the object, often changing the object’s state. Methods have a name, a signature, and modifiers. The signature specifies the number of parameters (and their sequence), the types of the parameters, whether a value is returned by the method, and if so, the type of the value returned by the method.
- **Property**  To the caller, this member looks like a field. But to the type implementer, it looks like a method (or two). Properties allow an implementer to validate input parameters and object state before accessing the value and/or calculating a value only when necessary. They also allow a user of the type to have simplified syntax. Finally, properties allow you to create read-only or write-only “fields.”
- **Event**  An event allows a notification mechanism between an object and other interested objects. For example, a button could offer an event that notifies other objects when the button is clicked.

The CTS also specifies the rules for type visibility and access to the members of a type. For example, marking a type as public (called public) exports the type, making it visible and accessible to any assembly. On the other hand, marking a type as assembly (called internal in C#) makes the type visible and accessible to code within the same assembly only. Thus, the CTS establishes the rules by which assemblies form a boundary of visibility for a type, and the CLR enforces the visibility rules.

A type that is visible to a caller can further restrict the ability of the caller to access the type’s members. The following list shows the valid options for controlling access to a member:

- **Private**  The member is accessible only by other members in the same class type.
- **Family**  The member is accessible by derived types, regardless of whether they are within the same assembly. Note that many languages (such as C++ and C#) refer to family as protected.
- **Family and assembly**  The member is accessible by derived types, but only if the derived type is defined in the same assembly. Many languages (such as C# and Visual Basic) don’t offer this

## The Common Language Specification

COM allows objects created in different languages to communicate with one another. On the other hand, the CLR now integrates all languages and allows objects created in one language to be treated as equal citizens by code written in a completely different language. This integration is possible because of the CLR’s standard set of types, metadata (self-describing type information), and common execution environment.

While this language integration is a fantastic goal, the truth of the matter is that programming languages are very different from one another. For example, some languages don’t treat symbols with case-sensitivity, and some don’t offer unsigned integers, operator overloading, or methods to support a variable number of arguments.

If you intend to create types that are easily accessible from other programming languages, you need to use only features of your programming language that are guaranteed to be available in all other languages. To help you with this, Microsoft has defined a Common Language Specification (CLS) that details for compiler vendors the minimum set of features their compilers must support if these compilers are to generate types compatible with other components written by other CLS-compliant languages on top of the CLR.

The CLR/CTS supports a lot more features than the subset defined by the CLS, so if you don’t care about interlanguage operability, you can develop very rich types limited only by the language’s feature set. Specifically, the CLS defines rules that externally visible types and methods must adhere to if they are to be accessible from any CLS-compliant programming language. Note that the CLS rules don’t apply to code that is accessible only within the defining assembly. Figure 1-6 summarizes the ideas expressed in this paragraph.

![](img/3f2c86949cdef7e2f9e27c37c607b28e_29_0.png)

**FIGURE 1-6** Languages offer a subset of the CLR/CTS and a superset of the CLS (but not necessarily the same superset).

As Figure 1-6 shows, the CLR/CTS offers a set of features. Some languages expose a large subset of the CLR/CTS. A programmer will typically want to write in all CLS language, for example, is able to use all of the features the CLR/CTS offers. Most other languages, such as C#, Visual Basic, and Fortran, expose a subset of the CLR/CTS features to the programmer. The CLS defines the minimum set of features that all languages must support.

If you’re designing a type in one language, and you expect that type to be used by another language, you shouldn’t take advantage of any features that are outside of the CLS in its public and protected members. Doing so would mean that your type’s members might not be accessible by programmers writing code in other programming languages.

In the following code, a CLS-compliant type is being defined in C#. However, the type has a few non–CLS-compliant constructs causing the C# compiler to complain about the code.

```csharp
using System;

// Tell compiler to check for CLS compliance
[assembly: CLSCompliant(true)]

namespace SomeLibrary {
    // Warnings appear because the class is public
    public sealed class SomeLibraryType {

        // Warning: Return type of 'SomeLibrary.SomeLibraryType.Abc()'
        // is not CLS-compliant
        public UInt32 Abc() { return 0; }

        // Warning: Identifier 'SomeLibrary.SomeLibraryType.abc()'
        // differing only in case is not CLS-compliant
        public void abc() { }

        // No warning: this method is private
        private UInt32 ABC() { return 0; }
    }
}
```

In this code, the [assembly:CLSCompliant(true)] attribute is applied to the assembly. This attribute tells the compiler to ensure that any publicly exposed type doesn’t have any construct that would prevent the type from being accessed from any other programming language. When this code is compiled, the C# compiler emits two warnings. The first warning is reported because the method Abc returns an unsigned integer; some other programming languages can’t manipulate unsigned integer values. The second warning is because this type exposes two public methods that differ only by case and return type: Abc and abc. Visual Basic and some other languages can’t call both of these methods.

Interestingly, if you were to delete public from in front of 'sealed class SomeLibraryType'

```csharp
// An event
public event EventHandler AnEvent;
}
```

When the compiler compiles this code, the result is a type that has a number of fields and methods defined in it. You can easily see this by using the IL Disassembler tool (ILDasm.exe) provided with the .NET Framework SDK to examine the resulting managed module, which is shown in Figure 1-7.

![](img/3f2c86949cdef7e2f9e27c37c607b28e_32_0.png)

**FIGURE 1-7** ILDasm showing Test type's fields and methods (obtained from metadata).

Table 1-4 shows how the programming language constructs got mapped to the equivalent CLR fields and methods.

**TABLE 1-4** Test Type's Fields and Methods (Obtained from Metadata)

| Type Member | Member Type | Equivalent Programming Language Construct |
| --- | --- | --- |
| AnEvent | Field | Event; the name of the field is AnEvent and its type is System.EventHandler. |
| .ctor | Method | Constructor. |
| Finalize | Method | Finalizer. |
| add_AnEvent | Method | Event add accessor method. |
| get_AProperty | Method | Property get accessor method. |
| get_Item | Method | Indexer get accessor method. |
| op_Addition | Method | + operator. |
| op_Equality | Method | == operator. |
