
-   这对于结构体 (§7.6.7) 的含义不同。
-   结构体的实例字段声明不允许包含变量初始值设定项 (§11.3.7)。
-   结构体不允许声明无参数的实例构造函数 (§11.3.8)。
-   结构体不允许声明析构函数 (§11.3.9)。

## 11.3.1 值语义

结构体是值类型 (§4.1)，据说具有值语义。另一方面，类是引用类型 (§4.2)，据说具有引用语义。

一个结构体类型变量直接包含结构体的數據，而一个类类型变量包含对数据的引用，后者称为对象。当结构体 B 包含类型为 A 的实例字段且 A 是结构体类型时，A 依赖于 B 会导致编译时错误。如果结构体 X 包含类型为 Y 的实例字段，则结构体 X 直接依赖于结构体 Y。基于此定义，结构体所依赖的结构体完整集合是直接依赖关系的传递闭包。例如

```
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```

是错误，因为 Node 包含其自身类型的实例字段。另一个例子

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

是错误，因为类型 A、B 和 C 彼此相互依赖。

对于类，两个变量可以引用同一个对象，因此对一个变量的操作可能会影响另一个变量引用的对象。对于结构体，变量各自拥有数据的副本（ref 和 out 参数变量的情况除外），因此一个变量上的操作不可能影响另一个变量。此外，由于结构体不是引用类型，结构体类型的值不可能为 null。

给定声明

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

```
Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);
```

输出值为 10。将 a 赋给 b 会创建值的副本，因此 b 不受对 a.x 的赋值影响。如果 Point 改为声明为类，则输出将为 100，因为 a 和 b 将引用同一个对象。

## 11.3.2 继承

所有结构体类型都隐式继承自类 System.ValueType，而后者又继承自类 object。结构体声明可以指定已实现的接口列表，但结构体声明不能指定基类。

结构体类型永远不是抽象的，并且始终隐式密封。因此，abstract 和 sealed 修饰符不允许出现在结构体声明中。

由于结构体不支持继承，结构体成员声明的访问性不能是 protected 或 protected internal。

结构体中的函数成员不能是 abstract 或 virtual，并且 override 修饰符仅允许用于重写从 System.ValueType 继承的方法。

## 11.3.3 赋值

将值赋给结构体类型变量会创建被赋值的副本。这与将值赋给类类型变量不同，后者复制引用但不复制引用所标识的对象。

类似于赋值，当结构体作为值参数传递或作为函数成员的结果返回时，会创建结构体的副本。结构体可以通过 ref 或 out 参数按引用传递给函数成员。

当结构体的属性或索引器的目标是赋值时，与属性或索引器访问关联的实例表达式必须被分类为变量。如果实例表达式被分类为值，则会发生编译时错误。这在 §7.17.1 中有更详细的描述。

## 11.3.4 默认值

如 §5.2 中所述，几种类型的变量在创建时会自动初始化为其默认值。对于类类型和其他引用类型的变量，此默认值是 null。然而，由于结构体是不能为 null 的值类型，结构体的默认值是通过将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 而产生的值。

参考上面声明的 Point 结构体，示例

```
Point[] a = new Point[100];
```

将数组中的每个 Point 初始化为将 x 和 y 字段设置为零而产生的值。

结构体的默认值对应于结构体默认构造函数返回的值 (§4.1.2)。与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，该构造函数始终返回将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 而产生的值。

结构体应设计为将默认初始化状态视为有效状态。在示例中

```
using System;
struct KeyValuePair
{
    string key;
    string value;
    public KeyValuePair(string key, string value) {
        if (key == null || value == null) throw new ArgumentException();
        this.key = key;
        this.value = value;
    }
}
```

用户定义的实例构造函数仅在显式调用时才防止 null 值。在 KeyValuePair 变量受默认值初始化的情况中，key 和 value 字段将为 null，并且结构体必须准备好处理此状态。

## 11.3.5 装箱和拆箱

类类型的值可以通过在编译时将引用视为另一种类型，简单地转换为 object 类型或由该类实现的接口类型。同样，object 类型的值或接口类型的值可以转换回类类型，而不会更改引用（但当然在这种情况下需要运行时类型检查）。

由于结构体不是引用类型，这些操作对于结构体类型实现方式不同。当结构体类型的值转换为 object 类型或由结构体实现的接口类型时，会发生装箱操作。同样，当 object 类型的值或接口类型的值转换回结构体类型时，会发生拆箱操作。与类类型上的相同操作相比，关键区别在于装箱和拆箱会将结构体值复制到装箱实例中或从装箱实例中复制出来。因此，在装箱或拆箱操作之后，对未装箱结构体的更改不会反映在装箱结构体中。

当结构体类型重写从 System.Object 继承的虚方法（如 Equals、GetHashCode 或 ToString）时，通过结构体类型实例调用虚方法不会导致装箱发生。即使结构体用作类型参数并且调用通过类型参数类型实例发生时也是如此。例如：

```csharp
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

尽管 ToString 具有副作用是不好的风格，但该示例证明了对 x.ToString() 的三次调用均未发生装箱。

同样，在受约束的类型参数上访问成员时，装箱永远不会隐式发生。例如，假设接口 ICounter 包含一个可用于修改值的方法 Increment。如果 ICounter 用作约束，则 Increment 方法的实现会使用对调用 Increment 的变量的引用调用，从不使用装箱的副本。
