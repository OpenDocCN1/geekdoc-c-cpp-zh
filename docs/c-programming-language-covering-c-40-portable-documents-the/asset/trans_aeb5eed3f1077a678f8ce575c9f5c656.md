
### 11.1.2 partial 修饰符

partial 修饰符表示此 struct-declaration 是一个 partial 类型声明。同一封闭命名空间或类型声明内具有相同名称的多个 partial 结构体声明会合并形成一个结构体声明，其规则在 §10.2 中指定。

### 11.1.3 结构体接口

结构体声明可以包含一个 struct-interfaces 规范，在这种情况下，结构体被认为直接实现了给定的接口类型。

```
struct-interfaces:
  : interface-type-list
```

接口实现在 §13.4 中进一步讨论。

### 11.1.4 结构体体

结构体的 struct-body 定义了结构体的成员。

```
struct-body:
  { struct-member-declarations_opt }
```

## 11.2 结构体成员

结构体的成员由其 struct-member-declarations 引入的成员以及从类型 System.ValueType 继承的成员组成。

```
struct-member-declarations:
  struct-member-declaration
  struct-member-declarations struct-member-declaration
```

```
struct-member-declaration:
  constant-declaration
  field-declaration
  method-declaration
  property-declaration
  event-declaration
  indexer-declaration
  operator-declaration
  constructor-declaration
  static-constructor-declaration
  type-declaration
```

除 §11.3 中所述的差异外，§10.3 至 §10.14 中提供的类成员描述同样适用于结构体成员。

## 11.3 类与结构体的差异

结构体与类在多个重要方面存在差异：

- 结构体是值类型（§11.3.1）。
- 所有结构体类型都隐式继承自类 System.ValueType（§11.3.2）。
- 向结构体类型变量赋值会创建被赋值值的副本（§11.3.3）。
- 结构体的默认值是通过将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 所产生的值（§11.3.4）。
- 使用装箱和拆箱操作在结构体类型与 object 之间进行转换（§11.3.5）。
- this 的含义对结构体不同（§7.6.7）。
- 结构体的实例字段声明不允许包含变量初始值设定项（§11.3.7）。
- 结构体不允许声明无参数实例构造函数（§11.3.8）。
- 结构体不允许声明析构函数（§11.3.9）。

> **JESSE LIBERTY** 请注意，这些差异在语义上是重要的，而不像 C++ 中结构体与类之间的微不足道差异。

### 11.3.1 值语义

结构体是值类型（§4.1），据说具有值语义。相比之下，类是引用类型（§4.2），据说具有引用语义。

> **BILL WAGNER** 下文中关于结构体类型变量直接包含结构体数据的陈述是那些正确但具有误导性的规范陈述之一。结构体可能包含引用类型的成员。结构体的 数据是对类类型的引用。例如：

```
struct Message
{
    int code;
    string message;
    // message contains a reference to a string
    // object, not the characters in the message
}
```

赋值复制的是 message 的引用，而不是其字符本身。

结构体类型变量直接包含结构体的 数据，而类类型变量包含对数据的引用，后者称为对象。当结构体 B 包含类型为 A 的实例字段且 A 是结构体类型时，A 依赖于 B 会导致编译时错误。如果结构体 X 包含类型为 Y 的实例字段，则结构体 X 直接依赖于结构体 Y。给定此定义，结构体所依赖的结构体的完整集合是直接依赖关系的传递闭包。例如，

```
struct Node
{
    int data;
    Node next; // Error: Node directly depends on itself
}
```

这是错误，因为 Node 包含其自身类型的实例字段。另一个例子

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

这是错误，因为类型 A、B 和 C 彼此相互依赖。

对于类，两个变量可能引用同一个对象，因此对一个变量的操作可能影响另一个变量引用的对象。对于结构体，每个变量都有自己数据的副本（ref 和 out 参数变量的情况除外），因此一个变量上的操作不可能影响其他变量。此外，由于结构体不是引用类型，结构体类型的值不可能为 null。

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

输出值为 10。a 赋给 b 时会创建值的副本，因此 b 不受 a.x 赋值的影響。如果 Point 改为声明为类，则输出将为 100，因为 a 和 b 将引用同一个对象。

### 11.3.2 继承

所有结构体类型都隐式继承自类 System.ValueType，而后者又继承自类 object。结构体声明可以指定已实现的接口列表，但结构体声明无法指定基类。

结构体类型永远不是抽象的，并且始终隐式密封。因此，abstract 和 sealed 修饰符不允许出现在结构体声明中。

由于结构体不支持继承，结构体成员声明的访问性不能为 protected 或 protected internal。

结构体中的函数成员不能为 abstract 或 virtual，并且 override 修饰符仅允许重写从 System.ValueType 继承的方法。

### 11.3.3 赋值

向结构体类型变量赋值会创建被赋值值的副本。这与向类类型变量赋值不同，后者复制引用但不复制引用所标识的对象。

类似于赋值，当结构体作为值参数传递或作为函数成员的结果返回时，会创建结构体的副本。结构体可使用 ref 或 out 参数按引用传递给函数成员。

> ERIC LIPPERT 另一种看待此问题的方式是 ref 和 out 参数为变量创建别名。与其想“我将使用 ref 参数按引用传递此结构体”，我更喜欢想“我将使用 ref 参数使此参数成为包含此结构体的变量的别名”。

当结构体的属性或索引器是赋值的目标时，与属性或索引器访问关联的实例表达式必须被分类为变量。如果实例表达式被分类为值，则会发生编译时错误。这在 §7.17.1 中有更详细的描述。

### 11.3.4 默认值

如 §5.2 所述，在创建时，几种类型的变量会自动初始化为其默认值。对于类类型和其他引用类型的变量，此默认值是 null。然而，由于结构体是不能为 null 的值类型，结构体的默认值是通过将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 所产生的值。

参考上面声明的 Point 结构体，示例

```
Point[] a = new Point[100];
```

将数组中的每个 Point 初始化为将 x 和 y 字段设置为零所产生的值。

结构体的默认值对应于结构体默认构造函数返回的值（§4.1.2）。与类不同，结构体不允许声明无参数实例构造函数。相反，每个结构体都隐式具有一个无参数实例构造函数，它始终返回将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 所产生的值。

结构体应设计为将默认初始化状态视为有效状态。在示例中

```
using System;
struct KeyValuePair
{
    string key;
    string value;
    public KeyValuePair(string key, string value) {
        if (key == null || value == null)
            throw new ArgumentException();
        this.key = key;
        this.value = value;
    }
}
```

用户定义的实例构造函数仅在显式调用时才防止 null 值。在 KeyValuePair 变量受默认值初始化的情况中，key 和 value 字段将为 null，结构体必须准备好处理此状态。

### 11.3.5 装箱与拆箱

> BILL WAGNER 自 C# 2.0 引入以来，你通常可以通过使用泛型来避免装箱和拆箱。

类类型的值可以通过在编译时将引用视为另一种类型，简单地转换为 object 类型或由该类实现的接口类型。
