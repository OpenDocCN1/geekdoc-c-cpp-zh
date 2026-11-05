}

# [Execution Result]

This is the old method.

This is the new method.

(Plus, a compiler warning: 'MyLibrary.OldMethod()' is obsolete: 'Use NewMethod instead')

The [Obsolete] attribute is a metadata tag in C#. When placed above a class, method, or property, it tells the compiler to warn (or error, depending on the setting) when the code is used.

This is incredibly useful for maintaining large codebases, especially when:

+   - You’re refactoring or improving code.
+   - You want to avoid accidental usage of outdated functions.
+   - You need to guide other developers to use updated APIs.

Syntax:

```
[Obsolete("Your message here", true)] // true makes it a compile-time error
```

In the code above, the message "Use NewMethod instead" helps the developer understand what to use in place of the deprecated method.

You can also force the compiler to throw an error instead of just a warning by passing true as the second argument:

```
[Obsolete("Use NewMethod instead", true)]
```