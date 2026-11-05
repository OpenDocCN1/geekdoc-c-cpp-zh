> > **PETER SESTOFT** The two bulleted points stating “if the field is readonly . . . then the result is a value” have a slightly surprising effect when the field has struct type, and that struct has a mutable field (not a recommended combination—see other annotations on this point). Consider the following example:

```
struct S {
    public int x;
    public void SetX() { x = 2; }
}
class C {
    public static void M() { s.SetX(); }
}
```

> > As expected, after the call `s.SetX()` the struct’s field `s.x` will have the value 2. Now if we add a readonly modifier to the declaration of the field `s`, then suddenly the call `s.SetX()` has no effect! That is, `s` in the method call is now a value, not a variable, per the rules given earlier; therefore `SetX()` is executed on a copy of field `s`, not on field `s` itself. Somewhat strangely, if instead `s` were a local variable of struct type declared in a using statement (§8.13), which also has the effect of making `s` immutable, then `s.SetX()` updates `s.x` as expected.

# 7.6.4.1 *Identical Simple Names and Type Names*

In a member access of the form E.I, if I is a single identifier, and if the meaning of E is a *simple-name* (§7.6.2) is a constant, field, property, local variable, or parameter with the same type as the meaning of E as a *type-name* (§3.8), then both possible meanings of E are permitted. The two possible meanings of E.I are never ambiguous, since I must necessarily be a member of the type E in both cases. In other words, the rule simply permits access to the static members and nested types of E where a compile-time error would otherwise have occurred. For example:

```
struct Color
{
    public static readonly Color White = new Color(...);
    public static readonly Color Black = new Color(...);

    public Color Complement() {...}
}

class A
{
    public Color Color;        // Field Color of type Color

    void F() {
        Color = Color.Black;   // References Color.Black static member
    }
}
```