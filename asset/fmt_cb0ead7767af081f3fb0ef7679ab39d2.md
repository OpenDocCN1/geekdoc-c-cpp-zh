
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

```
e = Employee.Lookup("Joe");

year = e.GetYearsEmployed();

e.GetProgressReport();

}
```

**图 4-8** 在线程栈上为 M3 分配局部变量

随后，M3 执行代码来构造一个 `Manager` 对象。这导致在托管堆中创建一个 `Manager` 类型的实例，即一个 `Manager` 对象，如图 4-9 所示。如你所见，`Manager` 对象与所有对象一样——具有一个类型指针和一个同步块索引。该对象还包含了存储 `Manager` 类型定义的所有实例数据字段所需的字节（在本例中，为 `Employee` 和 `Object`）。每当在堆上创建新对象时，CLR 都会初始化内部对象指针成员，指向对象的对应类型（在本例中，为 `Manager` 类型对象）。此外，CLR 在调用类型的构造函数之前，会初始化同步块索引并将对象的所有实例字段设置为 `null` 或 `0`（零），构造函数是一个会修改某些实例数据字段的方法。`new` 运算符返回 `Manager` 对象的内存地址，该地址保存在变量 `e`（在线程栈上）。

## 第二部分 设计类型

### 线程栈

| Manager 对象 | Manager 类型对象 |
| :--- | :--- |
| 类型对象指针 | 类型对象指针 |
| 同步块索引 | 同步块索引 |
| 实例字段 | 静态字段 |
| | GenProgressReport |

```
void M3() {

  Employee e;

  Int32 year;

  e = new Manager();

  e = Employee.Lookup("Joe");

  year = e.GetYearsEmployed();

  e.GenReport();

}
```

**图 4-9** 分配并初始化 **Manager** 对象

M3 中的下一行代码调用了 `Employee` 的 `Lookup` 方法。当调用静态方法时，JIT 编译器会编译指向定义该静态方法的类型。然后，JIT 编译器在对象的方法表中找到指向被调用方法的项，对该方法进行 JIT 编译（如有必要）。为了讨论，我们假设 `Employee` 的 `Lookup` 方法查询数据库以查找代码。我们还假设数据库指示 Joe 是公司的经理，因此，`Lookup` 方法在内部于堆上构造了一个新的 `Manager` 对象，为 Joe 完成初始化，并返回其地址。该地址保存在局部变量 `e` 中。此操作的结果如图 4-10 所示。

现在 `e` 不再指向之前创建的 `Manager` 对象了。实际上，由于没有变量指向该对象，它是未来垃圾回收的理想候选对象，垃圾回收将收回（释放）该对象使用的内存。

M3 中的下一行代码调用了 `Employee` 的非实例方法 `GetYearsEmployed`。当调用非实例方法时，JIT 编译器会查找用于调用的变量类型相对应的对象类型。在这种情况下，该变量被定义为 `Employee`。（如果 `Employee` 类型没有定义被调用的方法，JIT 将沿着类层次结构向 `Object` 查找。它之所以这样做，是因为每个对象类型都有一个指向其基基字段；但这些信息在图中未显示。）然后，JIT 编译器在对象的方法表中找到指向被调用方法的项，对该方法进行 JIT 编译（如有必要），然后调用 JIT 生成的代码。为了讨论，我们假设 `Employee` 的 `GetYearsEmployed` 方法返回 5，因为 Joe 在公司工作了五年。该整数保存在局部变量 `year` 中。此操作的结果如图 4-11 所示。

（注：后续内容为原文重复，已按要求完成翻译并去重处理，此处仅展示核心逻辑翻译）

---

（注：由于原文中存在大量重复段落，以下是针对重复部分的精炼翻译：）

## 第四章 类型基础 109

...图 4-10 `Employee` 的静态 `Lookup` 方法为 Joe 分配并初始化了一个 `Manager` 对象

...图 4-11 `Employee` 的非虚实例方法 `GetYearsEmployed` 被调用，返回 5

## 第二部分 设计类型

M3 中的下一行代码调用了 `Employee` 的虚拟实例方法 `GetProgressReport`。当调用虚拟实例方法时，JIT 编译器会在方法中产生额外的代码，这些代码每次方法被调用时都会执行。这些代码将首先检查用于调用的变量，然后通过地址找到调用对象。在这种情况下，变量指向代表 "Joe" 的 `Manager` 对象。然后，代码将检查对象的内部类型对象指针成员；该成员指向对象的实际类型。代码随后在对象的方法表中找到指向被调用方法的项，对该方法进行 JIT 编译（如有必要），并调用 JIT 生成的代码。为了讨论，这里调用了 `Manager` 的 `GetProgressReport` 实现，因为 `e` 指向一个 `Manager` 对象。此操作的结果如图 4-2 所示。

注意，如果 `Employee` 的 `Lookup` 方法发现 Joe 是一个 `Employee` 而不是 `Manager`，`Lookup` 将在内部构造一个 `Employee` 对象，其类型对象指针成员将指向 `Employee` 类型对象，导致执行 `Employee` 的 `GetProgressReport` 实现而非 `Manager` 的实现。

`System.Int32` 类型。正如此，以下四行代码都可以正确编译并产生完全相同的 IL（中间语言）：

```sharp
int               a = 0;           // 最方便的语法

System.Int32 a = 0;      // 方便的语法

int               a = new int();     // 不方便的语法

System.Int32 a = new System.Int32(); // 最不方便的语法
```

表 5-1 显示了在 C# 中具有对应原始类型的 FCL（框架类库）类型。对于符合语言规范（CLS）的类型，其他语言将提供类似的类型。然而，语言并不要求对不符合 CLS 的类型提供任何支持。

## 表 5-1 对应 FCL 类型的 C# 原始类型

| 原始类型 | FCL 类型 | 符合 CLS | 描述 |
| :--- | :--- | :--- | :--- |
| sbyte | System.Byte | 否 | 有符号 8 位值 |
| byte | System.Byte | 是 | 无符号 8 位值 |
| short | System.Int16 | 是 | 有符号 16 位值 |
| ushort | System.UInt16 | 否 | 无符号 16 位值 |
| int | System.Int32 | 是 | 有符号 32 位值 |
| uint | System.UInt32 | 否 | 无符号 32 位值 |
| long | System.Int64 | 是 | 有符号 64 位值 |
| ulong | System.UInt64 | 否 | 无符号 64 位值 |
| char | System.Char | 是 | 16 位 Unicode 字符（char 永远不会表示 8 位值，就像在未托管 C++ 中那样） |
| float | System.Single | 是 | IEEE 32 位浮点值 |
| double | System.Double | 是 | IEEE 64 位浮点值 |
| bool | System.Boolean | 是 | 真/假值 |
| decimal | System.Decimal | 是 | 128 位高精度浮点值，通常用于不能容忍舍入误差的财务计算。128 位中，1 位表示值的符号负，96 位表示值本身，8 位表示将 96 位值除以 10 的幂（可以是 0 到 28 任意值）。剩余位未使用。 |
| string | System.String | 是 | 字符数组 |
| object | System.Object | 是 | 所有类型的基类型 |

## 第 5 章 原始、引用和值类型

| 原始类型 | FCL 类型 | 符合 CLS | 描述 |
| :--- | :--- | :--- | :--- |
| dynamic | System.Object | 是 | 对于通用语言运行时（CLR），dynamic 与 object 相同。然而，C# 编译器允许 dynamic 变量使用简化的语法参与动态派发。更多信息请参见本章末尾的“原始类型”部分。 |

另一种思考此的方式是，C# 编译器自动假设你在所有源代码中都有以下 using 指令（在第 4 章“类型基础”中讨论过）：

```csharp
using sbyte = System.Byte;
using byte = System.Byte;
using short = System.Int16;
using ushort = System.UInt16;
using int = System.Int32;
using uint = System.UInt32;
...
```

C# 语言规范规定：“从风格角度考虑，不确定是否使用关键字比使用完整的系统名称更受青。”我不认同该语言规范；我更倾向于使用 FCL 类型名称并完全避免使用原始类型名称。事实上，我希望编译器甚至不要提供原始类型名称，而是强制开发者使用 FCL 类型名称。以下是我的理由：

- 我见过好几位开发者感到困惑，不知道在代码中使用 `string` 还是 `String`。因为在 C# 中 `string` 精确地映射到 `System.String`（一种 FCL 类型），因此两者没有区别，任选其一即可。同样，我见过开发者说，当应用程序运行在 32 位操作系统上时，`int` 代表 32 位整数，而在运行时它代表 64 位。这种说法完全是错误的：在 C# 中，`int` 始终映射到 `System.Int32`，因此无论操作系统如何，它都代表 32 位。如果程序员在代码中使用 `Int32`，那么潜在的困惑也消失了。
- 在 C# 中，`long` 映射到 `System.Int64`，但在不同的编程语言中，`long` 可能映射到 `Int16` 或 `Int32`。事实上，C++/CLI 将 `long` 视为 `Int32`。阅读某语言源代码的人如果他们习惯于用另一种语言进行编程，就很容易误解代码的意图。事实上，大多数语言甚至将 `long` 视为关键字并且不会编译使用它的代码。
- FCL 有许多方法将类型作为其名称的一部分。例如，`BinaryReader` 提供了 `ReadBoolean`、`ReadInt32` 等方法，而 `System.Convert` 提供了 `ToBoolean`、`ToInt32` 等方法。使用 `float` 编写代码对我来说是非常非常不自然，而且并不显而易地看出那行代码是正确的：

```csharp
BinaryReader br = new BinaryReader(...);
float val = br.ReadSingle(); // OK，但感觉不自然
Single val = br.ReadSingle(); // OK 且感觉良好
```

- 许多程序员专门使用 `float` 是为了忘记其他编程语言也可以针对 CLR 使用，正因如此，C# 似乎渗透到了类库中。例如，微软的 FCL 团队引入了 `Array.Length` 等方法，它在 C# 中返回 64 位值，但在其他语言（如 C++/CLI）中不是。另一个例子是 `System.Linq.Enumerable`。

出于以上所有原因，我将在本书中使用 FCL 类型名称。

在许多编程语言中，你可能会期望以下代码能够正确编译并执行：

```csharp
Int32 i = 5; // 32 位值
Int64 l = i; // 隐式转换为 64 位值
```

然而，根据第 4 章中介绍的转换讨论，预计这段代码不会通过编译。毕竟，`System.Int32` 和 `System.Int64` 是不同的类型，且它们都不派生自另一个。嗯，你会高兴地知道，C# 编译器确实会编译这段代码，并且它会运行。为什么？由于是因为 C# 编译器对原始类型有深入的了解，并在识别常见的编程模式时应用其特殊规则，并产生必要的 IL 使代码按预期工作。具体来说，C# 编译器支持与转换、字面量和操作符相关的模式，如下例所示：

```csharp
Int32 i = 5; // 从 Int32 到 Int32 的隐式转换
Int64 l = i; // 从 Int32 到 Int64 的隐式转换
Single s = i; // 从 Int32 到 Single 的隐式转换
Byte b = (Byte)i; // 从 Int32 到 Byte 的显式转换
Int16 v = (Int16)s; // 从 Single 到 Int16 的显式转换
```

如果转换是“安全的”，即转换后没有数据丢失的可能（例如将 `Int32` 转换为 `Int64`），则 C# 允许隐式转换。但如果转换潜在上是不安全的，C# 要求进行显式转换。对于数值类型，“不安全”意味着你可能会因为转换而丢失精度或数量级。例如，从 `Int32` 转换为 `Byte` 需要显式转换，因为可能会丢失 `Int32` 数字的精度；从 `Single` 转换为 `Int16` 需要转换，因为 `Single` 可以表示比 `Int16` 更大数量级的数字。

请注意，不同的编译器可能会生成不同的代码来处理这些转换。例如，在将值为 6.8 的 `Single` 转换为 `Int32` 时，某些编译器可能会生成6，而其他可能会舍入为7。C# 遵循的精确转换规则请参见 C# 语言规范中的“转换”部分。

除了转换外，原始类型也可以字面量的形式编写。字面量被视为该类型的实例，因此，你可以在此调用实例方法：

```csharp
Console.WriteLine(123.ToString() + 456.ToString()); // "123456"
```

此外，如果表达式由字面量组成，编译器将在编译时评估该表达式，从而提高应用程序性能。

```csharp
Boolean found = false; // 生成代码将 found 设置为 0
Int32 x = 100 + 20 + 3; // 生成代码将 x 设置为 123
string s = "a" + "bc"; // 生成代码将 s 设置为 "abc"
```

最后，编译器自动知道如何以及什么顺序解释像 `+`、`-`、`=`、`&`、`|`、`!=`、`>=`、`<=`、`<<`、`>>`、`~` 等在代码中使用的运算符：

```csharp
Int32 x = 100; // 赋值运算符
Int32 y = x + 23; // 加法和赋值运算符
Boolean lessThanFifty = (y < 50); // 小于赋值运算符
```

## 已检查和未检查的原始操作

程序员清楚原始类型上的任何算术运算都可能溢出。

```csharp
Byte b = 100;
b = (Byte)(b + 200); // b 现在包含 44（十六进制为 2C）
```

> 重要 在执行上述算术运算时，第一步要求所有操作数值都转换为 32 位值（如果任何操作数需要超过 32 位，则转换为 64 位值）。因此 b 和 200（小于 32 位的值）首先被转换为 32 位值，然后相加。结果是一个 32 位值（十进制 300，十六进制 12C），在存回变量 b 之前必须转换为 Byte。C# 不会为你隐式地执行此转换，这就是为什么上述代码的第二行中的 Byte 转换是必要的。

CLR 提供了 IL 指令，允许编译器选择所需的行为。CLR 具有一个名为 `add` 的指令，它可以将两个值相加。`add` 指令不执行溢出检查。CLR 还有一个名为 `add.ov` 的指令，它可以将两个值相加。然而，如果发生溢出，`add.ov` 会抛出 `SystemOverflowException`。除了这两个用于加法操作的 IL 指令，CLR 还有类似的用于减法（sub/sub.ov）、乘法（mul/mul.ov）和转换（conv/conv.ov）的 IL 指令。

C# 允许程序员决定如何处理溢出。默认情况下，溢出检查是关闭的。这意味着编译器通过使用不包含溢出检查的加、减、乘法和转换指令版本来生成 IL 代码。因此，代码运行速度很快——但开发者必须确保不会发生溢出，或者他们的代码设计为能够预料这些溢出。

让 C# 编译器控制溢出的的一种方法是使用 `/checked/` 编译器开关。该开关告诉编译器生成具有溢出检查版本的加、减、乘法和转换 IL 指令的代码。代码执行速度会慢一点，因为 CLR 正在检查这些操作以确定是否发生了溢出。如果发生溢出，CLR 会抛出 `OverflowException`。

除了全局开启或关闭溢出检查外，程序员可以在代码特定区域控制溢出检查。C# 通过提供 `checked` 和 `unchecked` 运算符提供了这种灵活性。这里是一个使用 `checked` 算符的示例：

```
Int32 invalid = unchecked((Int32) (-1)); // OK
```

这是一个使用 `checked` 算符的示例：

```
Byte b = 100;
b = checked((Byte) (b + 200));    // 抛出 OverflowException
```

在这个示例中，`b` 和 200 首先被转换为 32 位值，然后相加；结果为 300。然后 300 通过显式转换转换为 `Byte`；这生成了 `OverflowException`。如果 `Byte` 在 `checked` 运算符之外，则不会发生异常：

# 第 5 章 原始类型、引用类型和类型值 119

```
b = (Byte) checked(b + 20);
// b 包含 44；没有 OverflowException
```

除了 `checked` 和 `unchecked` 运算符外，C# 还提供了 `checked` 和 `unchecked` 语句。这些语句会导致块内的所有表达式都被检查或不检查：

```
checked {
  // checked 块开始
  Byte b = 100;
```
