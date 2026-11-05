
referenced as the target of an assignment (§12.21), or as the operand of ++ or -- (§12.8.15, §12.9.6), the set accessor is invoked with an argument that provides the new value (§12.21.2). The body of a set accessor shall conform to the rules for void methods described in §15.6.11. In particular, return statements in the set accessor body are not permitted to specify an expression. Since a set accessor implicitly has a parameter named value, it is a compile-time error for a local variable or constant declaration in a set accessor to have that name.

Based on the presence or absence of the get and set accessors, a property is classified as follows:

- A property that includes both a get accessor and a set accessor is said to be a *read-write property*.
- A property that has only a get accessor is said to be a *read-only property*. It is a compile-time error for a read-only property to be the target of an assignment.
- A property that has only a set accessor is said to be a *write-only property*. Except as the target of an assignment, it is a compile-time error to reference a write-only property in an expression.

*Note:* The pre- and postfix ++ and -- operators and compound assignment operators cannot be applied to write-only properties, since these operators read the old value of their operand before they write the new one. *end note*

*Example:* In the following code

```
public class Button : Control
{
    private string caption;

    public string Caption
    {
        get => caption;
        set
        {
            if (caption != value)
            {
                caption = value;
                Repaint();
            }
        }
    }

    public override void Paint(Graphics g, Rectangle r)
    {
        // Painting code goes here
    }
}
```

the Button control declares a public Caption property. The get accessor of the Caption property returns the string stored in the private caption field. The set accessor checks if the new value is different from the current value, and if so, it stores the new value and repaints the control. Properties often follow the pattern shown above: The get accessor simply returns a value stored in a private field, and the set accessor modifies that private field and then performs any additional actions required to update fully the state of the object. Given the Button class above, the following is an example of use of the Caption property:

```
Button okButton = new Button();
okButton.Caption = "OK"; // Invokes set accessor
string s = okButton.Caption; // Invokes get accessor
```

Here, the set accessor is invoked by assigning a value to the property, and the get accessor is invoked by referencing the property in an expression.

end example

The get and set accessors of a property are not distinct members, and it is not possible to declare the accessors of a property separately.

Example: The example

```csharp
class A
{
    private string name;

    // Error, duplicate member name
    public string Name
    {
        get => name;
    }

    // Error, duplicate member name
    public string Name
    {
        set => name = value;
    }
}
```

does not declare a single read-write property. Rather, it declares two properties with the same name, one read-only and one write-only. Since two members declared in the same class cannot have the same name, the example causes a compile-time error to occur.

end example

When a derived class declares a property by the same name as an inherited property, the derived property hides the inherited property with respect to both reading and writing.

Example: In the following code

```csharp
class A
{
    public int P
    {
        set {...}
    }
}

class B : A
{
    public new int P
    {
        get {...}
    }
}
```

the P property in B hides the P property in A with respect to both reading and writing. Thus, in the statements

```csharp
B b = new B();
b.P = 1;    // Error, B.P is read-only
((A)b).P = 1;  // Ok, reference to A.P
```

the assignment to b.P causes a compile-time error, since the read-only P property in B hides the write-only P property in A. Note, however, that a cast can be used to access the hidden P property.

*end example*

Unlike public fields, properties provide a separation between an object's internal state and its public interface.

*Example:* Consider the following code, which uses a Point struct to represent a location:

```csharp
class Label
{
    private int x, y;
    private string caption;

    public Label(int x, int y, string caption)
    {
        this.x = x;
        this.y = y;
        this.caption = caption;
    }

    public int X => x;
    public int Y => y;
    public Point Location => new Point(x, y);
    public string Caption => caption;
}
```

Here, the Label class uses two int fields, x and y, to store its location. The location is publicly exposed both as an X and a Y property and as a Location property of type Point. If, in a future version of Label, it becomes more convenient to store the location as a Point internally, the change can be made without affecting the public interface of the class:

```csharp
class Label
{
    private Point location;
    private string caption;

    public Label(int x, int y, string caption)
    {
        this.location = new Point(x, y);
        this.caption = caption;
    }

    public int X => location.X;
    public int Y => location.Y;
    public Point Location => location;
    public string Caption => caption;
}
```

Had x and y instead been public readonly fields, it would have been impossible to make such a change to the Label class.

*end example*

*Note: Exposing state through properties is not necessarily any less efficient than exposing fields directly. In particular, when a property is non-virtual and contains only a small amount of code, the execution environment might replace calls to accessors with the actual code of the accessors. This process is known as **inlining**, and it makes property access as efficient as field access, yet preserves the increased flexibility of properties. end note*

*Example:* Since invoking a get accessor is conceptually equivalent to reading the value of a field, it is considered bad programming style for get accessors to have observable side-effects. In the example

~~~csharp
class Counter
{
    private int next;

    public int Next => next++;
}
~~~

the value of the Next property depends on the number of times the property has previously been accessed. Thus, accessing the property produces an observable side effect, and the property should be implemented as a method instead.

The “no side-effects” convention for get accessors doesn’t mean that get accessors should always be written simply to return values stored in fields. Indeed, get accessors often compute the value of a property by accessing multiple fields or invoking methods. However, a properly designed get accessor performs no actions that cause observable changes in the state of the object.

*end example*

Properties can be used to delay initialization of a resource until the moment it is first referenced.

*Example:*

~~~csharp
public class Console
{
    private static TextReader reader;
    private static TextWriter writer;
    private static TextWriter error;

    public static TextReader In
    {
        get
        {
            if (reader == null)
            {
                reader = new StreamReader(Console.OpenStandardInput());
            }
            return reader;
        }
    }

    public static TextWriter Out
    {
        get
        {
            if (writer == null)
            {
                writer = new StreamWriter(Console.OpenStandardOutput());
            }
            return writer;
        }
    }
    public static TextWriter Error
    {
        get
        {
            if (error == null)
            {
                error = new StreamWriter(Console.OpenStandardError());
            }
            return error;
        }
    }
...
}
~~~

The Console class contains three properties, In, Out, and Error, that represent the standard input, output, and error devices, respectively. By exposing these members as properties, the Console class can delay their initialization until they are actually used. For example, upon first referencing the Out property, as in Console.Out.WriteLine("hello, world"); the underlying TextWriter for the output device is created. However, if the application makes no reference to the In and Error properties, then no objects are created for those devices.

end example

## 15.7.4 Automatically implemented properties

An automatically implemented property (or auto-property for short), is a non-abstract, non-extern, non-ref-valued property with semicolon-only accessor bodies. Auto-properties shall have a get accessor and may optionally have a set accessor.

When a property is specified as an automatically implemented property, a hidden backing field is automatically available for the property, and the accessors are implemented to read from and write to that backing field. The hidden backing field is inaccessible, it can be read and written only through the automatically implemented property accessors, even within the containing type. If the auto-property has no set accessor, the backing field is considered readonly (§15.5.3). Just like a readonly field, a read-only auto-property may also be assigned to in the body of a constructor of the enclosing class. Such an assignment assigns directly to the read-only backing field of the property.

An auto-property may optionally have a property_initializer, which is applied directly to the backing field as a variable_initializer (§17.7).

Example:

```
public class Point
{
    public int X { get; set; } // Automatically implemented
    public int Y { get; set; } // Automatically implemented
}
```
