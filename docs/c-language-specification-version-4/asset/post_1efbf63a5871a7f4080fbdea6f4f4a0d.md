
the assignment to b.P causes a compile-time error to be reported, since the read-only P property in B hides the write-only P property in A. Note, however, that a cast can be used to access the hidden P property.

Unlike public fields, properties provide a separation between an object's internal state and its public interface. Consider the example:

```
class Label
{
    private int x, y;
    private string caption;
    public Label(int x, int y, string caption) {
        this.x = x;
        this.y = y;
        this.caption = caption;
    }
    public int X {
        get { return x; }
    }
    public int Y {
        get { return y; }
    }
    public Point Location {
        get { return new Point(x, y); }
    }
    public string Caption {
        get { return caption; }
    }
}
```

Here, the Label class uses two int fields, x and y, to store its location. The location is publicly exposed both as an X and a Y property and as a Location property of type Point. If, in a future version of Label, it becomes more convenient to store the location as a Point internally, the change can be made without affecting the public interface of the class:

```
class Label
{
    private Point location;
    private string caption;
    public Label(int x, int y, string caption) {
        this.location = new Point(x, y);
        this.caption = caption;
    }
    public int X {
        get { return location.x; }
    }
    public int Y {
        get { return location.y; }
    }
    public Point Location {
        get { return location; }
    }
    public string Caption {
        get { return caption; }
    }
}
```

Had x and y instead been public readonly fields, it would have been impossible to make such a change to the Label class.

Exposing state through properties is not necessarily any less efficient than exposing fields directly. In particular, when a property is non-virtual and contains only a small amount of code, the execution environment may replace calls to accessors with the actual code of the accessors. This process is known as inlining, and it makes property access as efficient as field access, yet preserves the increased flexibility of properties.

Since invoking a get accessor is conceptually equivalent to reading the value of a field, it is considered bad programming style for get accessors to have observable side-effects. In the example

```
~~~csharp
class Counter
{
    private int next;
    public int Next {
        get { return next++; }
    }
}
~~~
```

The value of the Next property depends on the number of times the property has previously been accessed. Thus, accessing the property produces an observable side-effect, and the property should be implemented as a method instead.

The “no side-effects” convention for get accessors doesn’t mean that get accessors should always be written to simply return values stored in fields. Indeed, get accessors often compute the value of a property by accessing multiple fields or invoking methods. However, a properly designed get accessor performs no actions that cause observable changes in the state of the object.

Properties can be used to delay initialization of a resource until the moment it is first referenced. For example:

```
~~~csharp
using System.IO;
public class Console
{
    private static TextReader reader;
    private static TextWriter writer;
    private static TextWriter error;

    public static TextReader In {
        get {
            if (reader == null) {
                reader = new StreamReader(Console.OpenStandardInput());
            }
            return reader;
        }
    }

    public static TextWriter Out {
        get {
            if (writer == null) {
                writer = new StreamWriter(Console.OpenStandardOutput());
            }
            return writer;
        }
    }

    public static TextWriter Error {
        get {
            if (error == null) {
                error = new StreamWriter(Console.OpenStandardError());
            }
            return error;
        }
    }
}
~~~
```

The Console class contains three properties, In, Out, and Error, that represent the standard input, output, and error devices, respectively. By exposing these members as properties, the Console class can delay their initialization until they are actually used. For example, upon first referencing the Out property, as in

```
Console.Out.WriteLine("hello, world");
```

the underlying TextWriter for the output device is created. But if the application makes no reference to the In and Error properties, then no objects are created for those devices.

## 10.7.3 Automatically implemented properties

When a property is specified as an automatically implemented property, a hidden backing field is automatically available for the property, and the accessors are implemented to read from and write to that backing field.

The following example:

```
public class Point {
    public int X { get; set; } // automatically implemented
    public int Y { get; set; } // automatically implemented
}
```

is equivalent to the following declaration:

```
public class Point {
    private int x;
    private int y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

Because the backing field is inaccessible, it can be read and written only through the property accessors, even within the containing type. This means that automatically implemented read-only or write-only properties do not make sense, and are disallowed. It is however possible to set the access level of each accessor differently. Thus, the effect of a read-only property with a private backing field can be mimicked like this:

```
public class ReadOnlyPoint {
    public int X { get; private set; }
    public int Y { get; private set; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```

This restriction also means that definite assignment of struct types with auto-implemented properties can only be achieved using the standard constructor of the struct, since assigning to the property itself requires the struct to be definitely assigned. This means that user-defined constructors must call the default constructor.

## 10.7.4 Accessibility

If an accessor has an accessor-modifier, the accessibility domain (§3.5.2) of the accessor is determined using the declared accessibility of the accessor-modifier. If an accessor does not have an accessor-modifier, the accessibility domain of the accessor is determined from the declared accessibility of the property or indexer.

The presence of an accessor-modifier never affects member lookup (§7.3) or overload resolution (§7.5.3). The modifiers on the property or indexer always determine which property or indexer is bound to, regardless of the context of the access.

Once a particular property or indexer has been selected, the accessibility domains of the specific accessors involved are used to determine if that usage is valid:
- If the usage is as a value (§7.1.1), the get accessor must exist and be accessible.
- If the usage is as the target of a simple assignment (§7.17.1), the set accessor must exist and be accessible.
- If the usage is as the target of compound assignment (§7.17.2), or as the target of the ++ or -- operators (§7.5.9, §7.6.5), both the get accessors and the set accessor must exist and be accessible.

In the following example, the property A.Text is hidden by the property B.Text, even in contexts where only the set accessor is called. In contrast, the property B.Count is not accessible to class M, so the accessible property A.Count is used instead.

```csharp
class A
{
    public string Text {
        get { return "hello"; }
        set { }
    }
    public int Count {
        get { return 5; }
        set { }
    }
}
class B : A
{
    private string text = "goodbye";
    private int count = 0;

    new public string Text {
        get { return text; }
        protected set { text = value; }
    }

    new protected int Count {
        get { return count; }
        set { count = value; }
    }
}
class M
{
    static void Main() {
        B b = new B();
        b.Count = 12;        // Calls A.Count set accessor
        int i = b.Count;     // Calls A.Count get accessor
        b.Text = "howdy";    // Error, B.Text set accessor not accessible
        string s = b.Text;   // Calls B.Text get accessor
    }
}
```

An accessor that is used to implement an interface may not have an accessor-modifier. If only one accessor is used to implement an interface, the other accessor may be declared with an accessor-modifier:

```csharp
public interface I
{
    string Prop { get; }
}
public class C : I
{
    public string Prop {
        get { return "April"; }    // Must not have a modifier here
        internal set {...}         // Ok, because I.Prop has no set accessor
    }
}
```
