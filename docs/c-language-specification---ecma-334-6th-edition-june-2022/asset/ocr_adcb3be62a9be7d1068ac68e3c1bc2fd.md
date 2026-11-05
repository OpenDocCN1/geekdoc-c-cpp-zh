# C. Standard library

# C.1 General

A conforming C# implementation shall provide a minimum set of types having specific semantics. These types and their members are listed here, in alphabetical order by namespace and type. For a formal definition of these types and their members, refer to ISO/IEC 23271:2012 Common Language Infrastructure (CLI), Partition IV, Base Class Library (BCL), Extended Numerics Library, and Extended Array Library, which are included by reference in this specification.

This text is informative.

The standard library is intended to be the minimum set of types and members required by a conforming C# implementation. As such, it contains only those members that are explicitly required by the C# language specification.

It is expected that a conforming C# implementation will supply a significantly more extensive library that enables useful programs to be written. For example, a conforming implementation might extend this library by

+   - Adding namespaces.
+   - Adding types.
+   - Adding members to non-interface types.
+   - Adding intervening base classes or interfaces.
+   - Having struct and class types implement additional interfaces.
+   - Adding attributes (other than the ConditionalAttribute) to existing types and members.

End of informative text.

# C.2 Standard Library Types defined in ISO/IEC 23271

```
namespace System
{
    public delegate void Action();

    public class ArgumentException : SystemException
    {
        public ArgumentException();
        public ArgumentException(string message);
        public ArgumentException(string message, Exception innerException);
    }

    public class ArithmeticException : Exception
    {
        public ArithmeticException();
        public ArithmeticException(string message);
        public ArithmeticException(string message, Exception innerException);
    }
```