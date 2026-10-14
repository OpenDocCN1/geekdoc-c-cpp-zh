

## Note

尽管 x 和 y 字段是私有的，但同一类的其他实例仍然可以访问它们。重要的是要理解，private 术语在类级别上操作，而不在对象级别上；同一类的两个对象可以访问彼此的私有数据，但其他类的实例对象则不能。

要计算距离，可以使用毕达哥拉斯定理并计算 xDiff 的平方与 yDiff 的平方之和的平方根。System.Math 类提供了 Sqrt 方法，可用于计算平方根。

4. 声明一个名为 distance 的 double 类型变量，并用前面描述的计算结果来保存它。

Click here to view code image

```
public double DistanceTo(Point other)
{
    int xDiff = this.x - other.x;
    int yDiff = this.y - other.y;
    double distance = Math.Sqrt((xDiff * xDiff) + (yDiff * yDiff));
}
```

5. 在 DistanceTo 方法末尾添加 return 语句并返回 distance 变量中的值：

Click here to view code image

```
public double DistanceTo(Point other)
{
    int xDiff = this.x - other.x;
    int yDiff = this.y - other.y;
    double distance = Math.Sqrt((xDiff * xDiff) + (yDiff * yDiff));
    return distance;
}
```

您现在将测试 DistanceTo 方法。

6. 返回 Program 类中的 doWork 方法。在声明并初始化 origin 和 bottomRight Point 变量的语句之后，声明一个名为 distance 的 double 类型变量。用调用 origin 对象的 DistanceTo 方法并将 bottomRight 对象作为参数传递给它时得到的结果来初始化这个 double 变量。

doWork 方法现在应如下所示：

Click here to view code image

```
static void doWork()
{
    Point origin = new Point();
    Point bottomRight = new Point(1366, 768);
    double distance = origin.DistanceTo(bottomRight);
}
```

## Note

当你在 origin 后输入句点字符时，Microsoft IntelliSense 应显示 DistanceTo 方法。

7. 在 doWork 方法中添加另一条语句，使用 Console.WriteLine 方法将 distance 变量的值写入控制台。
完成的 doWork 方法应如下所示：

Click here to view code image

```
static void doWork()
{
    Point origin = new Point();
    Point bottomRight = new Point(1366, 768);
    double distance = origin.DistanceTo(bottomRight);
    Console.WriteLine($"Distance is: {distance}");
}
```

8. 在 Debug 菜单上，单击 Start Without Debugging。

9. 确认值 1568.45465347265 已写入控制台窗口，然后按 Enter 关闭应用程序并返回 Visual Studio 2015。

## Understanding static methods and data

在前面的练习中，您使用了 Math 类的 Sqrt 方法。同样地，在查看 Circle 类时，您读取了 Math 类的 PI 字段。如果仔细想想，您调用 Sqrt 方法或读取 PI 字段的方式有点奇怪。您是在类本身上调用方法或读取字段，而不是在 Math 类型的对象上。就像在前面的练习中添加的代码里试图写 Point.DistanceTo 而不是 origin.DistanceTo 一样。那么发生了什么，以及这是如何工作的？

您经常会发现并非所有方法都自然属于类的实例；它们是实用方法，因为它们提供了一个有用的功能，该功能独立于任何特定的类实例。Console 类的 WriteLine 方法在整本书中被广泛使用，这是一个常见的例子。Sqrt 方法是另一个例子。如果 Sqrt 是 Math 的实例方法，您就必须创建一个 Math 对象来调用 Sqrt：

```
Math m = new Math();
double d = m.Sqrt(42.24);
```

这会很麻烦。Math 对象在计算平方根中不会发挥任何作用。Sqrt 所需的所有输入数据都提供在参数列表中，并且结果通过方法的返回值传递回调用者。这里根本不需要对象，因此强行将 Sqrt 放入实例的束缚中并不是一个好主意。

## Note

除了包含 Sqrt 方法和 PI 字段之外，Math 类还包含许多其他数学实用方法，例如 Sin、Cos、Tan 和 Log。

在 C# 中，所有方法都必须在类中声明。但是，如果将方法或字段声明为 static，您就可以使用类名来调用方法或访问字段，而不需要实例。这就是 Math 类的 Sqrt 方法的声明方式：

Click here to view code image

```
class Math
{
    public static double Sqrt(double d)
    {
        ...
    }
    ...
}
```

您可以这样调用 Sqrt 方法：

```
double d = Math.Sqrt(42.24);
```

静态方法不依赖于类的实例，并且不能访问类中定义的任何实例字段或实例方法；它只能使用标记为 static 的字段和其他方法。

## Creating a shared field

将字段定义为 static 使您能够为从单个类创建的所有对象创建一个共享的字段实例。 （非静态字段对每个对象实例都是本地的。）在下面的示例中，Circle 类中的静态字段 NumCircles 在每次创建新的 Circle 对象时都会由 Circle 构造函数递增：

Click here to view code image

```
class Circle
{
    private int radius;
    public static int NumCircles = 0;

    public Circle() // default constructor
    {
        radius = 0;
        NumCircles++;
    }

    public Circle(int initialRadius) // overloaded constructor
    {
        radius = initialRadius;
        NumCircles++;
    }
}
```

所有 *Circle* 对象共享同一个 *NumCircles* 字段的实例，因此语句 *NumCircles++*; 每次创建新实例时都会递增相同的数据。请注意，您不能使用 *this* 关键字为 *NumCircles* 加前缀，因为 *NumCircles* 不属于特定对象。

您可以通过指定 *Circle* 类而不是 *Circle* 对象从类外部访问 *NumCircles* 字段，如以下示例所示：

Click here to view code image

```
Console.WriteLine($"Number of Circle objects: {Circle.NumCircles}");
```

## Note

请记住，静态方法也称为 *class methods*。然而，静态字段通常不称为 *class fields*；它们只是称为 *static fields*（或有时称为 *static variables*）。

## Creating a static field by using the const keyword

通过在字段前加上 *const* 关键字，您可以声明该字段是 static 的，但其值永远不会改变。关键字 *const* 是 *constant* 的缩写。*const* 字段在其声明中不使用 *static* 关键字，但仍然是 static 的。然而，出于超出本书范围的原因，您只能在字段为数值类型（例如 *int* 或 *double*）、字符串或枚举时声明字段为 *const*。 （您将在第 9 章“使用枚举和结构创建值类型”中了解有关枚举的信息。）例如，这里是 *Math* 类如何将 *PI* 声明为 *const* 字段：

Click here to view code image

```
class Math
{
    ...
    public const double PI = 3.14159265358979;
}
```

## Understanding static classes

C# 语言的另一个特性是能够将类声明为 *static*。静态类只能包含静态成员。 （使用该类创建的所有对象共享这些成员的单个副本。）静态类的目的是纯粹充当实用方法和字段的持有者。静态类不能包含任何实例数据或方法，并且使用 *new* 运算符从静态类创建对象是没有意义的。事实上，即使你想这样做，你也不能使用 *new* 来创建静态类的实例。 （如果尝试，编译器会报告错误。）如果需要执行任何初始化，静态类可以有一个默认构造函数，只要它也被声明为 *static*。任何其他类型的构造函数都是非法的，并且会被编译器报告。

如果您要定义自己的 *Math* 类版本，其中只包含静态成员，它可能看起来像这样：

Click here to view code image

```
public static class Math
{
    public static double Sin(double x) {...}
    public static double Cos(double x) {...}
    public static double Sqrt(double x) {...}
    ...
}
```

## Note

真正的 *Math* 类并非以这种方式定义，因为它实际上确实有一些实例方法。

## Static *using* statements

每当您调用静态方法或引用静态字段时，您必须指定方法或字段所属的类，例如 *Math.Sqrt* 或 *Console.WriteLine*。静态 *using* 语句使您能够将类引入作用域，并在访问静态成员时省略类名。它们的工作方式与将命名空间引入作用域的普通 *using* 语句非常相似。下面的示例说明了如何使用它们：

Click here to view code image

```
using static System.Math;
using static System.Console;
...
```

