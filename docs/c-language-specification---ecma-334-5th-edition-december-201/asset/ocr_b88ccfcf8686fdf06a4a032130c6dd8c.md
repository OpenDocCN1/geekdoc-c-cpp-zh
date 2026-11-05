rule simply permits access to the static members and nested types of E where a compile-time error would otherwise have occurred. [Example:

```
struct Color
{
    public static readonly Color white = new Color(...);
    public static readonly Color Black = new Color(...);
    public Color Complement() {...}
}
class A
{
    public Color Color;            // Field Color of type Color
    void F() {
        Color = Color.Black;       // Refs Color.Black static member
        Color = Color.Complement(); // Invokes Complement() on Color fld
    }
    static void G(){
        Color c = Color.White;     // Refs Color.White static member
    }
}
```

Within the A class, those occurrences of the Color identifier that reference the Color type are underlined, and those that reference the Color field are not underlined. end example]

# 12.7.6 Invocation expressions

# 12.7.6.1 General

An invocation-expression is used to invoke a method.

```
invocation-expression:
    primary-expression ( argument-list_opt )
```

An invocation-expression is dynamically bound (§12.3.3) if at least one of the following holds:

+   - The primary-expression has compile-time type dynamic.
+   - At least one argument of the optional argument-list has compile-time type dynamic.

In this case, the compiler classifies the invocation-expression as a value of type dynamic. The rules below to determine the meaning of the invocation-expression are then applied at run-time, using the run-time type instead of the compile-time type of those of the primary-expression and arguments that have the compile-time type dynamic. If the primary-expression does not have compile-time type dynamic, then the method invocation undergoes a limited compile-time check as described in §12.6.5.

The primary-expression of an invocation-expression shall be a method group or a value of a delegate-type. If the primary-expression is a method group, the invocation-expression is a method invocation (§12.7.6.2). If the primary-expression is a value of a delegate-type, the invocation-expression is a delegate invocation (§12.7.6.4). If the primary-expression is neither a method group nor a value of a delegate-type, a binding-time error occurs.

The optional argument-list (§12.6.2) provides values or variable references for the parameters of the method.

The result of evaluating an invocation-expression is classified as follows:

+   - If the invocation-expression invokes a method or delegate that returns void, the result is nothing. An expression that is classified as nothing is permitted only in the context of a statement-expression (§13.7) or as the body of a lambda-expression (§12.16). Otherwise a binding-time error occurs.
+   - Otherwise, the result is a value, with an associated type of the return type of the method or delegate. If the invocation is of an instance method, and the receiver is of a class type T, the associated type is