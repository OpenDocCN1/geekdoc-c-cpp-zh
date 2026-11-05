
```
object_initializer
  : '{' member_initializer_list? '}'
  | '{' member_initializer_list ',' '}'
  ;

member_initializer_list
  : member_initializer (',' member_initializer)*
  ;

member_initializer
  : initializer_target '=' initializer_value
  ;

initializer_target
  : identifier
  | '[' argument_list ']'
  ;

initializer_value
  : expression
  | object_or_collection_initializer
  ;
```

对象初始值设定项由一系列成员初始值设定项组成，这些成员初始值设定项由 { 和 } 标记括起来，并以逗号分隔。每个 member_initializer 应指定一个初始化目标。标识符应命名正在初始化的对象的一个可访问字段或属性，而用方括号括起来的 argument_list 应指定正在初始化的对象上一个可访问索引器的参数。对象初始值设定项为同一字段或属性包含多个成员初始值设定项是错误的。

注意：虽然不允许对象初始值设定项多次设置同一字段或属性，但对索引器没有此类限制。对象初始值设定项可以包含多个引用索引器的初始值设定项目标，甚至可以多次使用相同的索引器参数。注释结束

每个 initializer_target 后跟一个等号，以及一个表达式、一个对象初始值设定项或一个集合初始值设定项。对象初始值设定项内的表达式不能引用它正在初始化的新创建对象。

在等号后指定表达式的成员初始值设定项，其处理方式与对目标进行赋值（§11.18.2）相同。

在等号后指定对象初始值设定项的成员初始值设定项是嵌套对象初始值设定项，即对嵌入对象的初始化。嵌套对象初始值设定项中的赋值不会向该字段或属性赋予新值，而是被视为对该字段或属性成员的赋值。嵌套对象初始值设定项不能应用于值类型的属性，也不能应用于值类型的只读字段。

在等号后指定集合初始值设定项的成员初始值设定项是对嵌入集合的初始化。初始化器中给定的元素不会向目标字段、属性或索引器赋予新集合，而是添加到该目标引用的集合中。目标应是满足 §11.7.15.4 中规定要求的集合类型。

当初始值设定项目标引用索引器时，索引器的参数应始终恰好计算一次。因此，即使这些参数最终从未被使用（例如，由于空的嵌套初始值设定项），也会为它们的副作用而计算它们。

示例：以下类表示具有两个坐标的点：

```csharp
public class Point
{
    public int X { get; set; }
    public int Y { get; set; }
}
```

可以按如下方式创建并初始化 Point 的实例：

```csharp
Point a = new Point { X = 0, Y = 1 };
```

其效果与以下代码相同：

```csharp
Point __a = new Point();
__a.X = 0;
__a.Y = 1;
Point a = __a;
```

其中 __a 是一个在其他方面不可见且不可访问的临时变量。以下类表示由两个点创建的矩形：

```csharp
public class Rectangle
{
    public Point P1 { get; set; }
    public Point P2 { get; set; }
}
```

可以按如下方式创建并初始化 Rectangle 的实例：

```csharp
Rectangle r = new Rectangle
{
    P1 = new Point { X = 0, Y = 1 },
    P2 = new Point { X = 2, Y = 3 }
};
```

其效果与以下代码相同：

```csharp
Rectangle __r = new Rectangle();
Point __p1 = new Point();
__p1.X = 0;
__p1.Y = 1;
__r.P1 = __p1;
Point __p2 = new Point();
__p2.X = 2;
__p2.Y = 3;
__r.P2 = __p2;
Rectangle r = __r;
```

其中 __r、__p1 和 __p2 是在其他方面不可见且不可访问的临时变量。

如果 Rectangle 的构造函数分配两个嵌入的 Point 实例

```csharp
public class Rectangle
{
    public Point P1 { get; } = new Point();
    public Point P2 { get; } = new Point();
}
```

则可以使用以下构造来初始化这些嵌入的 Point 实例，而不是赋予新实例：

```csharp
Rectangle r = new Rectangle
{
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```

其效果与以下代码相同：

```csharp
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

示例结束

### 11.7.15.4 集合初始值设定项

```
collection_initializer
: '{' element_initializer_list '}'
| '{' element_initializer_list ';' '}'
;

element_initializer_list
: element_initializer (',' element_initializer)*
;

element_initializer
: non_assignment_expression
| '{' expression_list '}'
;

expression_list
: expression
| expression_list ',' expression
;
```

集合初始值设定项由一系列元素初始值设定项组成，这些元素初始值设定项由 { 和 } 标记括起来，并以逗号分隔。每个元素初始值设定项指定要添加到正在初始化的集合对象中的一个元素，并由一个表达式列表组成，该表达式列表由 { 和 } 标记括起来并以逗号分隔。单表达式元素初始值设定项可以不带大括号书写，但此时不能是赋值表达式，以避免与成员初始值设定项产生歧义。non_assignment_expression 产生式在 §11.19 中定义。

示例：以下是一个包含集合初始值设定项的对象创建表达式的示例：

```csharp
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

示例结束

应用集合初始值设定项的集合对象应是实现 System.Collections.IEnumerable 的类型，否则会发生编译时错误。对于按顺序指定的每个元素，都会应用普通成员查找来查找名为 Add 的成员。如果成员查找的结果不是方法组，则会发生编译时错误。否则，以元素初始值设定项的表达式列表作为参数列表应用重载决策，并且集合初始值设定项会调用得到的方法。因此，对于每个元素初始值设定项，集合对象应包含一个名称为 `Add` 的适用实例方法或扩展方法。

*示例：* 以下类表示一个包含姓名和电话号码列表的联系人：

```csharp
public class Contact
{
    public string Name { get; set; }
    public List<string> PhoneNumbers { get; } = new List<string>();
}
```

可以按如下方式创建并初始化一个 List<Contact>：

```csharp
var contacts = new List<Contact>
{
    new Contact
    {
        Name = "Chris Smith",
        PhoneNumbers = { "206-555-0101", "425-882-8080" }
    },
    new Contact
    {
        Name = "Bob Harris",
        PhoneNumbers = { "650-555-0199" }
    }
};
```

其效果与以下代码相同：

```csharp
var __clist = new List<Contact>();
Contact __c1 = new Contact();
__c1.Name = "Chris Smith";
__c1.PhoneNumbers.Add("206-555-0101");
__c1.PhoneNumbers.Add("425-882-8080");
__clist.Add(__c1);
Contact __c2 = new Contact();
__c2.Name = "Bob Harris";
__c2.PhoneNumbers.Add("650-555-0199");
__clist.Add(__c2);
var contacts = __clist;
```

其中 __clist、__c1 和 __c2 是在其他方面不可见且不可访问的临时变量。

*示例结束*

### 11.7.15.5 数组创建表达式

```
array_creation_expression
    : 'new' non_array_type '[' expression_list ']' rank_specifier*
      array_initializer?
    | 'new' array_type array_initializer
    | 'new' rank_specifier array_initializer
    ;
```

第一种形式的数组创建表达式分配一个数组实例，其类型是通过从表达式列表中删除各个表达式后得到的类型。

示例：数组创建表达式 `new int[10, 20]` 生成一个类型为 `int[,]` 的数组实例，而数组创建表达式 `new int[10][,]` 生成一个类型为 `int[,][,]` 的数组实例。示例结束

表达式列表中的每个表达式都应是 `int`、`uint`、`long` 或 `ulong` 类型，或者可隐式转换为这些类型中的一种或多种。每个表达式的值确定新分配的数组实例中对应维度的长度。由于数组维度的长度应为非负值，因此表达式列表中包含值为负的常量表达式属于编译时错误。

除非在不安全上下文（§22.2）中，否则数组的布局是未指定的。

如果第一种形式的数组创建表达式包含数组初始值设定项，则表达式列表中的每个表达式都应是常量，并且表达式列表指定的秩和维度长度应与数组初始值设定项的秩和维度长度匹配。

在第二种或第三种形式的数组创建表达式中，指定的数组类型或秩说明符的秩应与数组初始值设定项的秩匹配。各个维度长度从数组初始值设定项中每个对应嵌套级别的元素数量推断出来。因此，表达式

```
new int[,] {{0, 1}, {2, 3}, {4, 5}}
```

完全对应于

```
new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}
```

第三种形式的数组创建表达式称为隐式类型数组创建表达式。它与第二种形式类似，不同之处在于数组的元素类型不是显式给出的，而是确定为数组初始值设定项中表达式集合的最佳通用类型（§11.6.3.15）。对于多维数组，即 rank_specifier 包含至少一个逗号的数组，该集合包含嵌套 array_initializers 中找到的所有表达式。

数组初始值设定项在 §16.7 中进一步描述。

计算数组创建表达式的结果被归类为值，即对新分配的数组实例的引用。数组创建表达式的运行时处理包括以下步骤：

- expression_list 的维度长度表达式按从左到右的顺序计算。在计算每个表达式之后，会执行到以下类型之一的隐式转换（§10.2）：`int`、`uint`、`long`、`ulong`。选择此列表中存在隐式转换的第一种类型。如果表达式的计算或后续隐式转换导致异常，则不再计算其他表达式，也不再执行其他步骤。
- 对维度长度的计算值进行验证，如下所示：如果一个或多个值小于零，则引发 `System.OverflowException`，并且不再执行其他步骤。
- 分配具有给定维度长度的数组实例。如果没有足够的内存可用于分配新实例，则引发 `System.OutOfMemoryException`，并且不再执行其他步骤。
- 新数组实例的所有元素都初始化为其默认值（§9.3）。

