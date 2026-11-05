```
} protected virtual void PaintControl() {...}
class TextBox: Control
{
    protected override void PaintControl() {...}
}
```

Here, classes derived from Control can specialize the implementation of IControl.Paint by overriding the PaintControl method. end example

# 18.6.7 Interface re-implementation

A class that inherits an interface implementation is permitted to re-implement the interface by including it in the base class list.

A re-implementation of an interface follows exactly the same interface mapping rules as an initial implementation of an interface. Thus, the inherited interface mapping has no effect whatsoever on the interface mapping established for the re-implementation of the interface. [Example: In the declarations

```
interface IControl
{
    void Paint();
}
class Control: IControl
{
    void IControl.Paint() {...}
}
class MyControl: Control, IControl
{
    public void Paint() {}
}
```

the fact that Control maps IControl.Paint onto Control.IControl.Paint doesn't affect the re-implementation in MyControl, which maps IControl.Paint onto MyControl.Paint. end example]

Inherited public member declarations and inherited explicit interface member declarations participate in the interface mapping process for re-implemented interfaces. [Example:

```
interface IMethods
{
    void F();
    void G();
    void H();
    void I();
}
class Base: IMethods
{
    void IMethods.F() {}
    void IMethods.G() {}
    public void H() {}
    public void I() {}
}
class Derived: Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

Here, the implementation of IMethods in Derived maps the interface methods onto Derived.F, Base.IMethods.G, Derived.IMethods.H, and Base.I. end example]

When a class implements an interface, it implicitly also implements all that interface's base interfaces. Likewise, a re-implementation of an interface is also implicitly a re-implementation of all of the interface's base interfaces. [Example: