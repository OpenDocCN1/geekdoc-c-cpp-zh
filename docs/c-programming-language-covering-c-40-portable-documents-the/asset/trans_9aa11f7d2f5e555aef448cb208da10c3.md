
- 同时包含 get 访问器和 set 访问器的属性称为读写属性。
- 只有 get 访问器的属性称为只读属性。只读属性作为赋值目标会导致编译时错误。
- 只有 set 访问器的属性称为只写属性。除作为赋值目标外，在表达式中引用只写属性会导致编译时错误。

在下面的示例中

```
public class Button: Control
{
    private string caption;
    public string Caption {
        get {
            return caption;
        }
        set {
            if (caption != value) {
                caption = value;
                Repaint();
            }
        }
    }
    public override void Paint(Graphics g, Rectangle r) {
        // Painting code goes here
    }
}
```

Button 控件声明了一个公共的 Caption 属性。Caption 属性的 get 访问器返回存储在私有 caption 字段中的字符串。set 访问器检查新值是否与当前值不同；如果不同，则存储新值并重绘控件。属性通常遵循上面所示的模式：get 访问器只返回存储在私有字段中的值，而 set 访问器修改该私有字段，然后执行完全更新对象状态所需的任何附加操作。

给定上面的 Button 类，下面是 Caption 属性用法的一个示例：

```
Button okButton = new Button();
okButton.Caption = "OK";    // Invokes set accessor
string s = okButton.Caption;    // Invokes get accessor
```

在这里，通过向属性赋值来调用 set 访问器，通过在表达式中引用属性来调用 get 访问器。

属性的 get 和 set 访问器不是不同的成员，并且不能分别声明属性的访问器。因此，读写属性的两个访问器不可能具有不同的可访问性。下面的示例

```csharp
class A
{
    private string name;
    public string Name {          // Error: duplicate member name
        get { return name; }
    }
    public string Name {          // Error: duplicate member name
        set { name = value; }
    }
}
```

并未声明一个读写属性。相反，它声明了两个同名属性，一个只读，一个只写。由于同一个类中声明的两个成员不能同名，因此该示例会导致编译时错误。

当派生类声明一个与继承属性同名的属性时，该派生属性在读取和写入两方面都会隐藏继承属性。在下面的示例中

```csharp
class A
{
    public int P {
        set {...}
    }
}
class B: A
{
    new public int P {
        get {...}
    }
}
```

B 中的 P 属性在读取和写入两方面隐藏了 A 中的 P 属性。因此，在下面的语句中

```csharp
B b = new B();
b.P = 1;          // Error: B.P is read-only
((A)b).P = 1;     // Okay: reference to A.P
```

对 b.P 的赋值会导致报告编译时错误，因为 B 中的只读 P 属性隐藏了 A 中的只写 P 属性。但请注意，可以使用强制转换来访问被隐藏的 P 属性。

与公共字段不同，属性在对象的内部状态与其公共接口之间提供了一种分离。请考虑下面的示例：

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

在这里，Label 类使用两个 int 字段 x 和 y 来存储其位置。该位置通过 X 和 Y 属性以及 Point 类型的 Location 属性公开。如果在 Label 的未来版本中，在内部将位置存储为 Point 更方便，则可以在不影响该类公共接口的情况下进行此更改：

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

如果 x 和 y 改为公共 readonly 字段，就不可能对 Label 类做出这样的更改。

通过属性公开状态不一定比直接公开字段效率低。特别是，当属性是非虚属性且只包含少量代码时，执行环境可以用访问器的实际代码替换对访问器的调用。此过程称为内联，它使属性访问与字段访问一样高效，同时保留属性更高的灵活性。

由于调用 get 访问器在概念上等同于读取字段的值，因此 get 访问器具有可观察的副作用被认为是不良的编程风格。在下面的示例中

```
class Counter
{
    private int next;
    public int Next {
        get { return next++; }
    }
}
```

Next 属性的值取决于该属性先前被访问的次数。因此，访问该属性会产生可观察的副作用，该属性应改为作为方法实现。

get 访问器的“无副作用”约定并不意味着 get 访问器应始终编写为仅返回存储在字段中的值。实际上，get 访问器经常通过访问多个字段或调用方法来计算属性的值。但是，设计良好的 get 访问器不会执行任何会导致对象状态发生可观察变化的操作。

属性可用于将资源的初始化延迟到首次引用该资源的时刻。例如：

```
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
```

Console 类包含三个属性——In、Out 和 Error——分别表示标准输入、输出和错误设备。通过将这些成员公开为属性，Console 类可以将它们的初始化延迟到实际使用时。例如，在首次引用 Out 属性时，如下所示

`Console.Out.WriteLine("hello, world");`

就会为输出设备创建基础 TextWriter。但如果应用程序未引用 In 和 Error 属性，则不会为这些设备创建任何对象。

## 10.7.3 自动实现的属性

> JON SKEET C# 3.0 规范的一份早期草案将这些属性称为“自动属性”。这个名称存在的时间刚好长到足以流传下来，如今在社区中的使用范围已比全名广泛得多。

当属性被指定为自动实现的属性时，会自动为该属性提供一个隐藏的后备字段，并且访问器实现为从该后备字段读取并写入该后备字段。

