The nameof( ) expression can be used to get the name of a variable or a constant, as well as the name of a member in a type, in a program. This is mainly useful for the diagnostics purposes, etc.

Note that the argument of nameof( ) is a name/identifier and not a string. We mentioned the @-escape syntax in the previous lesson. What would be the value of the expression nameof(@while) if we declared a variable named @while?

The Example namespace contains one public static class CryptoMD5, which in turn contains one public static method, Hash( ). The Hash( ) method uses the .NET MD5 class defined in the System.Security.Cryptography namespace.

The MD5 type "implements" the System.IDisposable interface, and it implements the void Dispose( ) method of that interface.

The implementation of the IDisposable interface is an indication, e.g., by the creator of the type, that an object of the type uses the system resources and they need to be cleaned up by calling the Dispose( ) method. Not doing so will (likely) lead to a resource leak.

One of the common ways to call Dispose( ) is from inside the finally block. We will cover the exception handling in C#, and try/catch/finally in particular, later in the book. But, for now, there is an easier way.

C# supports an automatic cleanup of the IDisposable resources using the using statement. For an object created with using, the Dispose( ) method does not have to be called explicitly. At the end of the enclosing block (e.g., the method block), the resources are automatically released.

![](bbox=[0.09, 0.74, 0.86, 0.8])

In the code sample, the md5 object is created via the using statement: