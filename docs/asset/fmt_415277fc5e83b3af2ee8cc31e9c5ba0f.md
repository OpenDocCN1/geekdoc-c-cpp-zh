
```csharp
bool flag = int.TryParse(txtLo.Text, lo); // 输入验证

if (flag == false)
{
    MessageBox.Show("Numeric only, 100", "Input Error");
    txtLo.Focus();
}
flag = int.TryParse(txtHi.Text, hi);
if (flag == false)
{
    MessageBox.Show("Numeric only, 100", "Input Error");
    txtHi.Focus();
}
}
private void DoQQuery(int lo, int hi)
{
    var query = from p in numbers
                where p > lo && p < hi
                select p;
    foreach (var val in query)
    {
        lstOutput.Items.Add(val.ToString());
    }
}
#endregion
}
```

# 代码 15-1（续）

```csharp
private void DoQQuery(int lo, int hi)
{
    var query = from p in numbers
                where p > lo && p < hi
                select p; // “查询”
    foreach (var val in query) // 显示结果
    {
        lstOutput.Items.Add(val.ToString());
    }
}
```

# LINQ 的命名空间和引用

在本示例中，你使用了泛型对象，因此需要在程序中包含 `collections-generic` 命名空间。示例程序所需的 `using` 语句如下：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Windows.Forms;
```

为了可以使用正确的引用，你需要向标准列表添加几个新引用。哪些引用列表应该包含这些：

```
System
System.Core
System.Data
System.Data.DataSetExtensions
System.Linq
System.Drawing
System.Windows.Forms.
```

新引用为 LINQ 提供了必要的库。（这些引用没有出现在代码列表中，但在项目的引用部分中。）

定义了一个对象（`numbers`），它可以存储一个 `int` 类型数据的列表。第一个 `for` 循环简单地定义了一个 0 到 `MAXIMUM` 之间的随机数，并将其设置为 `numbers` `List` 对象，并将该值复制到 `Full` `listBox` 对象中。`MAXIMUM` 具有双重作用：既控制随机数的上限，又控制生成的随机数数量。这被称为 SDC（某种乱码代码），因为将一个符号常量用于双重用途通常不是一个好主意。如果这让你感到困扰，可以添加一个你自定义的新常量。

## VAR 关键字

以下语句说明了 LINQ 查询的语法。该语句定义了一个名为 `query` 的变量，其类型为 `var`：

```
var query = from p in numbers          // The "Query"
              where p > lo && p < hi
              select p;
```

`var` 类型允许你定义变量而不指定其具体类型。例如，你可以有这样的定义：

```
var myVar = 61;
```

这导致一些程序员得出结论，认为 `var` 等于 `object` 数据类型。实际上，`var` 与 `object` 是完全不同的。你可以通过以下语句向自己证明这一点：

```
var myVar = 61;
object myObj = 61;
myVar += 1;
myObj += 1;
```

最后一行会生成编译器错误，说明 `+=` 运算符无法应用于 `object` 和 `int` 类型。你可以通过尝试将 `myVar` 和 `myObj` 赋值给原始值类型来进一步证实 `var` 与 `object` 的区别，例如：

```
long big1 = myVar;
long big2 = myObj;
```

第一条语句可以顺利编译，但第二条语句会带来类型不匹配错误，并建议使用强制转换来解决问题。

最后，尝试编译以下语句：

```
var myVar = "Lynne York";
object myObj = "Tom Bangert";
```

变量 `myObj` 编译时通过且不会报错，但 `myVar` 会触发一个错误，指出无法将字符串转换为 `int`。这就是 `var` 类型和 `object` 类型之间的关键区别：`var` 是强类型的。这意味着 `var` 从其被使用的环境中推断出类型。

那么，编译器是如何推断 `var` 的类型的呢？它的类型在初始化时被确定。你不能在定义时不包含初始化来定义一个 `var`。也就是说，以下语句：

```
var myVar; // Causes compiler error!
```

会触发编译器错误：

隐式类型局部变量必须已初始化

因此，`var` 所承担的实际类型由初始化它的表达式决定。因为编译器必须在定义变量时对其进行类型标记，所以任何 `var` 类型定义都必须在定义处进行初始化。

## 在查询中使用 var

考虑列表 15-1 中的这条语句：

```
var query = from p in numbers             // The "Query"
              where p > lo && p < hi
              select p;
```

由于 `numbers` 通常被定义为 `int` 类型数据的列表，因此 `query` 假设其数据类型为 `int`。该语句的作用类似于 SQL 中的 `FROM-WHERE` 子句，用于检查 `numbers` 数据集并提取出落在 `lo` 和 `hi` 之间（不包含边界）的值。将落在指定范围内的值视为一个名为 `p` 的临时集合的一部分，然后将其赋值给 `query`。

该语句：

```
foreach (var val in query)             // Display results
lOutput.Items.Add(val.ToString());
```

定义了第二个名为 `val` 的 `var` 类型，由于其定义的初始化上下文，它假设了与 `query` 相同的数据类型。`foreach` 循环只是遍历 `query` 集合并将值添加到 `lstOutput` 列表框中。

尽管 LINQ 没有提供任何你不需要它就能写出来的功能，但 LINQ 让这一切变得更简单。额外的好处是它的语法模仿了 SQL，如果你已经熟悉 SQL，使用起来会更方便。

在接下来的“尝试一下”中，你将重写程序以使用 LINQ 和字符串数据而不是整数数据。正如列表 15-2所示，基础是相同的。

尝试另一个使用字符串数据的 LINQ 示例 (`Chapter15ProgramLINQExample02.zip`)

尝试另一个 LINQ 示例。在这个示例中，数据按个人所属的州命名。用户从 `listBox` 对象显示的列表中输入她想要检查的州缩写，然后点击计算（Calculate）按钮。右侧的 `listBox` 对象将显示与所选州缩写匹配的条目。图 15-2 显示了程序的示例运行。

以下步骤详细说明了如何设置示例项目：

- 1. 按常规方式创建一个新项目。
- 2. 从文件 `Chapter15ProgramLINQExample02.zip` 下载项目源码。
- 3. 创建一个与图 15-2 所示的用户界面。

### 工作原理

程序的代码在列表 15-2 中。代码与列表 15-10 所示的代码相似，因此我将注释限制在不同的部分。首先，注意我在列表顶部定义了两个静态变量（`passes` 和 `count`）。我使用 `static` 修饰符是因为我希望变量在程序加载时就可用。当 `frmMain()` 构造函数在内存中构建表单图像后，通过调用 `ShowAll()`填充左侧的 `listBox` 对象。

> 列表 15-2: 使用 LINQ 处理字符串数据 (`frmMain.cs`)

```csharp
using System;
using System.Linq;
using System.Windows.Forms;
public class frmMain : Form
{
    static int passes = 0;
    static int count;
    private Button btnClose;
    private ListBox lstOutput;
    private ListBox lstFull;
    private Label lblell;
    private TextBox txtState;
    private Button btnCalc;
    #region Windows code
    public frmMain()
    {
        InitializeComponent();
```

![](img/4329bd7a4f8df07f46abc710b6d0939f_499_0.png)

```
ShowAll();
}
```

```
public static void Main()
{
frmMain main = new frmMain();
Application.Run(main);
}}
```

```
private void btnCalc_Click(object sender, EventArgs e)
{
ShowAll();
}
```

```
private void ShowAll()
{
int i;
var friends = new[] {
new name = "Tom", state = "IN";
new name = "Terry", state = "MT";
new name = "Tammy", state = "IN";
new name = "Jane", state = "OH";
new name = "Don", state = "IN";
new name = "John", state = "IN";
new name = "Linda", state = "FL";
}
```

```
if (passes == 0)
{
count = 0;
for (i = 0; i < count; i++) {
lstOutput.Items.Add(friends[i].name + " " + friends[i].state);
}
passes++;
} else
{
lstOutput.Items.Clear();
var query = from p in friends             // The "Query"
where p.state == txtState.ToUpper()
select p;
foreach (var val in query)           // Display results
lstOutput.Items.Add(val.name + " " + val.state);
}
```

```
private void btnClose_Click(object sender, EventArgs e)
{
Close();
}
```
