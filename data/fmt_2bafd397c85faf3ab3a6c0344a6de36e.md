
### 基于字符串的 switch

`expression` 的求值是区分大小写的，因此只有当标签完全匹配时，`switch-section` 才会被执行。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_171_0.png)

如果 `expression` 的值与 `case` 标签中的某个常量匹配，则控制权转移到该标签之后的第一条语句。如果找不到匹配的 `case`，则控制权转移到 `default` 标签之后的第一条语句（如果存在）；否则，控制权转移到 `switch` 之后的下一条语句。

在清单 7.3 中，如果条件 `(x == 0)` 或 `(x == 1)` 评估为 `true`，则显示 `x` 的值；否则，显示 `"Invalid"`。

### 清单 7.3 一个简单的 switch 语句

```csharp
int x = 4;

switch (x)
{
    case 0:
        Console.WriteLine("x = " + x);
        break;

    case 1:
        Console.WriteLine("x = " + x);
        break;

    default:
        Console.WriteLine("Invalid");
        break;
}
```

你可能已经注意到，`case 0` 和 `case 1` 的代码是相同的。为了消除这种冗余，你可以提供一个没有中间语句的标签列表。

## 贯穿（Fall Through）

与 C 和 C++ 等其他编程语言不同，C# 中的 `switch` 语句不允许 `switch-section` 贯穿。贯穿发生在从一个 `switch-section` 开始执行并继续执行到另一个 `switch-section` 的情况中。

为了防止贯穿，C# 要求所有 `switch-section` 必须以具有不可达终点的语句结束，无条件跳转语句是其中一个例子。最常见的是 `break` 语句。

通过不允许这种贯穿行为，C# 消除了在 C 和 C++ 程序中发现的常见错误，并且允许更改 `switch-section` 的顺序而不影响语句的行为。

清单 7.4 显示了与清单 7.3 中相同的 `switch` 语句，但使用了 `case` 贯穿。因为没有中间语句，所以不违反“无贯穿规则”，控制权转移到列表中最后一个标签之后的第一条语句。

### 清单 7.4 使用 Case 贯穿的 switch 语句

```csharp
int x = 4;
switch (x)
{
    case 0:
    case 1:
        Console.WriteLine("x = " + x);
        break;

    default:
        Console.WriteLine("Invalid");
        break;
}
```

## 作用域

`switch` 语句内部的作用域由整个 `switch-block` 界定，而不是由每个 `switch-section` 界定。这意味着在 `switch-section` 内部声明的任何局部变量或常量都是整个 `switch-block` 的局部变量，而不仅仅是该 `switch-section` 的局部变量。

如果你需要将作用域限制在特定的 `switch-section` 内，你可以通过用花括号包围语句列表来创建额外的嵌套作用域。

## 试一试

### 使用 switch 语句

通过按照以下步骤操作，你可以了解 `switch` 语句的工作原理。如果你关闭了 Visual Studio，请先重复上一个练习。

- 1. 在代码编辑器中，找到名为 `buttonCheckGuess_Click` 的方法。该方法包含一个嵌套的 *if* 语句，根据 `CheckGuess` 方法的返回值确定显示哪些 *Label* 控件。
- 2. 修改 `buttonCheckGuess_Click` 方法，使其对 `CheckGuess` 方法的返回值使用 *switch* 语句，而不是嵌套的 *if* 语句。
- 3. 按 `F5` 运行应用程序。输入猜测值，并观察程序如何根据你的猜测做出响应，其结果应与上一个练习的行为完全相同。

## 迭代语句

虽然选择语句根据表达式的值执行一次语句，但迭代语句（也称为 **循环（looping）** 语句）会重复执行同一语句。迭代语句在每次通过循环的 **迭代（iteration）** 时都会对其表达式求值。**前测试循环（top-tested loop）** 在语句执行前对表达式求值，而 **后测试循环（bottom-tested loop）** 在语句执行后对表达式求值。

若要提前终止循环，而不重新评估表达式，你可以使用以下任何跳转语句：`break`、`goto`、`return` 或 `throw`。`continue` 语句将控制权传递给下一次迭代。

### while 语句

`while` 语句是一种前测试循环，它重复执行嵌入的语句，直到 `boolean-expression` 求值为 `false`。由于表达式在每次迭代前求值，因此该语句可以执行零次或多次。

`while` 语句的语法如下

```csharp
while (*boolean-expression*)
    *embedded-statement*
```

如果对 `boolean-expression` 的求值结果为 `true`，则控制权转移到 `embedded-statement`。当语句执行完毕后，控制权转移到循环的开始处，在那里重新评估表达式。

如果对 `boolean-expression` 的求值结果为 `false`，则控制权转移到 `while` 语句之后的下一条语句。如果 `boolean-expression` 的结果最初为 `false`，则 `embedded-statement` 永远不会执行。

在清单 7.5 中，循环体内的语句一直执行，直到 `i` 大于或等于 10。如果 `i++` 语句未包含在循环体中或 `boolean-expression` 中，循环将永远执行。

### 清单 7.5 while 语句

```csharp
int i = 0;
while (i < 10)
{
    Console.WriteLine(i);
    i++;
}
```

## 试一试

### 使用 while 语句

通过按照以下步骤操作，你可以了解 `while` 语句的工作原理。请在本练习结束时保持 Visual Studio 处于打开状态，因为你稍后会用到该应用程序。

- 1. 在 Visual Studio 中打开 `IterationStatements` 项目。
- 2. 右键单击 `Form1.cs` 文件并选择 **View Code** 上下文菜单选项，以此打开该文件。
- 3. 在代码编辑器中，修改 `PowersOfTwoWhileLoop` 方法，使其在 `while` 循环中执行以下语句。

```csharp
this.textBoxOutput.AppendText(String.Format("{0}^2 = {1}\r\n", i, Math.Pow(i, 2)));
i++;
```

- 4. 按 `F5` 运行应用程序。输入最大值，选择 While 单选按钮，然后单击 **Generate** 按钮。

### do 语句

`do` 语句也会重复执行嵌入的语句，直到 `boolean-expression` 求值为 `false`。与 `while` 语句不同，`do` 语句是一种 *后测试（bottom-tested）* 循环，因此在评估 `boolean-expression` 之前，`embedded-statement` 会被执行一次。这意味着它保证至少执行一次。

`do` 语句的语法如下

```csharp
do
    *embedded-statement*
while (*boolean-expression*);
```

如果布尔表达式求值结果为真，则控制权转移到循环的开头，嵌入式语句将再次执行。如果布尔表达式求值结果为假，则控制权转移到 `do` 语句之后的下一条语句。

在示例 7.6 中，如果 `i` 小于 10，循环体内的语句将会执行。与 `while` 语句一样，如果 `i++;` 语句未包含在循环体内，也未作为布尔表达式的一部分，循环将永远执行。

## 示例 7.6 do 语句

```csharp
int i = 0;
do
{
    Console.WriteLine(i);
    i++;
}
while (i < 10);
```

## 动手试一试

### 使用 do 语句

若要了解 `do` 语句的工作方式，请按照这些步骤操作。如果已关闭 Visual Studio，请先重复上一个练习。请务必保持此练习结束时 Visual Studio 处于打开状态，因为稍后您将使用此应用程序。

- 1. 在代码编辑器中，修改 `PowersOfTwoDoLoop` 方法，使其在 `do` 循环中执行以下语句：

```csharp
this.textBoxOutput.AppendText(String.Format("{0}^2 = {1}\r\n", i, Math.Pow(i, 2)));
```

- 2. 按 `F5` 运行应用程序。输入最大值，选中 Do 单选按钮，然后单击生成按钮。
- 3. 探索若从循环体中移除自增语句并将其作为 `while` 条件的一部分会发生什么。

## for 语句

`for` 语句可能是最容易被误解的迭代语句，因为它看起来最复杂；然而，它与其他迭代语句提供的基本行为相同。它也会重复执行嵌入式语句，直到指定的表达式求值结果为假。

`for` 语句的语法为

```
for ( 初始化程序 ; 条件 ; 迭代器 )
    嵌入式语句
```

`for` 语句最常用于顺序处理和遍历数组。

使 `for` 语句看起来复杂的是三个不同的表达式或部分，它们都是可选的。即使省略某一部分，每个部分也必须用分号分隔。

初始化程序可以是单个局部变量初始化，也可以是逗号分隔的局部变量初始化语句列表。在初始化程序中声明的任何局部变量的作用域仅限于条件、迭代器和嵌入式语句。

> **你知道吗？**
>
> **初始化程序声明空间**
>
> 将整个 `for` 语句视为定义在“不可见的括号”内，这些括号定义了初始化程序的局部变量声明空间。

条件必须是布尔表达式。如果省略条件，表达式默认为 `true`。

最后，迭代器可以是单个表达式，也可以是逗号分隔的表达式列表，通常用于更改在初始化程序中声明的对应局部变量。

> **注意！**
>
> **无限循环**
>
> 正如使用 `while` 语句可以创建无限循环一样，通过省略声明中的三个部分，也可以创建永久运行的 `for` 语句：
>
> ```csharp
> for ( ; ; )
> {
>     Console.WriteLine("line");
> }
> ```

再次查看示例 7.5 中的 `while` 语句，你应该会发现一些类似于 `for` 语句不同部分的元素。`while` 语句和 `for` 语句可以互换使用；`for` 语句是用更紧凑的方式编写相同代码的方法。图 7.1 展示了 `while` 语句和 `for` 语句之间的比较，这应该能让它们之间的关系变得清晰。

![图 7.1 for 语句和 while 语句的比较](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_177_0.png)

![图 7.1 for 语句和 while 语句的比较](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_177_1.png)

## 图 7.1

`for` 语句和 `while` 语句的比较

观察 `for` 语句执行时发生的事件序列，它与 `while` 语句的序列相同：

- 1. 如果存在初始化程序，则执行它。如果有多个表达式，它们将按照书写顺序执行。初始化程序在语句开始时执行一次。
- 2. 如果条件求值结果为真，控制权转移到嵌入式语句。
- 3. 执行嵌入式语句。
- 4. 如果存在，则求值迭代器中的语句，并重新评估条件。如果条件求值结果为假，控制权转移到 `for` 语句之后的下一条语句。

## 动手试一试

### 使用 for 语句

按照以下步骤，你将了解 `for` 语句的工作方式。如果已关闭 Visual Studio，请先重复上一个练习。请务必保持此练习结束时 Visual Studio 处于打开状态，因为稍后您将使用此应用程序。

- 1. 在代码编辑器中，修改 `PowersOfTwoForLoop` 方法，使其在 `for` 循环中执行以下语句：

```csharp
this.textBoxOutput.AppendText(String.Format("{0}^2 = {1}\r\n", i,
    Math.Pow(i, 2)));
```

- 2. 按 `F5` 运行应用程序。输入最大值，选中 For 单选按钮，然后单击生成按钮。
- 3. 探索若更改初始化程序和迭代器表达式会发生什么。

## foreach 语句

`foreach` 语句为数组或集合中的每个元素执行一个语句。与 `for` 语句不同，`foreach` 语句不能用于向源集合添加或移除项。

`foreach` 语句的语法为

```
foreach ( 类型 标识符 in 表达式 )
   嵌入式语句
```

如果表达式是数组类型，则执行隐式转换到 `IEnumerable`；否则，集合必须实现 `IEnumerable` 或 `IEnumerable<T>`，或者提供适当的 `GetEnumerator` 方法。

### 迭代变量

`foreach` 语句的类型和标识符是**迭代变量**，对应一个作用域仅限于嵌入式语句的只读局部变量。

随着迭代遍历集合中的元素，迭代变量代表当前元素。

`foreach` 语句是唯一不包含需求值的条件的迭代语句。嵌入式语句将继续执行集合中的所有元素，或者直到跳转语句终止循环为止。对于集合或一维数组，元素按递增顺序遍历，从索引 0 开始。如果表达式是多维数组，则按递增顺序遍历元素，从最右侧维度开始，然后是下一个左侧维度，并继续向左。

如果集合不包含任何元素，则嵌入式语句不会执行。

示例 7.7 中的代码在单独一行上显示字符串的每个字符。

## 示例 7.7 foreach 语句

```csharp
string s = "This is a test.";

foreach (char c in s)
{
    Console.WriteLine(c);
}
```

## 动手试一试

### 使用 foreach 语句

若要了解 `foreach` 语句的工作方式，请按照这些步骤操作。

- 在代码编辑器中，修改 `PowersOfTwoForEachLoop` 方法，使其在 `foreach` 循环中执行以下语句：

`this.textBoxOutput.AppendText(String.Format("{0}^2 = {1}\r\n", i, Math.Pow(i, 2)));`

- 按 `F5` 运行应用程序。输入最大值，选中 Foreach 单选按钮，然后单击生成按钮。

## 跳转语句

跳转语句与选择和迭代语句不同，因为它们无条件且立即将控制权转移到新位置，称为跳转语句的*目标*。

## goto 语句

虽然不常用，但 C# 确实提供了 `goto` 语句，该语句将控制权转移到由标签标记的语句。`goto` 语句还可以目标 `switch` 语句中的特定 `case` 或 `default` `case`。

`goto` 语句的语法为

```csharp
goto identifier;
goto case constant-expression;
goto default;
```

与 `break` 和 `continue` 语句一样，任何位于同一块中 `goto` 语句之后的语句都不会执行。

强烈建议在日常实践中避免使用 `goto` 语句，因为容易误用，并可能导致难以阅读和维护的代码。大量使用 `goto` 语句的代码通常被称为“意大利面”代码，因为程序流程与一盘意大利面的相似性。

> 顺便提一句

## break 语句

`break` 语句用于退出最近的 `switch`、`while`、`do`、`for` 或 `foreach` 语句。如果多个语句相互嵌套，则只退出最内层的语句。

清单 7.8 展示了与图 7.1 中相同的 `for` 语句，但使用了 `break` 语句，使循环在四次迭代后终止。

### 清单 7.8 break 语句

```csharp
for (int i = 0; i < 10; i++)
{
    Console.WriteLine(i);
    if (i == 3)
    {
        break;
    }
}
```

### ▼ 动手实践

#### 使用 break 语句

通过执行以下步骤，你可以看到 `break` 语句在不同迭代语句中的工作方式。请在本练习结束时保持 Visual Studio 处于打开状态，因为稍后你会用到这个应用程序。

1. 在 Visual Studio 中打开 `JumpStatements` 项目。
2. 右键单击 `Form1.cs` 文件，并选择“查看代码”上下文菜单项来打开它。
3. 在代码编辑器中，修改以下方法，以便在计算完 2 的幂之后，当循环迭代计数器等于 `breakAfter` 参数时包含一个 `break` 语句：
    - `PowersOfTwoBreakDoLoop`
    - `PowersOfTwoBreakForLoop`
    - `PowersOfTwoBreakForEachLoop`
    - `PowersOfTwoBreakWhileLoop`
4. 按 `F5` 运行应用程序。输入一个中断迭代值，选择一个单选按钮，并单击 Generate（生成）按钮。
5. 更改 `break` 语句的位置，使其发生在计算 2 的幂之前。
6. 再次按 `F5` 运行应用程序。输入一个中断迭代值，选择一个单选按钮，并单击 Generate（生成）按钮。你应该会注意到，对于在第 4 步中选择的相同迭代语句和中断迭代值，输出是不同的。

## continue 语句
