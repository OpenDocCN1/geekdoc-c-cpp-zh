
```csharp
// 创建一个新的 Circle 对象
Circle clone = new Circle();
// 将私有数据从 this 拷贝到 clone
clone.radius = this.radius;
// 返回包含拷贝数据的 Circle 对象
return clone;
}
}
namespace Parameters
{
    class Pass
    {
        public static void Value(int param)
        {
            param = 42;
        }
        static void doWork()
        {
            int i = 0;
            Console.WriteLine(i);
            Pass.Value(i);
            Console.WriteLine(i);
        }
    }
}
```

```csharp
namespace Parameters
{
    class WrappedInt
    {
        public int Number;
    }
    public static void Reference(WrappedInt param)
    {
        param.Number = 42;
    }
    static void doWork()
    {
        // int i = 0;
        // Console.WriteLine(i);
        // Pass.Value(i);
        // Console.WriteLine(i);
        WrappedInt wi = new WrappedInt();
        Console.WriteLine(wi.Number);
        Pass.Reference(wi);
        Console.WriteLine(wi.Number);
    }
}
```

```csharp
Circle c = new Circle(42);
Circle copy = new Circle(99); // 某个随机值，用于初始化
copy = c;
Circle c = new Circle(42);
Circle copy;
if (copy == // 仅当 copy 未初始化时才赋值，但这里应该填什么？）
copy = c; // copy 和 c 指向同一个对象
Circle c = new Circle(42);
Circle copy = null; // 已初始化
```

```csharp
if (copy == null)
{
    copy = c; // copy 和 c 指向同一个对象
}
```

```csharp
Circle c = null;
Console.WriteLine("圆 c 的面积是 {c.Area()}");
int i = 0;
double d = 0.0;
// copy 和 c 指向同一个对象
// 未初始化 !!!
```

```csharp
if (c != null)
{
    Console.WriteLine($"The area of circle c is {c.Area()}");
    Console.WriteLine($"The area of circle c is {c?.Area()}");
    if (i == null)
    {
        ...
    }
}
int? i = null;
int j = 99;
i = 100; // 将值类型常量拷贝到可空类型
i = j; // 将值类型变量拷贝到可空类型
int? i = 99;
Pass.Value(i); // 编译错误
int? i = null;
...
if (!i.HasValue)
{
    // 如果 i 为空，则给它赋值为 99
    i = 99;
}
else
{
    // 如果 i 不为空，则显示它的值
    Console.WriteLine(i.Value);
}
static void doIncrement(int param)
{
    param++;
}
static void Main()
{
    int arg = 42;
    doIncrement(arg);
    Console.WriteLine(arg); // 写入 42，而不是 43
}
static void doIncrement(ref int param) // 使用 ref
{
    param++;
}
static void Main()
{
    int arg = 42;
    doIncrement(ref arg); // 使用 ref
    Console.WriteLine(arg); // 写入 43
}
```

```csharp
static void doIncrement(ref int param)
{
    param++;
}
static void Main()
{
    int arg; // 未初始化
    doIncrement(ref arg);
    Console.WriteLine(arg);
}
static void doInitialize(out int param)
{
    param = 42; // 在结束前初始化 param
}
static void doInitialize(out int param)
{
    // 什么都不做
}
static void doInitialize(out int param)
{
    param = 42;
}
static void Main()
{
    int arg; // 未初始化
    doInitialize(out arg); // 合法
    Console.WriteLine(arg); // 写入 42
}
class Pass
{
    public static void Value(ref int param)
    {
        param = 42;
    }
...
}
```

```csharp
class Program
{
    static void doWork()
    {
        int i = 0;
        Console.WriteLine(i);
        Pass.Value(ref i);
        Console.WriteLine(i);
        ...
    }
}
```

```csharp
while (...)
{
    int i = ...; // i 在这里创建于栈上
    ...
}
```

```csharp
// i 在这里从栈上消失
void Method(int param)
{
    Circle c;
    c = new Circle(param);
    ...
    Circle c;
    c = new Circle(42);
    object o;
    o = c;
    int i = 42;
    object o = i;
    Circle c = new Circle();
}
```

```csharp
int i = 42;
object o;
o = c; // o 指向一个圆
i = o; // i 中存储了什么？
i = 42; // 装箱
```

```csharp
object o = i; // 装箱
i = (int)o; // 编译通过
Circle c = new Circle(42);
object o = c; // 没有装箱，因为 Circle 是引用变量
int i = (int)o; // 编译通过但在运行时抛出异常
```

```csharp
WrappedInt wi = new WrappedInt();
...
object o = wi;
if (o is WrappedInt)
{
    WrappedInt temp = (WrappedInt)o; // 这是安全的；o 是 WrappedInt
    ...
    WrappedInt wi = new WrappedInt();
    ...
    object o = wi;
    ...
    if (o is WrappedInt temp)
    {
        ... // 在此处使用 temp
    }
    WrappedInt wi = new WrappedInt();
    object o = wi;
    WrappedInt temp = o as WrappedInt;
    if (temp != null)
    {
        ... // 转换成功
    }
}
Circle c = new Circle(42); // 半径为 42 的圆
Square s = new Square(55); // 边长为 55 的正方形
Triangle t = new Triangle(33); // 边长为 33 的等边三角形
object o = s;
...
if (o is Circle)
{
    ... // Circle，Circle 中有一个可用的引用
}
else if (o is Square)
{
    ... // Square，Square 中有一个可用的引用
}
else if (o is Triangle)
{
    ... // Triangle，Triangle 中有一个可用的引用
}
```

```csharp
switch (o)
{
    case Circle:
        ... // Circle，Circle 中有一个可用的引用
        break;
    case Square:
        ... // Square，Square 中有一个可用的引用
        break;
    case Triangle:
        ... // Triangle，Triangle 中有一个可用的引用
        break;
    default:
        throw new ArgumentException("变量不是识别的形状");
        break;
}
switch (o)
{
    case Circle when Circle.Radius > 10:
        ...
        break;
    case Square when Square.SideLength == 100:
        ...
        break;
}
int* pi;
int i = 99;
...
pi = &i;
```

```csharp
public static void Main(string[] args)
{
    int x = 99, y = 100;
    unsafe
    {
        swap(&x, &y);
    }
    Console.WriteLine($"x is now {x}, y is now {y}");
}
public static void swap(int* a, int* b)
{
    int temp;
    temp = *a;
    *b = temp;
}
int i = 42;
int copy = i;
Circle c = new Circle(42);
Circle c = c;
static void Main()
{
    int arg = 42;
    doWork(ref arg);
    Console.WriteLine(arg);
}
static void Main()
{
    int arg;
    doWork(out arg);
    Console.WriteLine(arg);
}
WrappedInt wi = new WrappedInt();
object o = wi;
if (o is WrappedInt)
{
    ...
    WrappedInt wi = new WrappedInt();
    ...
    object o = wi;
    WrappedInt temp = o as WrappedInt;
    if (temp != null)
    {
        ...
    }
}
```

```csharp
enum Season { Spring, Summer, Fall, Winter }
enum Season { Spring, Summer, Fall, Winter }
class Example
{
    public void Method(Season parameter) // 参数
    Season localVariable; // 局部变量
    private Season currentSeason; // 字段
    Season colorful = Season.Fall;
    Console.WriteLine(colorful); // 写入 'Fall'
    string name = colorful.toString();
    Console.WriteLine(name); // 也写入 'Fall'
}
enum Season { Spring, Summer, Fall, Winter }
```

```csharp
Season colorful = Season.Fall;
Console.WriteLine((int)colorful); // 写入 '2'
enum Season { Spring = 1, Summer, Fall, Winter }
enum Season { Spring, Summer, Fall = Autumn, Winter }
enum Season { short { Spring, Summer, Fall, Winter }
```

```csharp
namespace StructsAndEnums {
    enum Month {
        January, February, March, April,
        May, June, July, August,
        September, October, November, December
    }
    static void doWork() {
        Month first = Month.January;
        Console.WriteLine(first);
    }
    static void doWork() {
        Month first = Month.January;
        Console.WriteLine(first);
        first++;
        Console.WriteLine(first);
    }
}
```

```csharp
static void doWork()
{
    Month first = Month.December;
    Console.WriteLine(first);
    first++;
    Console.WriteLine(first);
}
int i = 55;
Console.WriteLine(i.ToString());
Console.WriteLine(55.ToString());
float f = 98.765F;
Console.WriteLine(f.ToString());
Console.WriteLine(98.765F.ToString());
Console.WriteLine((500, 600).ToString()); // (500, 600) 是一个元组
string s = "42";
int i = int.Parse(s); // 与 Int32.Parse 完全相同
struct Time
{
    public int hours, minutes, seconds;
}
struct Time
{
    private int hours, minutes, seconds;
    ...
    public Time(int hh, int mm, int ss)
    {
        this.hours = hh % 24;
        this.minutes = mm % 60;
        this.seconds = ss % 60;
    }
    public int Hours()
    {
        return this.hours;
    }
}
struct Time
{
    public Time() { ... } // 编译错误
    ...
}
}
```

```csharp
struct Time
{
    private int hours, minutes, seconds;
    ...
    public Time(int hh, int mm)
    {
```
