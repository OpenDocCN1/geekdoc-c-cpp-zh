
另一种，你也可以在声明时初始化属性，如下所示：

点击此处查看代码图像

```
class Circle
{
    public DateTime CircleCreatedDate { get; } = DateTime.Now;
}
```

请注意，如果你以这种方式初始化属性，并且在构造函数中设置了它的值，那么构造函数提供的值将覆盖属性初始化器指定的值。请在这两种方法中二选一，而不要两者都用！

> 注意
> 你不能创建只写入的属性。如果你尝试创建一个不带 get 访问器的自动属性，将看到编译时错误。

## 使用属性初始化对象

在第 7 章中，你学习了如何定义构造函数来初始化对象。一个对象可以有多个构造函数，你可以定义具有不同参数的构造函数来初始化对象中的不同元素。例如，你可以定义一个模拟三角形的类，如下所示：

点击此处查看代码图像

```
public class Triangle
{
    private int sideLength;
    private int side2Length;
    private int side3Length;

    // 默认构造函数 - 所有边的默认值
    public Triangle()
{
  this.sideLength = this.side2Length = this.side3Length = 10;
}
```

```csharp
// 指定 sideLength 的长度，其他使用默认值
public Triangle(int length1)
{
  this.sideLength = length1;
  this.side2Length = this.side3Length = 10;
}
```

```csharp
// 指定 sideLength 和 side2Length 的长度，
// side3Length 使用默认值
public Triangle(int length1, int length2)
{
  this.sideLength = length1;
  this.side2Length = length2;
  this.side3Length = 10;
}
```

```csharp
// 指定所有边的长度
public Triangle(int length1, int length2, int length3)
{
  this.sideLength = length1;
  this.side2Length = length2;
  this.side3Length = length3;
}
```

根据类包含的字段数量以及你想要启用的初始化字段的各种组合，你可能会写出很多构造函数。如果许多字段具有相同类型，还会存在潜在的问题：你可能无法为所有字段组合编写一个唯一的构造函数。例如，在之前的 Triangle 类中，你无法轻松添加一个仅初始化 sideLength 和 side3Length 字段的构造函数，因为它没有唯一的签名；它接受两个 int 参数，而初始化 sideLength 和 side2Length 的构造函数已经具有此签名。

一种可能的解决方案是定义一个接受可选参数的构造函数，并在创建 Triangle 对象时通过参数指定参数的值。然而，一个更好且更透明的解决方案是将私有字段初始化一组默认值，并将它们作为属性暴露，如下所示：

点击此处查看代码图像

```csharp
public class Triangle
{
    private int sideLength = 10;
    private int side2Length = 10;
    private int side3Length = 10;

    public int SideLength
{
        set => this.sideLength = value;
    }

    public int Side2Length
{
        set => this.side2Length = value;
    }

    public int Side3Length
{
        set => this.side3Length = value;
    }
}
```

当你创建一个类的实例时，可以通过指定任何具有 set 访问器的公共属性的名称和值来初始化它。例如，你可以创建 Triangle 对象并初始化三边的任何组合，如下所示：

点击此处查看代码图像

```csharp
Triangle tri1 = new Triangle { Side3Length = 15 };
Triangle tri2 = new Triangle { SideLength = 15, Side3Length = 20 };
Triangle tri3 = new Triangle { Side2Length = 12, Side3Length = 17 };
Triangle tri4 = new Triangle { SideLength = 9, Side2Length = 12, Side3Length = 15 };
```

这种语法被称为对象初始化器。当你以这种方式调用对象初始化器时，C# 编译器会生成代码，调用默认构造函数，然后调用每个命名属性的 set 访问器以用指定的值对其进行初始化。你也可以对象初始化器与非默认构造函数结合使用。例如，如果 Triangle 类还提供了一个接受单个字符串参数以描述三角形类型的构造函数，你可以调用此构造函数并初始化其他属性，如下所示：

点击此处查看代码图像

```csharp
Triangle tri5 = new Triangle("Equilateral triangle")
{
    Side1Length = 3,
    Side2Length = 3,
    Side3Length = 3
}
```

需要记住的一点是，构造函数首先运行，然后设置属性。如果构造函数将对象中的字段设置为特定值，而你指定的属性更改了这些值，那么理解这种顺序是非常重要的。

## 自动属性和不可变性

自动属性的一个缺点是，它们必须是可变的，以便初始化器能够正常工作。回想一下对象初始化过程：首先通过构造函数实例化对象，然后在对象创建后将值写入指定的属性中。如果属性是只读的（它有 get 访问器但没有 set 访问器），一旦对象实例化，任何更改属性的尝试都将失败，即使使用对象初始化语法也是如此。

幸运的是，C# 9.0更高版本提供了自动 init-only 属性来处理这种情况。你通过创建 init-only 属性来处理这种情况。下面的示例显示了一个具有 init 访问器的类：

```csharp
class Grade
{
    public int StudentID { get; init; }
    public string Subject { get; init; }
    public char SubjectGrade { get; init; }
}
```

你可以使用 init 访问器来初始化属性，如下所示：

```csharp
var grade1 = new Grade { StudentID = 1, Subject = "Math", SubjectGrade = 'A' };
```

然而，一旦对象创建，任何修改它的尝试都会导致：

```csharp
grade1.SubjectGrade = 'B'; // 编译错误：init-only 属性 'Grade.SubjectGrade' 只能在对象初始化器中赋值
```

在下一个练习中，我们将定义一个类来模拟具有多边形。

## 定义自动属性并使用对象初始化器

1. 在 Visual Studio 中打开 AutomaticProperties 解决方案。
2. 在解决方案资源管理器中，右键点击 AutomaticProperties 项目，点击添加，并选择“类”。
3. 在名称框中，输入 Polygon.cs，然后选择“添加”。

Polygon.cs 文件已创建并添加到项目中，并出现在代码编辑器中。

4. 如下所示向 Polygon 类添加自动属性 NumSides 和 SideLength：

```csharp
class Polygon
{
    public int NumSides { get; set; }
    public double SideLength { get; set; }
}
```

5. 将所示的默认构造函数添加到 Polygon 类中：

```csharp
class Polygon
{
    public Polygon()
    {
        this.NumSides = 4;
        this.SideLength = 10.0;
    }
}
```

此构造函数使用默认值初始化 NumSides 和 SideLength 字段。在此处，默认的多边形是一个边长为 10 的正方形。

6. 在代码窗口中显示 Program.cs 文件。

7. 将所示语句添加到 doWork 方法中，替换 TODO 注释：

```csharp
static void doWork()
{
    Polygon square = new Polygon();
    Polygon triangle = new Polygon { NumSides = 3 };
    Polygon pentagon = new Polygon { SideLength = 15.5, NumSides = 5 };
}
```

这些语句创建了 Polygon 对象。square 变量使用构造函数初始化。triangle 和 pentagon 变量也使用构造函数初始化，然后这些代码更改了 Polygon 类暴露的属性值。对于 triangle 变量，NumSides 属性被设置为 3，但 SideLength 属性保持默认值 10.0。对于 pentagon 变量，代码更改了 SideLength 和 NumSides 的值。

8. 将所示代码添加到 doWork 方法的末尾：

```csharp
static void doWork()
{
```
