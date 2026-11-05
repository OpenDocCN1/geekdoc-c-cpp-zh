
- The scope of a name defined by an extern-alias-directive extends over the using-directives, global-attributes and namespace-member-declarations of its immediately containing compilation unit or namespace body. An extern-alias-directive does not contribute any new members to the underlying declaration space. In other words, an extern-alias-directive is not transitive, but, rather, affects only the compilation unit or namespace body in which it occurs.
- The scope of a name defined or imported by a using-directive (§9.4) extends over the namespace-member-declarations of the compilation-unit or namespace-body in which the using-directive occurs. A using-directive may make zero or more namespace or type names available within a particular compilation-unit or namespace-body, but does not contribute any new members to the underlying declaration space. In other words, a using-directive is not transitive but rather affects only the compilation-unit or namespace-body in which it occurs.
- The scope of a type parameter declared by a type-parameter-list on a class-declaration (§10.1) is the class-base, type-parameter-constraints-clauses, and class-body of that class-declaration.
- The scope of a type parameter declared by a type-parameter-list on a struct-declaration (§11.1) is the struct-interfaces, type-parameter-constraints-clauses, and struct-body of that struct-declaration.
- The scope of a type parameter declared by a type-parameter-list on an interface-declaration (§13.1) is the interface-base, type-parameter-constraints-clauses, and interface-body of that interface-declaration.
- The scope of a type parameter declared by a type-parameter-list on a delegate-declaration (§15.1) is the return-type, formal-parameter-list, and type-parameter-constraints-clauses of that delegate-declaration.
- The scope of a member declared by a class-member-declaration (§10.1.6) is the class-body in which the declaration occurs. In addition, the scope of a class member extends to the class-body of those derived classes that are included in the accessibility domain (§3.5.2) of the member.
- The scope of a member declared by a struct-member-declaration (§11.2) is the struct-body in which the declaration occurs.
- The scope of a member declared by an enum-member-declaration (§14.3) is the enum-body in which the declaration occurs.
- The scope of a parameter declared in a method-declaration (§10.6) is the method-body of that method-declaration.
- The scope of a parameter declared in an indexer-declaration (§10.9) is the accessor-declarations of that indexer-declaration.
- The scope of a parameter declared in an operator-declaration (§10.10) is the block of that operator-declaration.
- The scope of a parameter declared in a constructor-declaration (§10.11) is the constructor-initializer and block of that constructor-declaration.
- The scope of a parameter declared in a lambda-expression (§) is the lambda-expression-body of that lambda-expression.
- The scope of a parameter declared in an anonymous-method-expression (§) is the block of that anonymous-method-expression.
- The scope of a label declared in a labeled-statement (§8.4) is the block in which the declaration occurs.
- The scope of a local variable declared in a local-variable-declaration (§8.5.1) is the block in which the declaration occurs.
- The scope of a local variable declared in a switch-block of a switch statement (§8.7.2) is the switch-block.
- The scope of a local variable declared in a *for-initializer* of a *for* statement (§8.8.3) is the *for-initializer*, the *for-condition*, the *for-iterator*, and the contained statement of the *for* statement.
- The scope of a local constant declared in a *local-constant-declaration* (§8.5.2) is the block in which the declaration occurs. It is a compile-time error to refer to a local constant in a textual position that precedes its *constant-declarator*.
- The scope of a variable declared as part of a *foreach-statement*, *using-statement*, *lock-statement* or *query-expression* is determined by the expansion of the given construct.

Within the scope of a namespace, class, struct, or enumeration member it is possible to refer to the member in a textual position that precedes the declaration of the member. For example

```
class A
{
    void F() {
        i = 1;
    }

    int i = 0;
}
```

Here, it is valid for F to refer to i before it is declared.

Within the scope of a local variable, it is a compile-time error to refer to the local variable in a textual position that precedes the *local-variable-declarator* of the local variable. For example

```
class A
{
    int i = 0;
    void F() {
        i = 1;             // Error, use precedes declaration
        int i;
        i = 2;
    }

    void G() {
        int j = (j = 1);   // Valid
    }

    void H() {
        int a = 1, b = ++a; // Valid
    }
}
```

In the F method above, the first assignment to i specifically does not refer to the field declared in the outer scope. Rather, it refers to the local variable and it results in a compile-time error because it textually precedes the declaration of the variable. In the G method, the use of j in the initializer for the declaration of j is valid because the use does not precede the *local-variable-declarator*. In the H method, a subsequent *local-variable-declarator* correctly refers to a local variable declared in an earlier *local-variable-declarator* within the same *local-variable-declaration*.

The scoping rules for local variables are designed to guarantee that the meaning of a name used in an expression context is always the same within a block. If the scope of a local variable were to extend only from its declaration to the end of the block, then in the example above, the first assignment would assign to the instance variable and the second assignment would assign to the local variable, possibly leading to compile-time errors if the statements of the block were later to be rearranged.

The meaning of a name within a block may differ based on the context in which the name is used. In the example

```csharp
using System;

class A {}
class Test
{
    static void Main() {
        string A = "hello, world";
        string s = A;                       // expression context
        Type t = typeof(A);                 // type context
        Console.WriteLine(s);               // writes "hello, world"
        Console.WriteLine(t);               // writes "A"
    }
}
```

the name A is used in an expression context to refer to the local variable A and in a type context to refer to the class A.

## 3.7.1 Name hiding

The scope of an entity typically encompasses more program text than the declaration space of the entity. In particular, the scope of an entity may include declarations that introduce new declaration spaces containing entities of the same name. Such declarations cause the original entity to become hidden. Conversely, an entity is said to be visible when it is not hidden.

Name hiding occurs when scopes overlap through nesting and when scopes overlap through inheritance. The characteristics of the two types of hiding are described in the following sections.

### 3.7.1.1 Hiding through nesting

Name hiding through nesting can occur as a result of nesting namespaces or types within namespaces, as a result of nesting types within classes or structs, and as a result of parameter and local variable declarations.

In the example

```csharp
class A
{
    int i = 0;
    void F() {
        int i = 1;
    }
    void G() {
        i = 1;
    }
}
```

within the F method, the instance variable i is hidden by the local variable i, but within the G method, i still refers to the instance variable.

When a name in an inner scope hides a name in an outer scope, it hides all overloaded occurrences of that name.

In the example

```csharp
class Outer
{
    static void F(int i) {}
    static void F(string s) {}
    class Inner
    {
        void G() {
            F(1);          // Invokes Outer.Inner.F
            F("Hello");    // Error
        }
    }
}
```
