Notice that assembly-qualified references to types are everyday business in IL code because the runtime requires this form to locate referenced types. Figure 24.14 shows the compiled IL code corresponding to the preceding fragment. All the extern alias feature in C# provides for is syntax to carry out this disambiguation across assemblies containing a type with the same name.

![](bbox=[0.2, 0.26, 0.65, 0.55])

FIGURE 24.14 In IL code, types are always prefixed with the assembly in which they're defined.

Use of :: is officially known as namespace alias qualification and can also be used to write super-robust code in the face of potential future changes to code. For example, it's possible to have imported a namespace with an alias that starts to clash with a type name somewhere in the future:

```
// File1.cs
namespace Bar
{
    using Foo = System.Drawing;

    class Program
    {
        private Foo.Point point; // Refers to System.Drawing.Point
    }
}
```

If we now introduce a Bar.Foo type somewhere else, the preceding code will break:

```
// File2.cs
namespace Bar
{
    class Foo
    {
        ...
    }
}
```