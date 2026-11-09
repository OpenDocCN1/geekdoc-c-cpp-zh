
现在我们来学习匿名类型在查询中的使用。

## 在查询中使用匿名类型

LINQ 中的匿名类型提供了一种便捷方式，可将一组只读属性组合成要包含在查询结果中的元素。无需为这些属性定义类型，因为类型由编译器定义。这些类型使你无需编写类定义即可创建类的对象。此类类没有名称，因此称为匿名类型；匿名类型使你能够在查询中以任意顺序选择可用字段的任意组合，而无需为任何元素定义具名数据类型。

编译器动态构造匿名类型并为其分配名称。每次生成应用程序时名称都会变化；因此，不能在应用程序中直接使用匿名类型的名称。

LINQ 中的匿名类型用于查询表达式，以组合查询所选的数据列。它们使你能够编写选择任意数量列且可按任意顺序选择列的查询。

执行以下步骤以在 LINQ 查询中使用匿名类型：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏*选择* **文件→新建→项目**。“新建项目”对话框打开。
- 3. 在“新建项目”对话框左窗格的“已安装的模板”部分中*选择* **Visual C#→Windows**。右窗格中显示可用于在 C# 中开发基于 Windows 的应用程序的项目模板。
- 4. 在右窗格中*选择*“Windows 窗体应用程序”模板，以创建 Windows 窗体应用程序。
- 5. 在“名称”文本框中*输入*应用程序名称 **AnonymousTypes**（也随 CD 提供），并在“位置”组合框中为应用程序选择合适位置。
- 6. *单击*“确定”按钮关闭“新建项目”对话框。**AnonymousTypes** 应用程序即创建完成（图 C#-6.41）。
- 7. 从工具箱*拖放*一个 **ListView** 控件到窗体上。
- 8. 在窗体中选择 **ListView** 控件，并单击该控件右上角的右箭头按钮，以*打开* **ListView** 控件的智能标记（图 C#-6.45）。
- 9. 在 ListView 控件的智能标记中，*单击*“视图”下拉列表的下箭头按钮，然后从下拉列表中选择“平铺”选项，如图 C#-6.45 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_438_0.png)

图 C#-6.45

- 10. 单击 ListView 控件智能标记中的 **在父容器中停靠** 链接，以将 ListView 控件停靠在其父容器（窗体）中，如图 C#-6.46 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_439_0.png)

图 C#-6.46

- 11. *双击* Form1 打开代码编辑器，并在代码编辑器中*添加*清单 6.20 给出的突出显示代码：

### 清单 6.20：演示在 LINQ 查询中使用匿名类型

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    string[] words = {"APPLE", "BlueBERRY", "cHeRrY", "baNaNa", "MANGO", "PEACH",
                      "StrawBERRY"};
    var twoWords = from w in words
                   select new
                   {
                       Upper = w.ToUpper(),
                       Lower = w.ToLower()
                   };
    foreach (var upperLower in twoWords)
    {
        listView1.Items.Add(upperLower.Upper + "<-->" + upperLower.Lower);
    }
}
```

在前面的代码中，匿名类型有两个成员 **Upper** 和 **Lower**，分别存储字符串类型数组 words 的大写版本和小写版本。

- 12. *按*键盘上的 F5 键运行应用程序。应用程序的输出如图 C#-6.47 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_440_0.png)

图 C#-6.47

现在我们来学习 Lambda 表达式在 LINQ 查询中的使用。

## 在查询中使用 Lambda 表达式

Lambda 表达式是一种没有名称的函数，用于计算并返回单个值。它同时定义并执行。Lambda 表达式使用 lambda 运算符 =>，读作 **转到**。lambda 运算符的左侧指定输入参数，右侧指定表达式或语句，如下所示：

```text
(input parameter) => expression
```

如果 Lambda 表达式只有一个参数，则括号是可选的。但是，如果参数多于一个，则括号是必需的，在这种情况下，用逗号（,）分隔参数。使用 Lambda 表达式时，无需在声明中添加变量，因为编译器会添加它。

LINQ 中的 Lambda 表达式是使用 LINQ 中许多标准查询运算符的基础。编译器会创建 Lambda 表达式，以处理查询中定义的计算，例如 **Where**、**Select** 和 **OrderBy**。Lambda 表达式的用法与标准函数类似，区别在于它：

- 没有名称
- 不能具有修饰符，例如 **Overloads** 或 **Overrides**
- 不使用 **As** 子句来指定表示 Lambda 表达式的函数的返回类型
- 其主体是表达式而不是语句
- 没有 **return** 语句；函数返回的值是函数主体中表达式的值
- 不接受泛型参数

执行以下步骤以在 LINQ 查询中使用 Lambda 表达式：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏*选择* **文件→新建→项目**。**新建项目**对话框打开。
- 3. 在**新建项目**对话框左窗格的**已安装的模板**部分中*选择* **Visual C#→Windows**。**新建项目**对话框的右窗格中显示可用于在 C# 中开发**基于 Windows 的应用程序**的项目模板。
- 4. 在右窗格中*选择* **Windows 窗体应用程序**模板，以创建 Windows 窗体应用程序。
- 5. 在“名称”文本框中*输入*应用程序名称 **LambdaExpression**（也随 CD 提供），并在“位置”组合框中为应用程序选择合适位置。
- 6. *单击* **确定**按钮关闭**新建项目**对话框。**LambdaExpression** 应用程序即创建完成（图 C#-6.48）。
- 7. 从工具箱*拖放*两个 TextBox 控件、两个 Label 控件和一个 Button 控件到窗体上。
- 8. 将第一个和第二个 Label 控件的 Text 属性分别更改为“输入姓名的第一个字符：”和“结果”，并将 Button 控件的 Text 属性更改为“Click”，如图 C#-6.48 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_441_0.png)

- 9. 双击 Click 按钮，并在代码编辑器中添加清单 6.21 给出的突出显示代码。

### 清单 6.21：演示 Button1 控件的 Click 事件代码

```csharp
private void button1_Click(object sender, EventArgs e)
{
    textBox2.Text = "";
    string[] arrNames = { "Avantika", "Priya", "Ira", "Jaya",
                          "Amrita", "Puja" };
    foreach (var Name in arrNames.Where(n => n.StartsWith(textBox1.Text)))
    {
        textBox2.Text = (textBox2.Text + Name) + ",";
    }
}
```

在清单 6.21 中，定义了一个字符串数组 arrNames，并向其中添加了一些名称。我们还在 foreach 循环中创建了一个 Lambda 表达式，该表达式在 textBox2 中显示所有以 textBox1 中所输入文本开头的名称。

- 10. 按键盘上的 F5 键执行 LambdaExpression 应用程序，并在 textBox1 中输入一些文本。在我们的示例中，在 textBox1 中输入了字母 A，如图 C#-6.49 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_441_1.png)

- 11. 单击 Click 按钮。以 textBox1 中所输入字母开头的名称显示在 textBox2 中，如图 C#-6.50 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_442_0.png)

> 应注意，在 textBox1 中输入的值区分大小写。这意味着，如果在 textBox1 中输入任何小写值，则 textBox2 中不会返回任何值。这是因为输入字符串中的所有值都以大写单词开头。

应注意，如果在 textBox1 中未输入任何值就单击 Click 按钮，则输入字符串中的所有值都会返回在 textBox2 中。

现在我们来学习 PLINQ。

## 探索 PLINQ

PLINQ 是 LINQ 模式的并行实现，旨在使用系统中存在的所有处理器。用 PLINQ 设计的查询在语法上与 LINQ to Objects 查询非常相似。例如，考虑以下简单的 LINQ to Objects 查询：

```csharp
var output = from x in source
             where (some condition)
             select (something)
```

现在，考虑以下 PLINQ 查询：

```csharp
var output = from x in source.AsParallel()
             where (some condition)
             select(something)
```

请注意，前面的 PLINQ 查询与 LINQ to Objects 查询相同，只是使用了 AsParallel() 方法。此方法是 PLINQ 特有的，可在 ParallelEnumerable 类中使用。此类公开了大多数 PLINQ 功能，并且位于 System.Linq 命名空间中。

> LINQ to Objects 查询表示对任何内存中的 `IEnumerable` 或 `IEnumerable<T>` 接口使用 LINQ 查询。在 LINQ to Objects 查询中，查询的执行不使用 LINQ to SQL 等技术。

与非并行顺序 LINQ 查询类似，PLINQ 查询对任何内存中的 `IEnumerable` 或 `IEnumerable<T>` 接口执行操作。PLINQ 将数据源划分为不同段，然后在多个处理器上通过单独的工作线程执行每一段。在许多情况下，由于并行执行，查询运行得快得多。然而，并行化并不意味着所有查询都会运行得很快，因为并行化可能涉及各种复杂性。此外，请注意，PLINQ 概念仅适用于 LINQ to Objects 查询。

执行以下步骤以在控制台应用程序中使用简单的 PLINQ 查询：

- 1. 启动 Visual Studio 2010。
- 2. 从菜单栏选择“文件→新建→项目”。“新建项目”对话框打开。
- 3. 在“新建项目”对话框左窗格的“已安装的模板”部分中选择 Visual C#→Windows。右窗格中显示可用于在 C# 中开发控制台应用程序的项目模板。
- 4. 在右窗格中选择“控制台应用程序”模板，以创建控制台应用程序。
