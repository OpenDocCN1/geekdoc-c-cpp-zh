![](bbox=[0.161, 0.055, 0.632, 0.356])

**FIGURE 1-6** Languages offer a subset of the CLR/CTS and a superset of the CLS (but not necessarily the same superset).

If you’re designing a type in one language, and you expect that type to be used by another language, you shouldn’t take advantage of any features that are outside of the CLS in its public and protected members. Doing so would mean that your type’s members might not be accessible by programmers writing code in other programming languages.

In the following code, a CLS-compliant type is being defined in C#. However, the type has a few non-CLS-compliant constructs causing the C# compiler to complain about the code.

```
~~~csharp
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
~~~
```