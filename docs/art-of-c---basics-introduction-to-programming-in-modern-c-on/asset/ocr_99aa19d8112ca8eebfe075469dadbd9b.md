properties are allowed, the private property syntax is less commonly used.)

The (private) fields are implementation details, whereas the (public) properties are part of the public APIs for a given type.

> The fields are variables whereas the properties are (essentially) methods in C\#.

The `Cipher` type defines two core APIs as instance methods. Namely, `Encrypt()` and `Decrypt()`.

Since their implementation is "symmetric", we introduce a static helper method, `Rotate()`, in implementing both methods. If the encryption is shifting letters to the left by S, then the decryption is shifting the letters to the right by S.

# Summary

We defined our first custom type using `class` in this lesson. We looked at the constructor and initializer syntaxes for `class` (which are also applicable to `struct`, and `record` and `record struct`, as we will see in the following lessons).

We also discussed some of the essential members of a class, namely, instance fields, instance properties, and instance methods.

> Note that these are normally called just the fields, properties, and methods, respectively, unless they need to be specifically distinguished from the static fields, static properties, and static methods, which we discussed in the first Part.