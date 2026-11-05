# 10.1.1.3 Static Classes

The static modifier is used to mark the class being declared as a static class. A static class cannot be instantiated, cannot be used as a type, and can contain only static members. Only a static class can contain declarations of extension methods (§10.6.9).

A static class declaration is subject to the following restrictions:

+   * A static class may not include a sealed or abstract modifier. Note, however, that since a static class cannot be instantiated or derived from, it behaves as if it was both sealed and abstract.
+   * A static class may not include a class-base specification (§10.1.4) and cannot explicitly specify a base class or a list of implemented interfaces. A static class implicitly inherits from type object.
+   * A static class can only contain static members (§10.3.7). Note that constants and nested types are classified as static members.
+   * A static class cannot have members with protected or protected internal declared accessibility.

It is a compile-time error to violate any of these restrictions.

A static class has no instance constructors: It is not possible to declare an instance constructor in a static class, and no default instance constructor (§10.11.4) is provided for a static class.

The members of a static class are not automatically static, and the member declarations must explicitly include a static modifier (except for constants and nested types). When a class is nested within a static outer class, the nested class is not a static class unless it explicitly includes a static modifier.

> MAREK SAFAR A sealed class with a private constructor had to be used to simulate static classes in C# 1.0. That is no longer needed, as static classes offer a more elegant way to express this intention, plus the benefit of many compiler checks for operations that are not allowed in a static context.

# 10.1.1.3.1 Referencing Static Class Types

A namespace-or-type-name (§3.8) is permitted to reference a static class if

+   * The namespace-or-type-name is the T in a namespace-or-type-name of the form T.I, or
+   * The namespace-or-type-name is the T in a typeof-expression (§7.5.11) of the form typeof(T).