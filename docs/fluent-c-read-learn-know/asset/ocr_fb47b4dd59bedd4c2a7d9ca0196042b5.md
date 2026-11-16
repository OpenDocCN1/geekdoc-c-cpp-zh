# # INTERFACES & CLASSES

The syntax for defining an interface is almost identical to that for defining classes, but with two differences

+   • An interface can contain only member definitions, not implementation. Essentially, an interface defines something a class (or other interface) can do, but leaves the doing of it up to the class itself.

+   • Interfaces cannot define fields, constructors, destructors or other types.

```
interface <Name> <: base, interface, ...>
```

By convention, interface names begin with I and are usually adjectives that describe behavior (IPrintable).

```
interface IMyDoable
{
    Int32 MyProperty { get; set; }

    public void ShowHello();
}
```

This statement specifies that the property must have both get and set accessors. Don't confuse it with an auto-implemented property, even though the syntax is the same.

```
public class MyClass : IMyDoable
{
    Int32 m_myProperty;

    Int32 MyProperty
    {
        get {return m_myProperty;}
        set {m_myProperty = value;}
    }

    public void ShowHello ()
    {
        MessageBox.Show("Hello!");
    }
}
```

**ON YOUR OWN**

You may not realize it, but you already know how to create an interface in the Class Designer. Give it a try: Create the IPrintable interface and define its two methods.