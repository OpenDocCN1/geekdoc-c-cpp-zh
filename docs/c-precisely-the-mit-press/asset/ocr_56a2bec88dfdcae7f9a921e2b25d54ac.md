# 13.9 The checked and unchecked Statements

An operation on integral numeric values may produce a result that is too large. In a checked context, runtime-integer overflow will throw an OverflowException, and compile-time integer overflow will produce a compile-time error. In an unchecked context, both compile-time and run-time integer overflow will wrap around (discard the most significant bits), not throw any exception or a compile-time error.
A checked statement creates a checked context for a block-statement; it has the form

checked
block-statement

An unchecked statement creates an unchecked context for a block-statement; it has the form

unchecked
block-statement

In both cases, only arithmetic operations textually inside the block-statement are affected. Arithmetic operations performed in methods called the block-statement are not affected, whereas arithmetic operations in anonymous delegate expressions and lambda expressions textually inside the block-statement are. These are analogous to checked and unchecked expressions (section 12.3).

# 13.10 The using Statement

The purpose of the using statement is to release a resource res, such as a file handle or database connection, after its use. You may have the form

```
using type res = initializer;
body
```

This declares res to have type type, or if the keyword was used instead of type, the inferred type of initializer (section 6.3). The initializer is evaluated and its result assigned to res, the body is executed, and finally Dispose() is called on res regardless of whether body terminates normally, throws an exception, or exits by return or continue. The type must be implicitly convertible to IDisposable and the body cannot be a declaration statement or a labeled statement. Variable res is read-only; it cannot be assigned to or used as a ref or argument. The statement is equivalent to this:

```
{
  type res = initializer;
  { body }
  finally { if (res != null) {(IDisposable)res).Dispose(); }
}
```

The IDisposable interface for namespace System describes a single method:

+   void Dispose() is called to close or release resources held by an object, such as files, streams, or database connections. Calling multiple times must not throw an exception.

# 13.11 The lock Statement

The lock statement is thread-related and is described in section 21.2.