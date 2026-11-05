
## 7. 表达式

以下构造可用于初始化嵌入的 Point 实例，而非分配新的实例：

```
Rectangle r = new Rectangle {
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```

其效果与以下相同

```
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

### 7.6.10.3 集合初始化器

集合初始化器指定集合的元素。

```
collection-initializer:
    { element-initializer-list }
    { element-initializer-list , }

element-initializer-list:
    element-initializer
    element-initializer-list , element-initializer

element-initializer:
    non-assignment-expression
    { expression-list }

expression-list:
    expression
    expression-list , expression
```

集合初始化器由一系列元素初始化器组成，这些初始化器用 { 和 } 标记括起来并以逗号分隔。每个元素初始化器指定要添加到正在初始化的集合对象中的一个元素，并由用 { 和 } 标记括起来并以逗号分隔的表达式列表组成。单表达式元素初始化器可以不使用大括号书写，但此时不能是赋值表达式，以避免与成员初始化器的歧义。非赋值表达式产生式在 §7.18 中定义。

下面是一个包含集合初始化器的对象创建表达式的示例：

```
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

应用集合初始化器的集合对象必须是实现 System.Collections.IEnumerable 的类型，否则会发生编译时错误。对于每个指定的元素，按顺序，集合初始化器会在目标对象上调用 Add 方法，并将元素初始化器的表达式列表作为参数列表，使用正常的重载解析进行每次调用。因此，集合对象必须为每个元素初始化器包含一个适用的 Add 方法。

> ERIC LIPPERT  这里的规则有点奇怪：只有当对象实现 IEnumerable 且具有 Add 方法时，集合初始化器才是有效的。请注意，我们在集合初始化器中从不调用 IEnumerable 的任何方法！那么为什么我们要求它呢？C# 设计团队对现有对象进行了调查并得出了以下发现。首先，几乎所有具有 Add 方法的对象要么是集合，要么在实现某种算术运算。我们明确不希望这种设计成为算术运算的语法糖——只是集合创建。其次，在那些是集合的对象中，没有一个通用的接口被它们全部实现 Add 方法。第三，所有集合都实现了 IEnumerable，但算术对象则没有。由于所有这些原因，我们决定使用 IEnumerable 的存在加上 Add 方法作为判断集合初始化器是否有效的试金石。

下面的类表示具有姓名和电话号码列表的联系人：

```
public class Contact
{
    string name;
    List<string> phoneNumbers = new List<string>();
    public string Name { get { return name; } set { name = value; } }
    public List<string> PhoneNumbers { get { return phoneNumbers; } }
}
```

可以按如下方式创建并初始化 List<Contact>：

```
var contacts = new List<Contact> {
    new Contact {
        Name = "Chris Smith",
        PhoneNumbers = { "206-555-0101", "425-882-8088" }
    },
    new Contact {
        Name = "Bob Harris",
        PhoneNumbers = { "650-555-0199" }
    }
};
```

其效果与以下相同

```
var __clist = new List<Contact>();
Contact __c1 = new Contact();
__c1.Name = "Chris Smith";
__c1.PhoneNumbers.Add("206-555-0101");
__c1.PhoneNumbers.Add("425-882-8088");
__clist.Add(__c1);
Contact __c2 = new Contact();
__c2.Name = "Bob Harris";
__c2.PhoneNumbers.Add("650-555-0199");
__clist.Add(__c2);
var contacts = __clist
```

其中 __clist、__c1 和 __c2 是临时变量，否则不可见且无法访问。

### 7.6.10.4 数组创建表达式

数组创建表达式用于创建数组类型的新的实例。

```
array-creation-expression:
new non-array-type [ expression-list ] rank-specifiers_opt array-initializer_opt
new array-type array-initializer
new rank-specifier array-initializer
```

第一种形式的数组创建表达式分配一个数组实例，其类型是从表达式列表中删除每个单独表达式后得到的类型。例如，数组创建表达式 new int[10, 20] 生成类型为 int[,] 的数组实例，而数组创建表达式 new int[10][,] 生成类型为 int[][,] 的数组。表达式列表中的每个表达式必须是 int、uint、long 或 ulong 类型，或可隐式转换为其中一种或多种类型。每个表达式的值决定了新分配的数组实例中相应维度的长度。由于数组维度的长度必须为非负，因此在表达式列表中出现负值的常量表达式是编译时错误。

除在不安全上下文 (§18.1) 中外，数组的布局是未指定的。

如果第一种形式的数组创建表达式包含数组初始化器，则表达式列表中的每个表达式必须是常量，并且表达式列表指定的秩和维度长度必须与数组初始化器的相匹配。

在第二种或第三种形式的数组创建表达式中，指定的数组类型或秩说明符的秩必须与数组初始化器的秩匹配。各个维度长度是从数组初始化器的相应嵌套层级中的元素数量推断出来的。因此表达式

```
new int[,] {{0, 1}, {2, 3}, {4, 5}}
```

完全对应于

```
new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}
```

第三种形式的数组创建表达式被称为 *隐式类型化数组创建表达式*。它与第二种形式类似，只是数组的元素类型没有明确给出，而是根据数组初始化器中表达式集合的最佳公共类型 (§7.5.2.14) 确定。对于多维数组——即 *秩说明符* 包含至少一个逗号的数组——该集合包含嵌套 *数组初始化器* 中找到的所有 *表达式*。

数组初始化器在 §12.6 中进一步描述。

求值数组创建表达式的结果被归类为值——即对新分配的数组实例的引用。数组创建表达式的运行时处理包括以下步骤：

- 表达式列表的维度长度表达式按从左到右的顺序求值。在求值每个表达式后，执行一次到以下类型之一的隐式转换 (§6.1)：int、uint、long、ulong。选择列表中存在隐式转换的第一个类型。如果表达式的求值或随后的隐式转换导致异常，则不再求值任何进一步的表达式且不再执行后续步骤。
- 计算得到的维度长度值按如下方式验证。如果一个或多个值小于零，则抛出 System.OverflowException 且不再执行后续步骤。
- 分配具有给定维度长度的数组实例。如果没有足够的内存分配新实例，则抛出 System.OutOfMemoryException 且不再执行后续步骤。
- 新数组实例的所有元素都初始化为其默认值 (§5.2)。
- 如果数组创建表达式包含数组初始化器，则数组初始化器中的每个表达式都会被求值并赋给其对应的数组元素。求值和赋值按照表达式在数组初始化器中书写的顺序执行——换句话说，元素按递增的索引顺序初始化，最右边的维度最先递增。如果给定表达式的求值或随后对其对应数组元素的赋值导致异常，则不再初始化任何进一步的元素（因此剩余元素将保持其默认值）。
