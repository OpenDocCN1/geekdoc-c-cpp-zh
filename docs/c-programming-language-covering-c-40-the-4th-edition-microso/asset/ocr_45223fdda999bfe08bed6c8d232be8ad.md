```
    interface IComparable
    {
        int CompareTo(object other);
    }

    class ListEntry : ICloneable, IComparable
    {
        public object Clone() {...}

        public int CompareTo(object other) {...}
    }
```

> > **JON SKEET** It bugs me that the interface implementation is usually so totally
> > implicit. There's no indication that the CompareTo and Clone methods have anything
> > to do with the interfaces for which they're providing implementations. When overriding
> > virtual methods inherited from a base class, the override modifier makes this
> > behavior obvious: Anyone refactoring a class and wanting to rename a method is
> > informed that it's linked to a method elsewhere. No such indication is given for
> > interfaces.
> >
> > Unfortunately, the design of interface implementation wouldn't quite be consistent
> > with adding a modifier to the declaration. The code declaring a method doesn't necessarily
> > even know that it may be used to implement an interface:
> >
> >     interface IFoo { void Foo(); }
> >     class Base
> >     {
> >         public void Foo();
> >     }
> >     // IFoo.Foo is implemented by Base.Foo
> >     class Derived : Base, IFoo { }
> >
> > This is probably the most pragmatic approach to interfaces, but from a purity (or control
> > freak) standpoint, it feels slightly wrong.

A class or struct that directly implements an interface also directly implements all of the interface's base interfaces implicitly. This is true even if the class or struct doesn't explicitly list all base interfaces in the base class list. For example:

```
    interface IControl
    {
        void Paint();
    }

    interface ITextBox : IControl
    {
        void SetText(string text);
    }
```