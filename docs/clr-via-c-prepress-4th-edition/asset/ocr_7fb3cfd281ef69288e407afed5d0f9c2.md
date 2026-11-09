# **FIGURE 1-6** Languages offer a subset of the CLR/CTS and a superset of the CLS (but not necessarily the same superset).

As Figure 1-6 shows, the CLR/CTS offers a set of features. Some languages expose a large subset of the CLR/CTS. A programmer will typically want to write in all CLS language, for example, is able to use all of the features the CLR/CTS offers. Most other languages, such as C#, Visual Basic, and Fortran, expose a subset of the CLR/CTS features to the programmer. The CLS defines the minimum set of features that all languages must support.

If you’re designing a type in one language, and you expect that type to be used by another language, you shouldn’t take advantage of any features that are outside of the CLS in its public and protected members. Doing so would mean that your type’s members might not be accessible by programmers writing code in other programming languages.

In the following code, a CLS-compliant type is being defined in C#. However, the type has a few non–CLS-compliant constructs causing the C# compiler to complain about the code.

```
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
```

In this code, the [assembly:CLSCompliant(true)] attribute is applied to the assembly. This attribute tells the compiler to ensure that any publicly exposed type doesn’t have any construct that would prevent the type from being accessed from any other programmed language. When this code is compiled, the C# compiler emits two warnings. The first warning is reported because the method Abc returns an unsigned integer; some other programming languages can’t manipulate unsigned integer values. The second warning is because this type exposes two public methods that differ only by case and return type: Abc and abc. Visual Basic and some other languages can’t call both of these methods.

Interestingly, if you were to delete public from in front of 'sealed class SomeLibraryType'