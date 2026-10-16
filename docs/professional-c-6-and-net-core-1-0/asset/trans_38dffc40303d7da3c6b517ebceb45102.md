
泛型类型可以实现泛型接口，也可以通过派生自一个类来实现。泛型类可以派生自泛型基类：

```
public class Base<T>
{
}
```

```
public class Derived<T>: Base<T>
{
}
```

要求是必须重复接口的泛型类型，或者必须指定基类的类型，如此处所示：

```
public class Base<T>
{
}
```

```
public class Derived<T>: Base<string>
{
}
```

这样，派生类可以是泛型类或非泛型类。例如，你可以定义一个抽象泛型基类，并在派生类中用具体类型实现它。这使你可以针对特定类型编写*泛型特化*：

```
public abstract class Calc<T>
{
    public abstract T Add(T x, T y);
    public abstract T Sub(T x, T y);
}
```

```
public class IntCalc: Calc<int>
{
    public override int Add(int x, int y) => x + y;
    public override int Sub(int x, int y) => x - y;
}
```

你还可以创建部分特化，例如从`Query`派生`StringQuery`类，并且只定义其中一个泛型参数，例如为`TResult`指定`string`。要实例化`StringQuery`，你只需要为`TRequest`提供类型：

```
public class Query<TRequest, TResult>
{
}
```

```
public class StringQuery<TRequest> : Query<TRequest, string>
{
}
```

## 静态成员

泛型类的静态成员仅在该类的一个实例化中共享，并且需要特别注意。考虑以下示例，其中类`StaticDemo<T>`包含静态字段x：

```
public class StaticDemo<T>
{
    public static int x;
}
```

因为类`StaticDemo<T>`同时与`string`类型和`int`类型一起使用，所以会存在两组静态字段：

```
StaticDemo<string>.x = 4;
StaticDemo<int>.x = 5;
WriteLine(StaticDemo<string>.x);    // writes 4
```

## 泛型接口

使用泛型，你可以定义带有泛型参数方法的接口。在链表示例中，你已经实现了`IEnumerable<out T>`接口，该接口定义了一个返回`IEnumerator<out T>`的`GetEnumerator`方法。.NET为不同场景提供了许多泛型接口；例如`IComparable<T>`、`ICollection<T>`和`IExtensibleObject<T>`。通常也存在同一接口的较旧的非泛型版本；例如，.NET 1.0有一个基于对象的`IComparable`接口。

`IComparable<in T>`基于一个泛型类型：

```
public interface IComparable<in T>
{
    int CompareTo(T other);
}
```

> 注意 不要被泛型参数使用的in和out关键字弄混淆。它们很快会在“协变与逆变”一节中解释。

较旧的非泛型`IComparable`接口要求一个带有`CompareTo`方法的对象。这需要转换为特定类型，例如转换为`Person`类以使用`LastName`属性：

```
public class Person: IComparable
{
    public int CompareTo(object obj)
    {
        Person other = obj as Person;
        return this.lastname.CompareTo(other.LastName);
    }
    //
```

实现泛型版本后，不再需要将`object`强制转换为`Person`：

```
public class Person: IComparable<Person>
{
    public int CompareTo(Person other) => LastName.CompareTo(other.LastName);
    //...
```

## 协变与逆变

在 .NET 4 之前，泛型接口是不变的。.NET 4 为泛型接口和泛型委托添加了重要的变化：协变和逆变。协变和逆变用于处理带有参数和返回类型的类型转换。例如，你能将`Rectangle`传递给一个要求`Shape`的方法吗？让我们看一些示例，以了解这些扩展的优点。

在 .NET 中，参数类型是协变的。假设你有`Shape`和`Rectangle`两个类，且`Rectangle`派生自`Shape`基类。`Display`方法声明为其参数接受`Shape`类型的对象：

```
public void Display(Shape o) { }
```

现在，你可以传递任何派生自`Shape`基类的对象。因为`Rectangle`派生自`Shape`，所以`Rectangle`满足`Shape`的所有要求，编译器会接受此方法调用：

```
var r = new Rectangle { Width= 5, Height=2.5 };
Display(r);
```

方法的返回类型是逆变的。当方法返回`Shape`时，无法将其赋值给`Rectangle`，因为`Shape`不一定总是`Rectangle`；但相反的情况是可能的。如果某个方法（如`GetRectangle`方法）返回`Rectangle`，

```
public Rectangle GetRectangle();
```

则其结果可以赋值给`Shape`：

```
Shape s = GetRectangle();
```

在 .NET Framework 4 之前，泛型不支持这种行为。自 C# 4 起，该语言得到扩展，支持泛型接口和泛型委托的协变与逆变。让我们首先定义一个`Shape`基类和一个`Rectangle`类（代码文件`Variance/Shape.cs`和`Rectangle.cs`）：

```
public class Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public override string ToString() => $"Width: {Width}, Height: {Height}";
}
```

```
public class Rectangle: Shape
{
}
```

### 泛型接口的协变

如果泛型类型用`out`关键字标注，则泛型接口是协变的。这也意味着类型T只允许用于返回类型。接口 IIndex 对类型T是协变的，从一个只读索引器返回此类型（代码文件`Variance/IIndex.cs`）：

```
public interface IIndex<out T>
{
    T this[int index] { get; }
    int Count { get; }
}
```

IIndex<T>接口由RectangleCollection类实现。RectangleCollection将Rectangle用作泛型类型T：

> 注意 如果对IIndex接口使用读写索引器，泛型类型T会被传入方法并从方法中获取。这对于协变是不可能的；泛型类型必须定义为不变。定义不变类型时不使用out和in注解（代码文件`Variance/RectangleCollection.cs`）：

```
public class RectangleCollection: IIndex<Rectangle>
{
    private Rectangle[] data = new Rectangle[3]
    {
        new Rectangle { Height=2, Width=5 },
        new Rectangle { Height=3, Width=7 },
        new Rectangle { Height=4.5, Width=2.9 }
    };

    private static RectangleCollection _coll;
    public static RectangleCollection GetRectangles() =>
        _coll ?? (_coll = new RectangleCollection());

    public Rectangle this[int index]
    {
        get
        {
            if (index < 0 || index > data.Length)
                throw new ArgumentOutOfRangeException("index");
            return data[index];
        }
    }

    public int Count => data.Length;
}
```

> 注意 RectangleCollection.GetRectangles方法使用了合并运算符。如果变量`_coll`为null，则调用运算符右侧来创建RectangleCollection的新实例，并将其赋给变量`_coll`，随后从该方法返回该实例。该运算符在第8章中详细解释。

RectangleCollection.GetRectangles方法返回一个实现了IIndex<Rectangle>接口的RectangleCollection，因此你可以将返回值赋给一个类型为IIndex<Rectangle>的变量rectangle。因为该接口是协变的，也可以将返回值赋给类型为IIndex<Shape>的变量。Shape并不需要Rectangle提供之外的任何东西。使用shapes变量，在for循环中会用到接口的索引器和Count属性（代码文件`Variance/Program.cs`）：

```
public static void Main()
{
    IIndex<Rectangle> rectangles = RectangleCollection.GetRectangles();
    IIndex<Shape> shapes = rectangles;

    for (int i = 0; i < shapes.Count; i++)
    {
        WriteLine(shapes[i]);
    }
}
```

### 泛型接口的逆变

如果泛型类型用in关键字标注，则泛型接口是逆变的。这样，该接口只允许将泛型类型T用作其方法的输入（代码文件`Variance/IDisplay.cs`）：

```
public interface IDisplay<in T>
{
    void Show(T item);
}
```

ShapeDisplay类实现了IDisplay<Shape>，并使用Shape对象作为输入参数（代码文件`Variance/ShapeDisplay.cs`）：

```
public class ShapeDisplay: IDisplay<Shape>
{
    public void Show(Shape s) =>
        WriteLine($"{s.GetType().Name} Width: {s.Width}, Height: {s.Height}");
}
```

创建ShapeDisplay的新实例会返回IDisplay<Shape>，该值赋给shapeDisplay变量。因为IDisplay<T>是逆变的，所以可以将结果赋给IDisplay<Rectangle>，其中Rectangle派生自Shape。这一次，接口的方法仅将泛型类型用作输入，而Rectangle满足Shape的所有要求（代码文件`Variance/Program.cs`）：

```
public static void Main()
{
    //...
    IDisplay<Shape> shapeDisplay = new ShapeDisplay();
    IDisplay<Rectangle> rectangleDisplay = shapeDisplay;
    rectangleDisplay.Show(rectangles[0]);
}
```

## 泛型结构

