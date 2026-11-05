to the static members and nested types of E where a compile-time error would otherwise have occurred. For example:

```
struct Color
{
    public static readonly Color White = new Color(...);
    public static readonly Color Black = new Color(...);
    public Color Complement() {...}
}
class A
{
    public Color Color;            // Field Color of type Color
    void F() {
        Color = Color.Black;       // References Color.Black static member
        Color = Color.Complement(); // Invokes Complement() on Color field
    }
    static void G() {
        Color c = Color.White;     // References Color.white static member
    }
}
```

Within the A class, those occurrences of the Color identifier that reference the Color type are underlined, and those that reference the Color field are not underlined.

# 7.6.4.2 Grammar ambiguities

The productions for simple-name (§7.6.2) and member-access (§7.6.4) can give rise to ambiguities in the grammar for expressions. For example, the statement:

```
F(G<A,B>(7));
```

could be interpreted as a call to F with two arguments, G < A and B > (7). Alternatively, it could be interpreted as a call to F with one argument, which is a call to a generic method G with two type arguments and one regular argument.

If a sequence of tokens can be parsed (in context) as a simple-name (§7.6.2), member-access (§7.6.4), or pointer-member-access (§18.5.2) ending with a type-argument-list (§4.4.1), the token immediately following the closing > token is examined. If it is one of

```
( ) ] : ; , . ? == != | ^
```

then the type-argument-list is retained as part of the simple-name, member-access or pointer-member-access and any other possible parse of the sequence of tokens is discarded. Otherwise, the type-argument-list is not considered to be part of the simple-name, member-access or pointer-member-access, even if there is no other possible parse of the sequence of tokens. Note that these rules are not applied when parsing a type-argument-list in a namespace-or-type-name (§3.8). The statement

```
F(G<A,B>(7));
```

will, according to this rule, be interpreted as a call to F with one argument, which is a call to a generic method G with two type arguments and one regular argument. The statements

```
F(G < A, B > 7);
F(G < A, B >> 7);
```

will each be interpreted as a call to F with two arguments. The statement

```
x = F < A > +y;
```

will be interpreted as a less than operator, greater than operator, and unary plus operator, as if the statement had been written x = (F < A >) (+y), instead of as a simple-name with a type-argument-list followed by a binary plus operator. In the statement