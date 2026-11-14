

```
public class Circle : Shape
{
    private PointF center;
    private float radius;

    public Circle() :
        this(PointF.Empty, 0)
    {
    }

    public Circle(PointF c, float r)
    {
        center = c;
        radius = r;
    }

    public override void Draw()
    {
        //...
    }

    static public implicit operator Ellipse(Circle c)
    {
        return new Ellipse(c.center, c.center,
            c.radius, c.radius);
    }
}
```

有了隐式转换运算符后，你可以在任何需要 Ellipse 的地方使用 Circle。此外，转换会自动发生：

```
public static double ComputeArea(Ellipse e)
{
    // return the area of the ellipse.
    return e.R1 * e.R2 * Math.PI;
}
```

```
// call it:
Circle c1 = new Circle(new PointF(3.0f, 0), 5.0f);
ComputeArea(c1);
```

这个示例说明了我所说的可替换性：一个圆被替换为椭圆。即使进行了替换，ComputeArea 函数也能正常工作。你运气不错。但请看这个函数：

```
```
```csharp
public static void Flatten(Ellipse e)
{
    e.R1 /= 2;
    e.R2 *= 2;
}
```
```
```

// 使用圆调用：

```
```
```csharp
Circle c = new Circle(new PointF(3.0f, 0), 5.0f);
Flatten(c);
```
```
```

这行不通。Flatten() 方法将椭圆作为参数。编译器必须以某种方式将圆转换为椭圆。你创建了一个正好做到这一点的隐式转换。你的转换会被调用，Flatten() 函数将其参数设置为由你的隐式转换创建的椭圆。这个临时对象会被 Flatten() 函数修改，并立即变成垃圾。你期望的 Flatten() 函数的副作用会发生，但只发生在临时对象上。最终结果是圆 c 没有任何变化。

将转换从隐式改为显式，只会强制用户在调用时添加强制转换：

```
```
```csharp
Circle c = new Circle(new PointF(3.0f, 0), 5.0f);
Flatten((Ellipse)c);
```
```
```

原始问题依然存在。你只是强迫用户添加强制转换来引发问题。你仍然创建一个临时对象，将其展平，然后丢弃。圆 c 根本没有被修改。相反，如果你创建一个构造函数来将 Circle 转换为 Ellipse，操作会更清晰：

```
```
```csharp
Circle c = new Circle(new PointF(3.0f, 0), 5.0f);
Flatten(new Ellipse(c));
```
```
```

大多数程序员看到前两行代码会立即意识到，传递给 Flatten() 的椭圆的任何修改都会丢失。他们会通过跟踪新对象来修复这个问题：

```
```
```csharp
Circle c = new Circle(new PointF(3.0f, 0), 5.0f);
Flatten(c);
```
```
```

// 使用圆。
// ...
// 转换为椭圆。
Ellipse e = new Ellipse(c);
Flatten(e);

变量 e 保存了展平后的椭圆。通过用构造函数替换转换运算符，你并没有丢失任何功能；你只是让创建新对象的时机更加清晰。（资深 C++ 程序员应注意，C# 不会为隐式或显式转换调用构造函数。只有在显式使用 new 运算符时才会创建新对象，其他任何时候都不会。C# 中构造函数不需要 explicit 关键字。）

返回对象内部字段的转换运算符不会出现这种行为。它们有其他问题。你在类的封装上开了一个严重的漏洞。通过将你的类型转换为其他对象，你的类的客户端可以访问内部变量。出于 Item 26 中讨论的所有原因，最好避免这样做。

转换运算符引入了一种会在你的代码中引起问题的可替换性。你在暗示，在所有情况下，用户都可以合理地期望另一个类可以替代你创建的类。当访问这个替代对象时，你会导致客户端使用临时对象或内部字段，而不是你创建的类。然后你修改临时对象并丢弃结果。这些微妙的 bug 难以发现，因为编译器会生成代码来转换这些对象。在你的 API 中避免使用转换运算符。

## Item 10: 使用可选参数来最小化方法重载

C# 现在支持调用位置的命名参数。这意味着形式参数的名称现在是你类型公共接口的一部分。更改公共参数的名称可能会破坏调用代码。这意味着你在许多情况下应避免使用命名参数，并且还应避免更改公共或受保护方法上的形式参数名称。

当然，没有语言设计师会添加功能只是为了让你的生活变得困难。命名参数是出于某种原因而添加的，并且有积极的用途。命名参数与可选参数配合使用，可以限制许多 API 周围的冗余，尤其是 Microsoft Office 的 COM API。这段小代码使用经典 COM 方法创建 Word 文档并插入少量文本：

```
var wasted = Type.Missing;
var wordApp = new
    Microsoft.Office.Interop.Word.Application();
wordApp.Visible = true;
Documents docs = wordApp.Documents;

Document doc = docs.Add(ref wasted,
    ref wasted, ref wasted, ref wasted);

Range range = doc.Range(0, 0);

range.InsertAfter("Testing, testing, testing. . .");
```

这段小代码（可以说是无用的）使用了四次 Type.Missing 对象。任何 Office Interop 应用程序都会在应用程序中使用大量的 Type.Missing 对象。这些实例会使你的应用程序变得混乱，并隐藏你正在构建的软件的实际逻辑。

这种额外的噪音是向 C# 语言添加可选参数和命名参数的主要驱动力。可选参数意味着这些 Office API 可以为所有原本会使用 Type.Missing 的位置创建默认值。这甚至简化了这段小代码：

```
var wordApp = new
    Microsoft.Office.Interop.Word.Application();
wordApp.Visible = true;
Documents docs = wordApp.Documents;

Document doc = docs.Add();

Range range = doc.Range(0, 0);

range.InsertAfter("Testing, testing, testing. . .");
```

即使是这个小改动也提高了这段代码的可读性。当然，你可能并不总是想使用所有默认值。然而，你仍然不想在中间添加所有 Type.Missing 参数。假设你想创建一个新网页而不是新 Word 文档。这是 Add() 方法中四个参数的最后一个。使用命名参数，你可以只指定最后一个参数：

```
var wordApp = new
    Microsoft.Office.Interop.Word.Application();
wordApp.Visible = true;
Documents docs = wordApp.Documents;
object docType = WdNewDocumentType.wdNewWebPage;
Document doc = docs.Add(DocumentType: ref docType);
Range range = doc.Range(0, 0);
range.InsertAfter("Testing, testing, testing . . . ");
```

命名参数意味着，在任何带有默认参数的 API 中，你只需要指定你打算使用的参数。这比多个重载更简单。事实上，有四个不同的参数时，你需要为 Add() 方法创建 15 个不同的重载，才能达到命名参数和可选参数提供的同样灵活性。请记住，某些 Office API 最多有 16 个参数，可选参数和命名参数非常有帮助。

我在参数列表中保留了 ref 修饰符，但 C# 4.0 的另一个变化使其在 COM 场景中成为可选。这是因为 COM 通常按引用传递对象，因此几乎所有参数都是按引用传递的，即使被调用的方法没有修改它们。事实上，Range() 调用按引用传递值 (0,0)。我在那里没有包含 ref 修饰符，因为那会明显具有误导性。事实上，在大多数生产代码中，我也不会在 Add() 调用中包含 ref 修饰符。我上面这样做是为了让你能看到实际的 API 签名。

当然，仅仅因为命名参数和可选参数的理由是 COM 和 Office API，并不意味着你应该将它们的使用限制在 Office 互操作应用程序中。事实上，你不能。调用你 API 的开发人员可以使用命名参数来装饰调用位置，无论你是否希望他们这样做。

这个方法：

```
private void SetName(string lastName, string firstName)
{
```

