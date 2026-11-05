
- 将值赋给结构体类型的变量会创建被赋值的副本 (§16.4.4)。
- 结构体的默认值是通过将所有字段设置为其默认值而产生的数值 (§16.4.5)。
- 装箱和拆箱操作用于在结构体类型与某些引用类型之间进行转换 (§16.4.6)。
- this 在结构体成员中的含义与类中不同 (§16.4.7)。
- 结构体的实例字段声明不允许包含变量初始值设定项 (§16.4.8)。
- 结构体不允许声明无参数的实例构造函数 (§16.4.9)。
- 结构体不允许声明终结器。

## 16.4.2 值语义

结构体是值类型 (§9.3)，据说具有值语义。另一方面，类是引用类型 (§9.2)，据说具有引用语义。

结构体类型的变量直接包含结构体的數據，而类类型的变量包含对包含数据的对象的引用。当结构体 B 包含类型为 A 的实例字段且 A 是结构体类型时，A 依赖于 B 或由 B 构造的类型会成为编译时错误。如果 X 包含类型为 Y 的实例字段，则结构体 X 直接依赖于结构体 Y。给定此定义，结构体所依赖的结构体的完整集合是直接依赖关系的传递闭包。

```
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```

是错误，因为 Node 包含其自身类型的实例字段。另一个示例

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

是错误，因为类型 A、B 和 C 彼此相互依赖。 end example

对于类，两个变量可能引用同一个对象，因此对一个变量的操作可能影响另一个变量所引用的对象。对于结构体，变量各自拥有数据的副本（ref 和 out 参数变量的情况除外），因此一个变量上的操作不可能影响另一个变量。此外，除非显式可空 (§9.3.11)，结构体类型的值不可能为 null。 [Note: 如果结构体包含引用类型的字段，则所引用对象的内容可以由其他操作更改。然而字段本身的值，即它引用哪个对象，不能通过对不同结构体值的修改来更改。 end note]

```
struct Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

代码片段

Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);

```
public KeyValuePair(string key, string value) {
    if (key == null || value == null) throw new ArgumentException();
    this.key = key;
    this.value = value;
}
```

用户定义的实例构造函数仅在显式调用时才防止空值。在 KeyValuePair 变量受默认值初始化的情况下，key 和 value 字段将为 null，并且结构体应准备好处理此状态。 end note]

## 16.4.6 装箱和拆箱

类类型的值可以通过在编译时将引用视为另一种类型，简单地转换为 object 类型或由该类实现的接口类型。同样，object 类型的值或接口类型的值可以转换回类类型而不会更改引用（当然，在这种情况下需要运行时类型检查）。

由于结构体不是引用类型，这些操作对于结构体类型实现方式不同。当结构体类型的值转换为某些引用类型时（定义见 §11.2.8），会发生装箱操作。同样，当某些引用类型的值（定义见 §11.3.6）转换回结构体类型时，会发生拆箱操作。与类类型上的相同操作相比，装箱和拆箱会将结构体值复制到装箱实例中或从装箱实例中复制出来这一关键区别。 [Note: 因此，在装箱或拆箱操作之后，对未装箱结构体的更改不会反映在装箱的结构体中。 end note]

有关装箱和拆箱的更多详细信息，请参阅 §11.2.8 和 §11.3.6。

## 16.4.7 this 的含义

结构体中 this 的含义与类中 this 的含义不同，如 §12.7.8 所述。当结构体类型重写从 System.ValueType 继承的虚方法时（如 Equals、GetHashCode 或 ToString），通过结构体类型的实例调用虚方法不会导致装箱发生。即使结构体用作类型参数并且调用通过类型参数类型的实例发生，也同样成立。 [Example:

```
using System;
struct Counter
{
    int value;
    public override string ToString() {
        value++;
        return value.ToString();
    }
}
class Program
{
    static void Test<T>() where T: new() {
        T x = new T();
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
    }
    static void Main() {
        Test<Counter>();
    }
}
```

程序的输出是：
1
2
3

虽然 ToString 具有副作用是不好的风格，但该示例证明了对 x.ToString() 的三次调用均未发生装箱。 end example]

同样，当在约束类型参数上访问成员时，如果该成员在值类型内实现，则永远不会隐式发生装箱。例如，假设接口 ICounter 包含一个可用于修改值的方法 Increment。如果 ICounter 用作约束，则 Increment 方法的实现会使用对调用 Increment 的变量的引用调用，而永远不是装箱的副本。 [Example:

```csharp
using System;
interface ICounter
{
    void Increment();
}
struct Counter: ICounter
{
    int value;
    public override string ToString() {
        return value.ToString();
    }
    void ICounter.Increment() {
        value++;
    }
}
class Program
{
    static void Test<T>() where T: ICounter, new() {
        T x = new T();
        Console.WriteLine(x);
        x.Increment();    // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();  // Modify boxed copy of x
        Console.WriteLine(x);
    }
    static void Main() {
        Test<Counter>();
    }
}
```

第一次调用 Increment 修改变量 x 中的值。这与第二次调用 Increment 不等价，后者修改的是 x 的装箱副本中的值。因此，程序的输出是：

0
1
1

end example]

## 16.4.8 字段初始值设定项

如 §16.4.5 所述，结构体的默认值由将所有值类型字段设置为其默认值且所有引用类型字段设置为 null 所产生的值组成。因此，结构体不允许实例字段声明包含变量初始值设定项。此限制仅适用于实例字段。结构体的静态字段允许包含变量初始值设定项。 [Example: 以下

```csharp
struct Point
{
    public int x = 1; // Error, initializer not permitted
    public int y = 1; // Error, initializer not permitted
}
```

是错误的，因为实例字段声明包含变量初始值设定项。 end example]

## 16.4.9 构造函数

与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，该构造函数始终返回将所有值类型字段设置为其默认值且所有引用类型字段设置为 null 所产生的值 (§9.3.3)。结构体可以声明具有参数的实例构造函数。 [Example:

```
struct Point
{
    int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

给定上述声明，语句

```
Point p1 = new Point();
Point p2 = new Point(0, 0);
```

都创建了一个 x 和 y 初始化为零的 Point。 end example]

结构体实例构造函数不允许包含形式为 base(argument-list) 的构造函数初始值设定项。

结构体实例构造函数的 this 参数对应于结构体类型的 out 参数。因此，this 必须在构造函数返回的每个位置都被明确赋值 (§10.4)。同样，在被明确赋值之前，不能在构造函数体中读取它（即使是隐式读取）。

如果结构体实例构造函数指定了构造函数初始值设定项，则该初始值设定项被视为对 this 的明确赋值，该赋值发生在构造函数体之前。因此，主体本身没有初始化要求。 [Example: 考虑以下实例构造函数实现：

```
struct Point
{
    int x, y;
    public int X {
        set { x = value; }
    }
    public int Y {
        set { y = value; }
    }
    public Point(int x, int y) {
        X = x;    // error, this is not yet definitely assigned
        Y = y;    // error, this is not yet definitely assigned
    }
}
```

在被构造的结构体的所有字段都被明确赋值之前，不能调用任何实例函数成员（包括属性 X 和 Y 的 set 访问器）。请注意，然而，如果 Point 是类而不是结构体，则实例构造函数实现将被允许。
end example]

## 16.4.10 静态构造函数

结构体的静态构造函数遵循与类的大多数相同规则。结构体类型的静态构造函数的执行由应用程序域内首先发生的以下事件触发：

- 引用了结构体类型的静态成员。
- 调用了结构体类型的显式声明的构造函数。

