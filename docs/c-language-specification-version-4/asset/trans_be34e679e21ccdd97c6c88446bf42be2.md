
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
        x.Increment();            // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();  // Modify boxed copy of x
        Console.WriteLine(x);
    }
    static void Main() {
        Test<Counter>();
    }
}
```

第一次调用 Increment 修改变量 x 中的值。这与第二次调用 Increment 不等价，后者修改的是 x 的装箱副本中的值。因此，程序的输出为：

0
1
1

有关装箱和拆箱的进一步细节，请参阅 §4.3。

## 11.3.6 this 的含义

在类的实例构造函数或实例函数成员中，this 被归类为值。因此，虽然可以使用 this 来引用调用该函数成员的实例，但在类的函数成员中无法为 this 赋值。

在结构体的实例构造函数中，this 对应于结构体类型的 out 参数，而在结构体的实例函数成员中，this 对应于结构体类型的 ref 参数。在这两种情况下，this 被归类为变量，并且可以通过为 this 赋值或将 this 作为 ref 或 out 参数传递来修改调用该函数成员的整个结构体。

## 11.3.7 字段初始化器

如 §11.3.4 所描述，结构体的默认值由将所有值类型字段设置为其默认值且所有引用类型字段设置为 null 得到的结果组成。因此，结构体不允许实例字段声明包含变量初始化器。此限制仅适用于实例字段。结构体的静态字段允许包含变量初始化器。

示例

```
struct Point
{
    public int x = 1;  // Error, initializer not permitted
    public int y = 1;  // Error, initializer not permitted
}
```

由于实例字段声明包含变量初始化器，因此出错。

## 11.3.8 构造函数

与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，该构造函数始终返回将所有值类型字段设置为其默认值且所有引用类型字段设置为 null 得到的值（§4.1.2）。结构体可以声明具有参数的实例构造函数。例如

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

根据上述声明，以下语句

```
    Point p1 = new Point();
    Point p2 = new Point(0, 0);
```

都创建了一个 x 和 y 初始化为零的 Point。

结构体实例构造函数不允许包含形式为 base(...) 的构造函数初始化器。

如果结构体实例构造函数未指定构造函数初始化器，则 this 变量对应于结构体类型的 out 参数，并且与 out 参数类似，this 必须在构造函数返回的每个位置都已明确赋值（§5.3）。如果结构体实例构造函数指定了构造函数初始化器，则 this 变量对应于结构体类型的 ref 参数，并且与 ref 参数类似，this 在进入构造函数体时被视为已明确赋值。请考虑下面的实例构造函数实现：

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
        X = x;      // error, this is not yet definitely assigned
        Y = y;      // error, this is not yet definitely assigned
    }
}
```

在被构造的结构体的所有字段都已明确赋值之前，不能调用任何实例成员函数（包括属性 X 和 Y 的 set 访问器）。请注意，然而，如果 Point 是类而不是结构体，则实例构造函数实现将被允许。

## 11.3.9 析构函数

结构体不允许声明析构函数。

## 11.3.10 静态构造函数

结构体的静态构造函数遵循与类的大多数相同规则。结构体类型的静态构造函数的执行由应用程序域内首先发生的以下事件触发：

- 引用了结构体类型的静态成员。
- 调用了结构体类型的显式声明的构造函数。

结构体类型的默认值（§11.3.4）的创建不会触发静态构造函数。（一个例子是数组中元素的初始值。）

## 11.4 结构体示例

以下展示了使用结构体类型创建可与语言内置类型类似使用但具有修改后语义的类型两个重要示例。

## 11.4.1 数据库整数类型

下面的 DBInt 结构体实现了一种整数类型，该类型可以表示 int 类型的完整值集合，外加一个表示未知值的额外状态。具有这些特征的类型在数据库中常用。

```
using System;
public struct DBInt
{
    // The Null member represents an unknown DBInt value.
    public static readonly DBInt Null = new DBInt();
    // when the defined field is true, this DBInt represents a known value
    // which is stored in the value field. When the defined field is false,
    // this DBInt represents an unknown value, and the value field is 0.
    int value;
    bool defined;
    // Private instance constructor. Creates a DBInt with a known value.
    DBInt(int value) {
        this.value = value;
        this.defined = true;
    }
    // The IsNull property is true if this DBInt represents an unknown value.
    public bool IsNull { get { return !defined; } }
    // The Value property is the known value of this DBInt, or 0 if this
    // DBInt represents an unknown value.
    public int Value { get { return value; } }
    // Implicit conversion from int to DBInt.
    public static implicit operator DBInt(int x) {
        return new DBInt(x);
    }
    // Explicit conversion from DBInt to int. Throws an exception if the
    // given DBInt represents an unknown value.
public static explicit operator int(DBInt x) {
    if (!x.defined) throw new InvalidOperationException();
    return x.value;
}
public static DBInt operator +(DBInt x) {
    return x;
}
public static DBInt operator -(DBInt x) {
    return x.defined ? -x.value : Null;
}
public static DBInt operator +(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value + y.value: Null;
}
public static DBInt operator -(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value - y.value: Null;
}
public static DBInt operator *(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value * y.value: Null;
}
public static DBInt operator /(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value / y.value: Null;
}
public static DBInt operator %(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value % y.value: Null;
}
public static DBBool operator ==(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value == y.value: DBBool.Null;
}
public static DBBool operator !=(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value != y.value: DBBool.Null;
}
public static DBBool operator >(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value > y.value: DBBool.Null;
}
public static DBBool operator <(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value < y.value: DBBool.Null;
}
public static DBBool operator >=(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value >= y.value: DBBool.Null;
}
public static DBBool operator <=(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value <= y.value: DBBool.Null;
}
public override bool Equals(object obj) {
    if (!(obj is DBInt)) return false;
    DBInt x = (DBInt)obj;
    return value == x.value && defined == x.defined;
}
public override int GetHashCode() {
    return value;
}
public override string ToString() {
    return defined? value.ToString(): "DBInt.Null";
}
}
```
