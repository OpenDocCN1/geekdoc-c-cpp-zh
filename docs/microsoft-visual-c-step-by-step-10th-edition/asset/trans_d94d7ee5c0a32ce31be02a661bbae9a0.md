

```csharp
class Circle
{
    private int radius;
    public Circle() // 默认构造函数
    {
        radius = 0;
    }

    public double Area()
    {
        return Math.PI * radius * radius;
    }
}
```

```csharp
Circle c;
c = new Circle();
double area0fCircle = c.Area();
```

```csharp
class Circle
{
    private int radius;
    public Circle() // 默认构造函数
    {
        radius = 0;
    }

    public Circle(int initialRadius) // 重载的构造函数
    {
        radius = initialRadius;
    }

    public double Area()
    {
        return Math.PI * radius * radius;
    }
}
```

```csharp
partial class Circle
{
    public Circle() // 默认构造函数
    {
        this.radius = 0;
    }

    public Circle(int initialRadius) // 重载的构造函数
    {
        this.radius = initialRadius; 
    }
}
```

```csharp
partial class Circle
{
    private int radius;
    public double Area()
    {
        return Math.PI * this.radius * this.radius;
    }
}
```

```csharp
class Program
{
    static void doWork()
    {
        // TODO: 测试 Point 类：
    }

    static void Main(string[] args)
    {
        try
        {
            doWork();
        } catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

```csharp
class Point
{
    public Point(int x, int y)
    {
        Console.WriteLine($"x:{x}, y:{y}");
    }
}
```

没有对应于 'Point.Point(int, int)' 所需形式参数 'x' 的参数。

```csharp
class Point
{
    public Point()
    {
        Console.WriteLine("调用默认构造函数");
    }

    public Point(int x, int y)
    {
        Console.WriteLine($"x:{x}, y:{y}");
    }
}
```

```csharp
static void doWork()
{
    var origin = new Point();
    var bottomRight = new Point(2496, 1664);
}
```

```csharp
class Point
{
    private int x, y;
    public Point()
    {
        Console.WriteLine("调用默认构造函数");
    }

    public Point(int x, int y)
    {
        Console.WriteLine($"x:{x}, y:{y}");
    }
}
```

```csharp
public Point(int x, int y) // 不要这样打字！
{
    x = x;
    y = y;
}
```

```csharp
class Point
{
    ...
    public double DistanceTo(Point other)
    {
    }
}
```

```csharp
public double DistanceTo(Point other)
{
    int xDiff = this.x - other.x;
}
```

```csharp
public double DistanceTo(Point other)
{
    int xDiff = this.x - other.x;
    int yDiff = this.y - other.y;
}
```

```csharp
public double DistanceTo(Point other)
{
    int xDiff = this.x - other.x;
    int yDiff = this.y - other.y;
    double distance = Math.Sqrt((xDiff * xDiff) + (yDiff * yDiff));
}
```

```csharp
public double DistanceTo(Point other)
{
    int xDiff = this.x - other.x;
    int yDiff = this.y - other.y;
    double distance = Math.Sqrt((xDiff * xDiff) + (yDiff * yDiff));
    return distance;
}
```

```csharp
static void doWork()
{
    Point origin = new Point();
    Point bottomRight = new Point(2496, 1664);
    double distance = origin.DistanceTo(bottomRight);
    Console.WriteLine($"距离为: {distance}");
    Console.WriteLine($"Point 对象数量: {Point.Count()}");
}
```

```csharp
myAnonymousObject = new { Name = "John", Age = 47 };
```

```csharp
var myAnonymousObject = new { Name = "John", Age = 47 };
```

```csharp
Console.WriteLine("名称: {myAnonymousObject.Name} 年龄: {myAnonymousObject.Age}");
```

```csharp
var anotherAnonymousObject = new { Name = "Diana", Age = 53 };
```

```csharp
anotherAnonymousObject = myAnonymousObject;
```

```csharp
class Point
{
    public Point(int x, int y)
    {
        ...
    }
}
```

```csharp
Point origin = new Point(0, 0);
```

```csharp
class Point
{
    public static int ObjectCount()
    {
        ...
    }
}
```

```csharp
int pointsCreatedSoFar = Point.ObjectCount();
```

```csharp
class Point
{
    ...
    private static int objectCount;
}
```

```csharp
class Math
{
    ...
    public const double PI = ...;
}
```

```csharp
double area = Math.PI * radius * radius;
```

```csharp
int i = 42; // 定义并初始化 i
int copyi = i; /* copyi 包含了 i 中数据的拷贝：
               i 和 copyi 的值均为 42 */
i++;
               /*  i 对 copyi 没有影响；
               i 现在包含 43，但 copyi 仍然包含 42 */
```

```csharp
var refc = new Circle();
refc.radius = c.radius; // 不要尝试这样做
```

```csharp
class Circle
{
    private int radius;
    // 省略构造函数和其他方法
    ...
    public Circle Clone()
    {
        // 创建一个新的 Circle 对象
        Circle clone = new Circle();

        // 将私有数据从这里拷贝到 clone
        clone.radius = this.radius;

        // 返回包含拷贝数据的 Circle 对象
        return clone;
    }
}
```

```csharp
namespace Parameters
{
    class Pass
    {
        public static void Value(int param)
        {
            param = 42;
        }
    }
}
```

```csharp
public static void Reference(WrappedInt param)
{
    param.Number = 42;
}
```

```csharp
static void doWork()
{
    // int i = 0;
    // Console.WriteLine(i);
    // Pass.Value(i);
    // Console.WriteLine(i);
    var wi = new WrappedInt();
    // Console.WriteLine(wi.Number);
    // Pass.Reference(wi);
    // Console.WriteLine(wi.Number);
}
```

```csharp
var c = new Circle(42);
var copy = new Circle(99); // 初始化 copy 的某个随机值
...
copy = c;                   // copy 和 c 指向同一个对象
```

```csharp
var c = new Circle(42);
Circle copy; // 未初始化 !!!
...
if (copy == // 只有在 copy 未初始化时才赋值，但这里写什么呢？）
{
    copy = c; // copy 和 c 指向同一个对象
    ...
}
```

