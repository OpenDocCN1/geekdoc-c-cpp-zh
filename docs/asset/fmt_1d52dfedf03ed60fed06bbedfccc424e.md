
- 你只能使用字母（大写和小写）、数字和下划线字符。

- 标识符必须以字母或下划线开头。

例如，`result`、`_score_`、`footballTeam` 和 `plan9` 都是有效的标识符，而 `result%`、`footballTeam$` 和 `9plan` 则不是。

> **重要**

`C#` 是一种区分大小写的语言。例如，`footballTeam` 和 `FootballTeam` 是两个不同的标识符。

### 识别关键字

`C#` 预留了 77 个标识符供自身使用。你不能将这些标识符用于你自己的目的。这些标识符被称为关键字，每个关键字都有特定的含义。关键字的示例包括 `class`、`namespace` 和 `using`。随着本书学习的进行，你将学习到大多数 `C#` 关键字的含义。以下是关键字列表：

| abstract | do | in | protected | true |

|---|---|---|---|---|

| as | double | int | public | try |

| base | else | interface | readonly | typeof |

| bool | enum | internal | ref | uint |

| break | event | is | return | ulong |

| byte | explicit | lock | sbyte | unchecked |

| case | extern | long | sealed | unsafe |

| catch | false | namespace | short | ushort |

| char | finally | new | sizeof | using |

| checked | fixed | null | stackalloc | virtual |

| class | float | object | static | void |

| const | for | operator | string | volatile |

| continue | foreach | out | struct | while |

| decimal | goto | override | switch |

| default | if | params | this |

| delegate | implicit | private | throw |

> ### 提示

在 `Visual Studio 2022` 代码和文本编辑器窗口中，当你输入关键字时，它们会显示为蓝色。

`C#` 还使用了以下标识符。这些标识符没有被 `C#` 预留，这意味着你可以将这些名称作为你自己的方法、变量和类的标识符，但如果可能，你应该避免这样做，因为这可能会给试图理解和维护你代码的其他开发者带来困惑。

| add | global | select |

| alias | group | remove |

| and | into | set |

| ascending | join | value |

| async | let | var |

| await | typeof | when |

| descending | not | where |

| dynamic | or | yield |

| from | orderby | |

| get | partial | |

### 使用变量

变量是存储值的存储位置。你可以将变量想象成计算机内存中的一个盒子，用于存放临时信息。你必须为程序中的每个变量提供一个无歧义的名称，以便在所使用的上下文中唯一地标识它。

你使用变量名来引用它所持有的值。例如，如果你想存储商店中某个物品的成本，你可以创建一个名为 `cost` 的变量，并将物品成本存储在该变量中。稍后，如果你引用 `cost` 变量，获取到的值将是你存储的物品成本。

### 变量命名

你应该为变量采用命名规范，以帮助避免对你定义的变量产生困惑。如果你正参与一个由多个开发者负责不同部分的项目，这一点尤尤为重要。一致的命名规范有助于避免混淆并减少错误。以下列表包含了一些建议：

- 不要以下划线作为标识符开头。虽然这在 `C#` 中是合法的，但可能会限制你的代码与其他语言（如 Visual Basic）的互操作性。

- 不要创建仅大小写上不同的标识符。例如，不要创建一个名为 `myFunction` 的变量和另一个名为 `MyVariable` 的变量，因为它们很容易被混淆。

- 以小写字母开头名称。

- 在多单词标识符中，第二个及后续单词以大写字母开头（这被称为驼峰命名法）。

- 不要使用匈牙命名法（如果你是 `C++` 开发者，你可能熟悉匈牙命名法。如果你不知道它是什么，不用担心！）。

例如，`score`、`_score` 和 `FootballTeam` 都是有效的，但推荐第一个。

### 声明变量

变量持有值。`C#` 有许多可以存储和处理的不同值类型：整数、浮点数和字符串。当你声明变量时，必须指定它将包含的数据类型。始终，你必须用分号结束语句。

```int age;
```

> 注意

如果你是 Visual Basic 程序员，你应该注意，`C#` 不允许隐式声明。你必须在使用所有变量之前显式地声明它们。

在声明变量之后，你可以给它赋值。接下来的语句将将值 `42` 赋值给该变量。等号 (`=`) 是赋值运算符，它将右侧的值赋值给左侧的变量。赋值之后，你就可以在代码中使用 `age` 变量来引用它持有的值。如果你将鼠标指针悬停在 `Visual Studio 2022` 代码和文本编辑器窗口中的变量上，屏幕提示（ScreenTip）会指示变量的类型。下一个语句将 `age` 变量的值（`42`）写入控制台：

```csharp
Console.WriteLine(age);
```

### 指定数值值

理解变量类型对变量可以持有的数据的影响以及如何处理这些数据至关重要。例如，显而易见，数值变量不能持有如“Hello”之类的字符串值。然而，在某些情况下，赋值给变量的值类型并不总是明确的。

以字面量值 `42` 为例。它是数值且整数。但如果你尝试将此值赋值给非整数类型（例如浮点变量）会发生什么？答案是 `C#` 将把整数值转换为浮点值。这样做是无害的，但并不总是好的做法。你可以通过在字面量后添加后缀来指定将 `42` 是浮点数：

```csharp
// = 42F;
```

赋值之后，你就可以在代码中使用 `age` 变量来引用它所持有的值。如果你将鼠标指针悬停在 `Visual Studio 2022` 代码和文本编辑器窗口中的变量上，屏幕提示会指示变量的类型。下一个语句将 `age` 变量的值（`42`）写入控制台：

```csharp
Console.WriteLine(age);
```

那么 `0.42`? 这个表达式的类型是什么？答案是，像包含小数点的字面量一样，它实际上是一个双精度变量。在下一节中，你会看到 `double` 的范围更大，精度更高。如果你想将 `0.42` 赋值给 `float`，必须应用 `F` 后缀（`C#` 编译器强制要求）：

```csharp
```

`C#` 还有其他数值类型：范围更大的长整数，以及小数。（虽然 `float` 和 `double` 持有精确的小数值，但在涉及计算时会受到舍入和其他近似。）你应该使用 `L` 后缀将字面量值赋值给长整数，并使用 `M` 后缀将字面量值赋值给小数。

这似乎是一个微不足道的点，但通过无意中给变量赋值错误类型的值，程序中产生多少微妙错误是令人惊讶的。考虑如果你尝试执行涉及大量有效小数位的计算并将结果存储在 `float` 中会发生什么。在最的情况下，这会导致数据截断，引起计算错误。例如，如果你的程序是空间探测器的引导应用程序，此类错误可能会导致它完全错过火星，转而向太阳系统的深处去！

### 使用原始数据类型

`C#` 的数值类型，以及用于字符串、字符和布尔值的其他常用类型，统称为原始数据类型。下表列出了最常用的原始数据类型以及每个类型可以存储的值的范围：

| 数据类型 | 说明 | 大小（位） | 范围 | 示例用法 |

| --- | --- | --- | --- | --- |

| int | 整数 | 32 | -2³¹ 到 2³¹ - 1 | `int count = 42` |

| long | 整数（范围更大） | 64 | -2⁶³ 到 2⁶³ - 1 | `long wait = 42L` |

| float | 浮点数 | 32 | -3.4 x 10³⁸ 到 3.4 x 10³⁸ | `float away; away = 0.42F;` |

| 数据类型 | 描述 | 大小 (位) | 范围 | 示例用法 |

|---|---|---|---|---|

| double | 双精度（更精确）浮点数 | 64 | ±5.0 x 10³324 至 ±1.7 x 10³308 | `double trouble; trouble = 0.42;` |

| decimal | 货币数值 | 128 | 28 位有效数字 | `decimal coin; coin = 0.42M;` |

| string | 字符序列 | 每个字符16 位 | 不适用 | `string vest; vest = "forty two";` |

| char | 单字符 | 16 | 单个字符 | `char grill; grill = 'x';` |

| bool | 布尔值 | 8 | true 或 false | `boolean teeth; teeth = false;` |

### 未赋值的局部变量

当你声明一个变量时，在给它赋值之前，它包含一个随机值。这种行为在 `C` 和 `C++` 程序中是 Bug 的常见根源，因为程序创建了一个变量，但在赋值之前就不小心将其作为信息源使用。

`C#` 不允许使用未赋值的变量。你必须在使用变量之前对其进行赋值；否则，程序将无法编译。这一要求被称为**确定赋值规则**（definite assignment rule）。例如，以下语句会生成编译错误信息：“使用未赋值的局部变量 'age'，因为 `Console.WriteLine` 语句尝试显示未初始化变量的值：

点击此处查看代码图像

```
int age;
Console.WriteLine(age); // 编译错误
```

### 显示原始数据类型的值

在接下来的练习中，你将使用名为 `PrimitiveDataTypes` 的 `C#` 程序来演示几种原始数据类型是如何工作的。

### 如何显示原始数据类型的值

- 1. 如果 `Visual Studio 2022` 已经在运行，在“文件”（File）菜单上，选择“打开”（Open），然后选择“项目/解决方案”（Project/Solution）。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_115_0.png)

- 如果 `Visual Studio 2022` 没有运行，请启动它，然后选择“打开项目或解决方案”（Open a project or solution）。

“打开项目”对话框打开了。

- 2. 导航到**文档**（Documents）文件夹中的 **Microsoft Press\VCSBS\Chapter 2\PrimitiveDataTypes** 文件夹。

- 3. 选择 **PrimitiveDataTypes** 解决方案文件，然后选择**打开**（Open）。

解决方案加载，解决方案管理器显示 `PrimitiveDataTypes` 项目。

> 注意

> 解决方案名称具有 `.sln` 后缀，例如 `PrimitiveDataTypes.sln`。一个解决方案可以包含一个或多个项目。Visual C# 项目文件具有 `.csproj` 后缀。如果你打开的是项目而不是解决方案，`Visual Studio 2022` 会自动为它创建一个新的解决方案文件。

如果你不知道此功能，可能会可能会很困惑，因为可能会导致你不意地为同一个项目生成多个解决方案。

- 4. 在“调试”（Debug）菜单上，选择“开始调试”（Start Debugging）。这使得应用程序比简单运行运行时更容易捕获和报告错误。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_117_0.png)

- 5. 在“选择数据类型”（Choose a data type）列表中，选择 **string**。

文本 *forty-two* 出现在示例值框中。

- 6. 在“选择数据类型”（Choose a data type）列表中，选择 **int**。

文本 *do* 出现在示例值框中，表示显示 *int* 值的语句仍需编写。

- 7. 选择列表中的每个数据类型。确认 **double** 和 **bool** 类型的代码尚未实现；应用程序显示的结果为 *to*。

- 8. 返回 `Visual Studio 2022`，然后在“调试”（Debug）菜单上选择“停止调试”（Stop Debugging）。或者，关闭窗口以停止调试。

### 如何在代码中使用原始数据类型

- 1. 在解决方案管理器中，展开 `PrimitiveDataTypes` 项目（如果它尚未展开），然后双击 `MainPage.xaml`。

应用程序显示在设计视图窗口中。

> 提示

> 如果你的屏幕不够大以显示整个表单，可以通过按 `Ctrl+Alt=+` 和 `Ctrl+Alt−` 在设计视图窗口中放大或缩小，或者通过设计视图窗口左下角的缩放下拉列表中选择尺寸。

- 2. 在 `XAML`窗格中，向下滚动找到 `ListBox` 控件的标记。该控件在表单左侧显示数据类型列表。它看起来如下（为了可读性，已从文本中删除某些属性）：

点击此处查看代码图像

```
<ListBox x:Name="type" ...
SelectionChanged="typeSelectionChanged">
  <ListBox>int</ListBox>
  <ListBox>long</ListBox>
  <ListBox>float</ListBox>
  <ListBox>double</ListBox>
  <ListBox>decimal</ListBox>
  <ListBox>string</ListBox>
  <ListBox>char</ListBox>
  <ListBox>bool</ListBox>
</ListBox>
```

`ListBox` 控件将每个数据类型显示为独立的 `ListBoxItem`。当应用程序运行时，如果用户选择列表中的项，就会发生 `SelectionChanged` 事件（这类似于第一章中用户选择按钮时发生的 `Click` 事件）。在这种情况下，`ListBox` 调用 `typeSelection` 方法。该方法定义在 `MainPage.xaml` 文件中。

- 在“视图”（View）菜单上，选择“代码”（Code）。

代码编辑器打开，显示 `MainPage.xaml` 文件。

> 注意

> 你也可以使用解决方案管理器访问代码。选择 `MainPage.xaml` 文件左侧的箭头展开节点，然后双击 `MainPage.xaml.cs`。

- 在代码编辑器中，找到 `typeSelectionChanged` 方法。

要在项目中查找项，打开“编辑”（Edit）菜单，选择“查找替换”（Find And Replace），然后选择“快速查找”（Quick Find）。快捷菜单在代码编辑器窗口的右上角打开。在快捷菜单的文本框中，输入要查找的项目名称，然后选择“查找下一个”（文本框旁的右箭头符号）。

5.向下滚动代码并找到 `showFloatValue` 方法，它看起来如下：

点击此处查看代码图像

```csharp
private void showFloatValue()
{
    float floatVar;
    floatVar = 0.42F;
    value.Text = floatVar.ToString();
}
```

该方法的体包含三个语句。

- 第一条语句声明了一个名为 `floatVar` 的类型为 `float` 的变量。

- 第二条语句为 `floatVar` 赋值值 `0.42F`。

> 请记住，`F` 类型后缀表示 `0.42` 应被视为 `float` 值。如果你忘记了 `F`，则值 `0.42` 将被视为 `double` 类型，你的程序将无法编译，因为在不编写额外代码的情况下，你无法将一种类型的值赋值给不同类型的变量。`C#` 在这方面非常严格。

- 第三个语句在表单的文本框中显示该变量的值。这条语句需要你注意。如第 1 章所示，在框中显示项目的方法是设置其 `Text` 属性（在第 1 章中是通过使用 `XAML` 实现的）。你也可以通过编程方式执行此任务，这正是这里正在发生的。注意，你通过使用运行方法时看到的点符号语法来访问对象的属性。（还记得第 1 章的 `Console.WriteLine` 吗？）此外，你放入属性中的数据必须是字符串而不是数字。如果你尝试将数字赋值给 `Text` 属性，你的程序将无法编译。幸运的是，`.NET` 库通过 `ToString` 方法提供了一些帮助。

`.NET` 库中的每种数据类型都有 `ToString` 方法。`ToString` 的目的是将对象转换为其字符串表示。`showFloatValue` 方法使用 `float` 变量 `floatVar` 的 `ToString` 方法生成该变量值的字符串版本。你可以安全地将此字符串赋值给 `value`框的 `Text` 属性。当你创建自己的数据类型和类时，你可以定义 `ToString` 方法的自己的实现，以指定你的类如何表示为字符串。你将在第 7 章“创建和管理类与对象”中学习更多内容。

6. 在代码和文本编辑器窗口中，找到 `showIntValue` 方法：

点击此处查看代码图像

```csharp
private void showIntValue()
{
    value.Text = "to do";
}
```

当你在列表框中选择 `int` 类型时，会调用 `showIntValue` 方法。

7. 在 `showIntValue` 方法的开头，即大括号之后的新行，添加以下**加粗**的两个语句：

点击此处查看代码图像

```csharp
private void showIntValue()
{
    int intVar;
    intVar = 42;
    value.Text = "to do";
}
```
