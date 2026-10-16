

给正在调用的函数传递几个参数。你可以使用它快速地将布尔值转换为字符串值 true 或 false。它也很适合用于显示单词正确的单数或复数形式：

```csharp
int x = 1;
string s = x + "";
s += (x == 1 ? "man" : "men");
WriteLine(s);
```

这段代码在 x 等于 1 时显示 1 man，但对于任何其他数字则显示正确的复数形式。但请注意，如果你的输出需要本地化为不同的语言，就必须编写更复杂的例程，以考虑不同语言的不同语法规则。

## checked 和 unchecked 运算符

考虑以下代码：

```csharp
byte b = byte.MaxValue;
b++;
WriteLine(b);
```

byte 数据类型只能保存 0 到 255 范围内的值。将 byte.MaxValue 赋给 byte 会得到 255。对于 255，byte 中可用的 8 位全部被置位：11111111。将此值加一会导致溢出，结果为 0。

CLR 如何处理这种情况取决于许多因素，包括编译器选项；因此，只要存在意外溢出的风险，就需要某种方法来确保获得你想要的结果。

为此，C# 提供了 checked 和 unchecked 运算符。如果将代码块标记为 checked，CLR 将强制执行溢出检查，并在发生溢出时抛出 OverflowException。以下代码修改了前面的代码，加入了 checked 运算符：

```csharp
byte b = 255;
checked
{
    b++;
}
WriteLine(b);
```

尝试运行此代码时，你会看到类似这样的错误消息：

```
System.OverflowException: Arithmetic operation resulted in an overflow.
```

> **注意** 你可以通过指定 /checked 编译器选项，对程序中所有未标记的代码强制执行溢出检查。

如果希望取消溢出检查，可以将代码标记为 `unchecked`：

```csharp
byte b = 255;
unchecked
{
    b++;
}
WriteLine(b);
```

在这种情况下，不会引发异常，但你会丢失数据，因为 `byte` 类型无法保存 256 这个值，溢出的位会被丢弃，你的 `b` 变量的值为零（0）。

请注意，`unchecked` 是默认行为。唯一可能需要显式使用 `unchecked` 关键字的情况是，在显式标记为 `checked` 的较大块中，需要少量未检查的代码行。

> **注意** *默认编译设置为 `/unchecked`，因为强制检查会影响性能。使用 `/checked` 时，每次算术运算的结果都需要验证值是否超出范围。算术运算也通过使用 `i++` 的 `for` 循环完成。为了避免这种性能影响，最好保留默认的 `/unchecked` 编译器设置，并在需要的地方使用 `checked` 运算符。*

## is 运算符

`is` 运算符允许你检查对象是否与特定类型兼容。“兼容”意味着对象要么是该类型，要么派生自该类型。例如，若要检查变量是否与 `object` 类型兼容，可以使用以下代码：

```csharp
int i = 10;
if (i is object)
{
    WriteLine("i is an object");
}
```

`int` 与所有 C# 数据类型一样，继承自 `object`；因此，在这种情况下，表达式 `i is object` 的计算结果为 `true`，并会显示相应的消息。

## as 运算符

`as` 运算符用于对引用类型执行显式类型转换。如果要转换的类型与指定类型兼容，则转换成功执行。但是，如果类型不兼容，`as` 运算符将返回值 `null`。如下面的代码所示，如果 `object` 引用实际上并不引用字符串实例，则尝试将 `object` 引用转换为 `string` 会返回 `null`：

```csharp
object o1 = "Some String";
object o2 = 5;

string s1 = o1 as string; // s1 = "Some String"
string s2 = o2 as string; // s2 = null
```

as 运算符允许你在单个步骤中执行安全的类型转换，而无需先使用 is 运算符测试类型，然后再执行转换。

> **注意** is 和 as 运算符将在第 4 章“继承”中结合继承展示。

## sizeof 运算符

你可以使用 sizeof 运算符来确定值类型在栈上所需的大小（以字节为单位）：

```csharp
WriteLine(sizeof(int));
```

这会显示数字 4，因为 int 的长度为 4 个字节。

如果对复杂类型（而非基元类型）使用 sizeof 运算符，则需要将代码块放在 unsafe 块中，如下所示：

```csharp
unsafe
{
    WriteLine(sizeof(Customer));
}
```

第 5 章将更详细地介绍不安全代码。

## typeof 运算符

typeof 运算符返回表示指定类型的 System.Type 对象。例如，typeof(string) 返回表示 System.String 类型的 Type 对象。当你希望使用反射动态查找有关对象的信息时，这很有用。有关更多信息，请参阅第 16 章“反射、元数据和动态编程”。

## nameof 运算符

nameof 运算符是 C# 6 中新增的。该运算符接受符号、属性或方法，并返回其名称。

它有什么用处？一个例子是需要变量名称时，例如检查参数是否为 null：

```csharp
public void Method(object o)
{
    if (o == null) throw new ArgumentNullException(nameof(o));
}
```

当然，不使用 nameof 运算符，而是传入一个字符串来抛出异常，效果也类似。但是，如果拼错名称，传入字符串不会产生编译器错误。此外，当你更改参数名称时，很容易忘记更改传递给 ArgumentNullException 构造函数的字符串。

```csharp
if (o == null) throw new ArgumentNullException("o");
```

使用 nameof 运算符获取变量名称只是一个用例。你还可以使用它获取属性名称——例如，在属性 set 访问器中触发更改事件（使用 INotifyPropertyChanged 接口）并传递属性名称。

```csharp
public string FirstName
{
    get { return _firstName; }
    set
    {
        _firstName = value;
        OnPropertyChanged(nameof(FirstName));
    }
}
```

nameof 运算符还可以用于获取方法的名称。即使方法被重载，这也同样有效，因为所有重载都会产生相同的值：方法的名称。

```csharp
public void Method()
{
    Log($"{nameof(Method)} called");
}
```

## index 运算符

在第 7 章“数组和元组”中，你已经使用索引运算符（方括号）访问数组。这里，索引运算符通过传递数字 2 来访问名为 arr1 的数组的第三个元素：

```csharp
int[] arr1 = {1, 2, 3, 4};
int x = arr1[2]; // x == 3
```

与访问数组元素类似，索引运算符也在集合类中实现（将在第 11 章“集合”中讨论）。

索引运算符不要求括号内必须是整数。索引运算符可以使用任何类型定义。以下代码片段创建了一个泛型字典，其中键是 string，值是 int。对于字典，键可以与索引器一起使用。在下面的示例中，字符串 first 被传递给索引运算符以在字典中设置此元素，然后将相同的字符串传递给索引器以检索此元素：

```csharp
var dict = new Dictionary<string, int>();
dict["first"] = 1;
int x = dict["first"];
```

> **注意** 在本章后面的“实现自定义索引运算符”一节中，你可以了解如何在自己的类中创建索引运算符。

## 可空类型和运算符

值类型和引用类型之间的一个重要区别是引用类型可以为 null。而 int 这样的值类型不能为 null。这在将 C# 类型映射到数据库类型时是一个特殊问题。数据库中的数字可以为 null。在早期 C# 版本中，解决方案是使用引用类型来映射可空的数据库数字。然而，这种方法会影响性能，因为垃圾回收器需要处理引用类型。现在你可以使用可空 int 而不是普通 int。这样做的开销只是一个额外的 Boolean，用于检查或设置 null 值。可空类型仍然是值类型。

在下面的代码片段中，变量 i1 是一个 int，被赋值为 1。i2 是一个可空 int，被赋值为 2。可空性通过将 ? 与类型一起使用来定义。int? 可以像 i1 的赋值一样被赋予整数值。变量 i3 演示了可空类型也可以被赋予 null。

```csharp
int i1 = 1;
int? i2 = 2;
int? i3 = null;
```

每个结构体都可以定义为可空类型，如 long? 和 DateTime? 所示：

```csharp
long? l1 = null;
DateTime? d1 = null;
```

如果在程序中使用可空类型，则必须始终考虑 null 值在与各种运算符一起使用时可能产生的影响。通常，当对可空类型使用一元或二元运算符时，如果一个或两个操作数为 null，则结果将为 null。例如：

```csharp
int? a = null;

int? b = a + 4;      // b = null
int? c = a * 5;      // c = null
```

比较可空类型时，如果只有一个操作数为 null，则比较结果始终为 false。这意味着你不能仅仅因为条件的相反情况为 false 就假定条件为 true，而在使用非可空类型的程序中这种情况经常发生。例如，在下面的示例中，如果 a 为 null，那么无论 b 的值是 +5 还是 -5，都会始终执行 else 子句。

```csharp
int? a = null;
int? b = -5;
```

