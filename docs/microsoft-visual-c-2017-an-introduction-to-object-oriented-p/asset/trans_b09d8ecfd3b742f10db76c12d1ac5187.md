

在第二条语句中，`IdNumber` 属性被设置为 2345。等号右侧的值被赋值给名为 `value` 的隐式参数设置访问器。（隐式参数是指未声明并自动获取值的参数）。在语句 `myChe.IdNumber = 2345;` 中，常量 2345 被发送到 `set` 访问器，在那里它变成了 `value` 的值。在 `set` 访问器内部，`value` 被赋值给字段 `idNumber`。由于 `idNumber` 是私有的，无法通过 `Main()` 找到该字段；然而，由于属性是公共的，可以通过其 `set` 访问器设置 `IdNumber`。

编写读取访问器（getter）允许你像使用简单变量一样使用属性。例如，声明的 `Employee` 员工编号可以通过以下方式显示：`WriteLine("ID number is {0}", myChe.IdNumber);`

表达式 `myChe.IdNumber`（使用以小写 `i` 开头的字段名在客户端程序中是不被允许的，因为 `idNumber` 是私有的；然而，属性的公共 `get` 访问器允许 `myChe.IdNumber` 显示）。图 9-9 显示了一个使用图 9-8 中定义的 `Employee` 类的完整应用程序。图 9-10 显示了输出。

```c
using static System.Console;
class CreateEmployee2
{
    static void Main()
{
        Employee myChe = new Employee();
        myChe.IdNumber = 2345;
        WriteLine("ID number is {0}", myChe.IdNumber);
        myChe.WelcomeMessage();
    }
}
```

图 9-9 使用包含属性的 `Employee` 类的 CreateEmployee2 应用程序

ID number is 2345
Welcome from Employee #2345
How can I help you?

图 9-10 CreateEmployee2 应用程序的输出

此时，声明除了从字段检索值或给字段赋值外什么都不做的 `get` 和 `set` 访问器似乎工作量很大但回报很少。毕竟，如果字段是公共的而不是私有的，你只需直接使用它，而无需创建属性的工作。然而，按照惯例（并符合面向对象的原则），将类的字段设为私有，并允许访问器按照你认为适当的方式对其进行操作。保持数据隐藏是面向对象编程的一个重要特性，因为它控制了数据值的设置和使用方式。此外，你可以自定义访问器以限制你想要对某些字段实施的检索和访问限制。例如，你可以编写如下的 `set` 访问器来限制 `Employee` 类中的 ID 编号：

```c
set
if(value < 500)
    idNumber = value;
else
    idNumber = 500;
```

此 `set` 访问器将确保 `Employee` 的 `idNumber` 永远不会大于 500。如果客户端可以直接访问私有的 `idNumber` 字段，你就无法控制可以分配哪些值，但当你为类编写自定义的 `set` 访问器时，你就获得了对允许值的完全控制权。

使用属性时的一个小不便是，属性不能作为 `ref` 或 `out` 参数传递给方法。例如，如果 `idNumber` 是 `Employee` 属性且 `myChef` 是一个 `Employee` 对象，则以下语句无法编译：
`int.TryParse(ReadLine(), out myChef.idNumber);`

相反，要使用 `TryParse()` 交互式地获取 `idNumber` 值，你必须使用临时变量，如下例：
```csharp
int temp;
int.TryParse(ReadLine(), out temp);
myChef.idNumber = temp;
```

## 使用自动实现属性

虽然可以在属性的 `get` 和 `set` 访问器中包含任意数量的自定义语句，但常见的情况是 `set` 访问器只需将值分配给相应的字段，而 `get` 访问器只需返回字段值。由于 `get` 和 `set` 访问器中的代码通常非常标准且简洁，程序员有时会采用几种简写方法来编写属性。

例如，与其像图 9-8 那样使用 11 行代码编写 `IdNumber` 属性，程序员可能会用五行编写该属性，如下：

```csharp
public int IdNumber
{
    get {return idNumber;}
    set {idNumber = value;}
}
```

这种格式并没有消除属性原始版本中的任何字符；它只是消除了部分空格，将每个访问器放在单行上。

其他程序员选择了更紧凑的格式 `{get {return idNumber;} set {idNumber = value;}}`。

