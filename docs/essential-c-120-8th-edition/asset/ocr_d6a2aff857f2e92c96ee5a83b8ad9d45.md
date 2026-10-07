# Chapter 23: Platform Interoperability and Unsafe Code

behave like a value or a reference type, whether the size is small (approximately
less than 16 bytes).

# Inline Arrays

It can be helpful to declare struct types as buffers. With C# 12.0 structs can be
decorated so that they can be used as a fixed size array. Inline arrays are implicitly
convertible to Span<T> or ReadOnlySpan<T> as an easy way to interact with the
inline array. You can also directly access the elements in the inline array with a
inline indexer suffix, including ranges and index for reading and writing elements.
To create an inline array, declare a struct with a single field and decorated with the
System.Runtime.CompilerServices.InlineArrayAttribute
specifying the size of the inline array in the attribute.

# Skip Initializing Locals

Since C# 1.0, local variables have been initialized to zero values. However, in some
high-performance situations, these zero initialized values are then overwritten. C# 9.0
introduced a new SkipLocalsInitAttribute. This attribute will result in the
compiler not outputting localsinit CIL flag. The result is that locals may not
be initialized. Accessing uninitialized data is discouraged because the behavior
is undefined.

# Error Handling

One inconvenient aspect of Win32 API programming is the fact that the APIs
frequently report errors in inconsistent ways. For example, some APIs return a value
(0, 1, false, and so on) to indicate an error, whereas others set out an
parameter in some way. Furthermore, the details of what went wrong require
additional calls to the GetLastError() API and then an additional call to
FormatMessage() to retrieve an error message corresponding to the error. In
summary, Win32 error reporting in unmanaged code seldom occurs via exceptions.

Fortunately, the P/Invoke designers provided a mechanism for error handling. To enable it, if the SetLastError named parameter of the DllImport attribute is
true, it is possible to instantiate a System.ComponentModel