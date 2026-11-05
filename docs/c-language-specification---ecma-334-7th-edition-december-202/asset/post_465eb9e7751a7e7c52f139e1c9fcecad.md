
the class A is referenced with global::A and the type System.Net.Sockets.Socket is referenced with S::Socket. Using A.x and S.Socket instead would have caused compile-time errors because A and S would have resolved to the parameters.

end example

Note: The identifier global has special meaning only when used as the left-hand identifier of a qualified_alias_name. It is not a keyword and it is not itself an alias; it is a contextual keyword (§6.4.4). In the code:

```
class A { }

class C
{
    global.A x; // Error: global is not defined
    global::A y; // Valid: References A in the global namespace
}
```

using global.A causes a compile-time error since there is no entity named global in scope. If some entity named global were in scope, then global in global.A would have resolved to that entity.

Using global as the left-hand identifier of a qualified_alias_member always causes a lookup in the global namespace, even if there is a using alias named global. In the code:

```
using global = MyGlobalTypes;

class A { }

class C
{
    global.A x; // Valid: References MyGlobalTypes.A
    global::A y; // Valid: References A in the global namespace
}
```

global.A resolves to MyGlobalTypes.A and global::A resolves to class A in the global namespace.

end note

## 14.8.2 Uniqueness of aliases

Each compilation unit and namespace body has a separate declaration space for extern aliases and using aliases. Thus, while the name of an extern alias or using alias shall be unique within the set of extern aliases and using aliases declared in the immediately containing compilation unit or namespace body, an alias is permitted to have the same name as a type or namespace as long as it is used only with the :: qualifier.

Example: In the following:

```
namespace N
{
    public class A {}
    public class B {}
}

namespace N
{
    using A = System.IO;
    class X
    {
        A.Stream s1; // Error, A is ambiguous
        A::Stream s2; // Ok
    }
}
```

the name A has two possible meanings in the second namespace body because both the class A and the using alias A are in scope. For this reason, use of A in the qualified name A.Stream is ambiguous and causes a compile-time error to occur. However, use of A with the :: qualifier is not an error because A is looked up only as a namespace alias.

*end example*

## 15. Classes

### 15.1 General

A class is a data structure that may contain data members (constants and fields), function members (methods, properties, events, indexers, operators, instance constructors, finalizers, and static constructors), and nested types. Class types support inheritance, a mechanism whereby a derived class can extend and specialize a base class.

### 15.2 Class declarations

### 15.2.1 General

A class_declaration is a type_declaration (§14.7) that declares a new class.

```
class_declaration
: attributes? class_modifier* 'partial'? 'class' identifier
  type_parameter_list? class_base? type_parameter_constraints_clause*
  class_body ';'?
```

A class_declaration consists of an optional set of attributes (§22), followed by an optional set of class_modifiers (§15.2.2), followed by an optional partial modifier (§15.2.7), followed by the keyword class and an identifier that names the class, followed by an optional type_parameter_list (§15.2.3), followed by an optional class_base specification (§15.2.4), followed by an optional set of type_parameter_constraints_clauses (§15.2.5), followed by a class_body (§15.2.6), optionally followed by a semicolon.

A class declaration shall not supply a type_parameter_constraints_clauses unless it also supplies a type_parameter_list.

A class declaration that supplies a type_parameter_list is a generic class declaration. Additionally, any class nested inside a generic class declaration or a generic struct declaration is itself a generic class declaration, since type arguments for the containing type shall be supplied to create a constructed type (§8.4).

### 15.2.2 Class modifiers

### 15.2.2.1 General

A class_declaration may optionally include a sequence of class modifiers:

```
class_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| 'abstract'
| 'sealed'
| 'static'
| unsafe_modifier  // unsafe code support
;
```

unsafe_modifier (§23.2) is only available in unsafe code (§23).

It is a compile-time error for the same modifier to appear multiple times in a class declaration.

The new modifier is permitted on nested classes. It specifies that the class hides an inherited member by the same name, as described in §15.3.5. It is a compile-time error for the new modifier to appear on a class declaration that is not a nested class declaration.

The public, protected, internal, and private modifiers control the accessibility of the class. Depending on the context in which the class declaration occurs, some of these modifiers might not be permitted (§7.5.2).

When a partial type declaration (§15.2.7) includes an accessibility specification (via the public, protected, internal, and private modifiers), that specification shall agree with all other parts that include an accessibility specification. If no part of a partial type includes an accessibility specification, the type is given the appropriate default accessibility (§7.5.2).

The abstract, sealed, and static modifiers are discussed in the following subclauses.

### 15.2.2.2 Abstract classes

The abstract modifier is used to indicate that a class is incomplete and that it is intended to be used only as a base class. An abstract class differs from a non-abstract class in the following ways:

- An abstract class cannot be instantiated directly, and it is a compile-time error to use the new operator on an abstract class. While it is possible to have variables and values whose compile-time types are abstract, such variables and values will necessarily either be null or contain references to instances of non-abstract classes derived from the abstract types.
- An abstract class is permitted (but not required) to contain abstract members.
- An abstract class cannot be sealed.

When a non-abstract class is derived from an abstract class, the non-abstract class shall include actual implementations of all inherited abstract members, thereby overriding those abstract members.

Example: In the following code

```
abstract class A
{
    public abstract void F();
}

abstract class B : A
{
    public void G() {}
}

class C : B
{
    public override void F()
    {
        // Actual implementation of F
    }
}
```

the abstract class A introduces an abstract method F. Class B introduces an additional method G, but since it doesn't provide an implementation of F, B shall also be declared abstract. Class C overrides F and provides an actual implementation. Since there are no abstract members in C, C is permitted (but not required) to be non-abstract.

*end example*

If one or more parts of a partial type declaration (§15.2.7) of a class include the `abstract` modifier, the class is abstract. Otherwise, the class is non-abstract.

### 15.2.2.3 Sealed classes

The `sealed` modifier is used to prevent derivation from a class. A compile-time error occurs if a sealed class is specified as the base class of another class.

A sealed class cannot also be an abstract class.

*Note:* The `sealed` modifier is primarily used to prevent unintended derivation, but it also enables certain run-time optimizations. In particular, because a sealed class is known to never have any derived classes, it is possible to transform virtual function member invocations on sealed class instances into non-virtual invocations. *end note*

If one or more parts of a partial type declaration (§15.2.7) of a class include the `sealed` modifier, the class is sealed. Otherwise, the class is unsealed.

### 15.2.2.4 Static classes

### 15.2.2.4.1 General

The `static` modifier is used to mark the class being declared as a *static class*. A static class shall not be instantiated, shall not be used as a type and shall contain only static members. Only a static class can contain declarations of extension methods (§15.6.10).

A static class declaration is subject to the following restrictions:

- A static class shall not include a `sealed` or `abstract` modifier. (However, since a static class cannot be instantiated or derived from, it behaves as if it was both sealed and abstract.)
- A static class shall not include a `class_base` specification (§15.2.4) and cannot explicitly specify a base class or a list of implemented interfaces. A static class implicitly inherits from type `object`.
- A static class shall only contain static members (§15.3.8).
  *Note:* All constants and nested types are classified as static members. *end note*
- A static class shall not have members with `protected`, `private protected`, or `protected internal` declared accessibility.

It is a compile-time error to violate any of these restrictions.

A static class has no instance constructors. It is not possible to declare an instance constructor in a static class, and no default instance constructor (§15.11.5) is provided for a static class.

The members of a static class are not automatically static, and the member declarations shall explicitly include a `static` modifier (except for constants and nested types). When a class is nested within a static outer class, the nested class is not a static class unless it explicitly includes a `static` modifier.

If one or more parts of a partial type declaration (§15.2.7) of a class include the `static` modifier, the class is static. Otherwise, the class is not static.
