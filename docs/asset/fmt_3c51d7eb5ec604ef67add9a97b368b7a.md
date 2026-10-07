
```csharp
greenLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Green);
}

private void blueLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Blue);
}

private void indigoLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Indigo);
}

private void violetLabel_Click(object sender, EventArgs e)
{
    DisplayColor(Spectrum.Violet);
}
```

# 获取枚举器或枚举变量的整数值

你不能直接将枚举器赋值给 `int` 变量，但可以使用强制转换运算符将枚举器转换为底层整数类型。这是一个示例：

```csharp
int value = (int)Day.Friday;
```

该语句声明了一个名为 `value` 的 `int` 变量，并用 `Day.Friday` 的整数值对其初始化。执行该语句后，`value` 将等于 5。这是另一个示例：

```csharp
Day workDay = Day.Monday;
int value = (int)workDay;
```

第一个语句声明了一个名为 `workDay` 的 `Day` 变量，用 `Day.Monday` 进行初始化。第二个语句声明了一个名为 `value` 的 `int` 变量，并用变量 `workDay` 的整数值对其初始化。执行该语句后，`value` 将等于 1。

# 为枚举器指定整数值

默认情况下，枚举数据类型中的枚举器被赋值整数 0、1、2 等。如果不合适，可以指定赋值的值，如下例：

```csharp
enum Water { Freezing = 2, Boiling = 1 }
```

在此示例中，`Water.Freezing` 枚举被赋值整数值 2，`Water.Boiling` 被赋值整数值 1。

分配枚举的整数值不需要是唯一的。例如，以下代码显示了一个名为 `MonthDays` 的枚举。它的枚举是 January、February、March 等。注意赋值给枚举的值是月份的天数（January 有 31 天，February 有 28 天等）。此数据类型可能用于每个月份的天数。

```csharp
enum MonthDays
{January = 31, February = 28, March = 31,
    April = 30, May = 31, June = 30,
    July = 31, August = 31, September = 30,
    October = 31, November = 30, December = 31}
```

# 比较枚举器和枚举变量

之前你看到可以使用相等运算符 `==` 比较枚举器和枚举变量。你还可以使用关系运算符来比较它们。例如，使用 `Day` 类型，以下表达式为真：

```csharp
Day.Friday > Day.Monday
```

该表达式为真，因为枚举器 `Day.Friday` 在内存中存储为 5，而枚举器 `Day.Monday` 存储为 1。以下代码显示“Friday大于 Monday”。

```csharp
if (Day.Friday > Day.Monday)
    MessageBox.Show("Friday is greater than Monday.");
```

以下代码显示了比较两个枚举变量的示例：

```csharp
Day day1 = Day.Friday;
Day day2 = Day.Monday;
if (day1 > day2)
    MessageBox.Show(day1 + " is greater than " + day2);
```

枚举器和枚举变量可以直接与整数值进行比较。例如，以下代码显示“Sunday等于0”。

```csharp
if (Day.Sunday == 0)
    MessageBox.Show("Sunday is equal to zero.");
```

# 使用枚举变量遍历数组

由于枚举器表示整数值，因此可以在循环中遍历数组元素。例如，查看以下代码：

```csharp
decimal[] sales = {1000, 2000, 3000, 4000,
    5000, 6000, 7000};
for (Day dayCount = Day.Sunday; dayCount <= Day.Saturday; dayCount++)
{
    MessageBox.Show("Sales for " + dayCount + " were " + sales[(int)dayCount].ToString("c"));
}
```

第1行和第2行创建了一个名为 `sales` 的 `decimal` 数组。第4行开始 `for` 循环使用枚举变量 `dayCount` 作为计数器。注意关于该循环的以下点：

- `dayCount` 变量初始化为 `Day.Sunday`。
- 只要 `dayCount` 小于等于 `Day.Saturday`，循环就会继续。
- 在每次迭代结束时，`dayCount` 会加1。

在第7行，表达式 `(int) dayCount` 被数组下标。随着循环执行，它显示以下消息：

- "Sales for Sunday were $1,00.00"
- "Sales for Monday were $2000.00"
- "Sales for Tuesday were $3000.00"
- "Sales for Wednesday were $4000.00"
- "Sales for Thursday were $5000.00"
- "Sales for Friday were $6000.00"
- "Sales for Saturday were $7000.00"

# 检查

## 9.17 查看以下声明：

```csharp
enum Flower { Rose, Daisy, Petunia }
```

a. 数据类型的名称是什么？
b. 在内存中，枚举器 `Flower.Rose` 存储什么值？`Flower.Daisy` 呢？`Flower.Petunia` 呢？
c. 写一个语句声明此枚举类型的变量。变量名应为 `flora`。用 `Flower.Petunia` 枚举初始化该变量。

**9.18** 你使用什么方法来显示枚举器的字符串值？

**9.19** 如何获取枚举器的整数值？

# 9.5 字典

## 概念

字典是一个存储数据集合的对象。字典中的每个元素都有两个部分：键 `key` 和值 `value`。每个键与一个特定的值关联，并用于定位该值。

当你听到“字典”这个词时，你可能会想到像韦氏词典》这样的大书，它包含了单词及其定义。如果你想知道某个单词的含义，可以在字典中找到它并查看其定义。

在编程中，字典是一个存储数据集合的对象。存储在字典中的每个元素都有两个部分：键和值。事实上，字典元素通常被称为“键值对”。当你想要从字典中检索特定值时，使用与该值关联的键。这与在《韦氏词典》中查找单词的过程相似，其中单词是键，定义是值。

例如，假设公司中的每个员工都有一个 ID 号，我们编写一个程序，通过输入员工 ID 来查找员工姓名。我们可以创建一个字典，其中每个元素包含员工 ID 作为键以及该员工姓名作为值。这如图 9-15 所示。如果我们将知道员工的 ID 号，我们就可以检索该员工的名字。

**图 9-15** 键值对

| 键 Keys | 值 Values |
|---|---|
| 101 | "Chris Jones" |
| 102 | "Jessica Smith" |
| 103 | "Amanda Stevens" |
| 104 | "Will Osborn" |

另一个示例是一个允许我们输入姓名并返回该人员电话号码的程序。程序可以使用字典，其中每个元素包含一个姓名作为键 `key`，并将其电话号码作为值 `value`。如果我们知道一个人的名字，就可以检索他的电话号码。

## Dictionary 类

.NET Framework 提供了一个 `Dictionary` 类，你可以用它在程序中实现字典容器。`Dictionary` 类提供了许多方法用于存储元素、检索元素、删除元素、遍历字典等。

要使用 `Dictionary` 类，你需要在程序中使用以下 `using` 语句：

```csharp
using System.Collections.Generic;
```

然后，你就可以声明一个 `Dictionary` 对象。这里是通用格式：

```csharp
Dictionary<KeyType, ValueType> DName = new Dictionary<KeyType, ValueType>();
```

其中：

- `KeyType` 是每个元素之键的数据类型
- `ValueType` 是每个元素的值的数据类型
- `DName` 是 `Dictionary` 的名称

下面是一个示例，展示了如何声明一个 `Dictionary` 来存储员工 ID 号（作为 `int` 类型）及其对应的员工姓名（作为 类型）：

```csharp
Dictionary<int, string> employees = new Dictionary<int, string>();
```

此语句声明了一个名为 `employees` 的 `Dictionary`。在尖括号 `<>` 中，第一个数据类型 `int` 是每个键的类型，在这种情况下，它们是员工 ID 号。第二个数据类型 `string` 是对应值的类型，在这种情况下，它们是员工姓名。因此，此 `Dictionary` 的每个元素都是一个键值对，其中键是 `int`，值是 `string`。

如果你在方法内部局部声明 `Dictionary` 变量，可以使用 `var` 关键字来简化声明，如下所示：

```csharp
var employees = new Dictionary<int, string>();
```

`Dictionary` 中的键必须是唯一的。`Dictionary` 中没有两个元素可以具有相同的键值。

## 初始化字典

你可以使用初始化列表来初始化 `Dictionary`。下面的代码显示了一个示例：

```csharp
Dictionary<int, string> employees = new Dictionary<int, string>(
{
    {101, "Chris Jones"},
    {102, "Jessica Smith"},
    {103, "Amanda Stevens"},
    {104, "Will Osborn"}
});
```

此代码创建了一个名为 `employees` 的 `Dictionary`，并对其如下初始化：

- 第一个元素是 `{101, "Chris Jones"}`。在该元素中，101 是键，"Chris Jones" 是值。
- 第二个元素是 `{102, "Jessica Smith"}`。在该元素中，102 是键，"Jessica Smith" 是值。
- 第三个元素是 `{103, "Amanda Stevens"}`。在该元素中，103 是键，"Amanda Stevens" 是值。
- 第四个元素是 `{104, "Will Osborn"}`。在该元素中，104 是键，"Will Osborn" 是值。

注意初始化列表的以下几个方面：

- 初始化列表包含在一对大括号 `{}` 中；
- 每个元素都包含在自己的大括号中，键和值之间用逗号分隔；
- 元素之间用逗号分隔；
- 在最后一个大括号之后，声明以分号结束。

如前所述，`Dictionary` 中的键必须是唯一的。如果初始化列表中的两个或多个元素具有相同的键，运行时将抛出异常。

## 向现有字典添加元素

你可以使用以下通用格式的赋值语句向 `Dictionary` 中添加元素：

```csharp
dictionaryName[key] = value;
```

在通用格式中，`dictionaryName` 是 `Dictionary` 的名称，`key` 是一个键。如果键已存在于 `Dictionary` 中，其关联的值将被更改为 `value`。如果键不存在，它将被添加到 `Dictionary`，并将 `value` 作为其关联值。下面的代码显示了一个示例：

```csharp
Dictionary<int, string> employees = new Dictionary<int, string>();
employees[110] = "Beth Young";
employees[111] = "Jake Brown";
employees[112] = "Emily Davis";
```

第一条语句创建一个名为 `employees` 的空 `Dictionary`。随后的语句向 `Dictionary` 中添加了以下元素：

- Key = 110, Value = "Beth Young"
- Key = 111, Value = "Jake Brown"
- Key = 112, Value = "Emily Davis"

记住 `Dictionary` 中的键必须是唯一的。如果你为现有键分配一个新值，新值将替换之前存储的值。例如，请看下面的代码：

```csharp
Dictionary<int, string> employees = new Dictionary<int, string>();
employees[110] = "Beth Young";
employees[110] = "Jake Brown";
```

第一条语句创建一个名为 `employees` 的空 `Dictionary`。第二条语句将 "Beth Young" 分配给键 110。第三条语句将 "Jake Brown" 分配给键 110。

## 使用 Add 方法添加元素

除了使用 `[]` 运算符外，你还可以使用以下通用格式的 `Add` 方法向 `Dictionary` 添加元素：

```csharp
dictionaryName.Add(key, value);
```

在通用格式中，`dictionaryName` 是 `Dictionary` 的名称，`key` 是一个键。如果键已存在于 `Dictionary` 中，则会抛出异常。如果键不存在，它将被添加到 `Dictionary`，并将 `value` 作为其关联值。下面的代码显示了一个示例：

```csharp
Dictionary<int, string> employees = new Dictionary<int, string>();
employees.Add(110, "Beth Young");
employees.Add(111, "Jake Brown");
employees.Add(112, "Emily Davis");
```

第一条语句创建一个名为 `employees` 的空 `Dictionary`。随后的语句向 `Dictionary` 中添加了以下元素：

- Key = 110, Value = "Beth Young"
- Key = 111, Value = "Jake Brown"
- Key = 112, Value = "Emily Davis"

## 从 Dictionary 中检索值

要从 `Dictionary` 中检索值，你可以使用以下表达式：

```csharp
value = dictionaryName[key];
```

在通用格式中，`dictionaryName` 是 `Dictionary` 的名称，`key` 是一个键。如果键存在于 `Dictionary` 中，它将返回与键关联的值。如果键不存在，将抛出异常。下面的代码片段演示了这一点：

```csharp
Dictionary<int, string> employees = new Dictionary<int, string>();
employees[101] = "Chris Jones";
employees[102] = "Jessica Smith";
employees[103] = "Amanda Stevens";
employees[104] = "Will Osborn";

// 显示元素
for (int key = 101; key <= 104; key++)
{
    employeesListBox.Items.Add(employees[key]);
}
```

## 从 Dictionary 中删除元素

你可以使用 `Remove` 方法从 `Dictionary` 中删除元素。调用 `Remove` 方法时传递要删除元素的键。下面的代码显示了一个示例：

```csharp
Dictionary<int, string> employees = new Dictionary<int, string>();
employees[101] = "Chris Jones";
employees[102] = "Jessica Smith";
employees[103] = "Amanda Stevens";
employees[104] = "Will Osborn";

// 删除 ID 为 102 的员工。
```
