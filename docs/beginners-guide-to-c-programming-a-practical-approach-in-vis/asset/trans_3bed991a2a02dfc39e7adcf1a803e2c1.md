
![](img/41d82527c4e41cdb7e56259564306ddc_245_0.png)

图 9.9. 用 0 到 10 的数字填充的 ComboBox

## 9.4. Do-While 循环

Do-while 循环与 while 循环类似。它们的区别在于，在 do-while 结构中，循环条件是在循环块结束时检查的，如下所示：

```
loop variable initialization
do
{
    The code that will be repeated will be written here.
    Loop variable change (usually increment/decrement).
}
while(loop condition)
```

代码 9.21

从此模板可以看出，当 do-while 循环开始时，循环块会执行一次，然后再检查循环条件。如果该条件得到满足，循环会继续。并且与 while 循环一样，当循环条件不满足时循环结束。从此代码结构可以看出，do-while 循环至少执行一次。

让我们为本项目修改 while 循环示例：

- 1. 复制 while 循环项目文件夹并将其重命名为 do-while 项目。
- 2. 在 populate_Click(...) 方法中删除 while 循环部分，并将循环变量 i 的初始值设为 2：

```csharp
private void populateButton_Click(object sender, EventArgs e)
{
    int stopValueInt = Convert.ToInt32(stopValue.Text);
    int i = 2;
}
```

代码 9.22

- 3. 输入 do 并双击 Tab（在键盘上按两次 Tab），形成如下的 do-while 模板：

```csharp
private void populateButton_Click(object sender, EventArgs e)
{
    int stopValueInt = Convert.ToInt32(stopValue.Text);
    int i = 2;
    do
    {
    } while (true);
}
```

代码 9.23

- 4. 在 do-while 块内添加将循环变量当前值插入 ComboBox 的代码行并将 i 增加 1：

```csharp
private void populateButton_Click(object sender, EventArgs e)
{
    int stopValueInt = Convert.ToInt32(stopValue.Text);
    int i = 2;
    do
    {
        numbersComboBox.Items.Add(i);
        i++;
    } while (true);
}
```

代码 9.24

- 5. 最后，如前所述设置循环条件：

```csharp
private void populateButton_Click(object sender, EventArgs e)
{
    int stopValueInt = Convert.ToInt32(stopValue.Text);
    int i = 2;
    do
    {
        numbersComboBox.Items.Add(i);
        i++;
    } while (i <= stopValueInt);
}
```

代码 9.24（续）

- 6. 构建并运行项目。会出现以下程序窗口：

![](img/41d82527c4e41cdb7e56259564306ddc_247_0.png)

图 9.11. 程序窗口

当我们输入一个大于 2 的数字并单击 Populate 按钮时，ComboBox 将从 2 填充到该数字：

![](img/41d82527c4e41cdb7e56259564306ddc_247_1.png)

图 9.12. 由值填充的 ComboBox

程序的操作与在 TextBox 中输入大于或等于 2 的 while 循环示例相同。但是，如果我们输入一个小于 2 的数字，例如 2，则 do-while 循环的差异就会显现出来：

![](img/41d82527c4e41cdb7e56259564306ddc_248_0.png)

图 9.13. 输入数字为 1 时程序的输出

根据循环条件 i <= stopValueInt，循环条件从未得到满足（开始时 i=2 且 stopValueInt=1）。然而，由于 do-while 块中的代码行在检查此条件之前执行一次，因此 ComboBox 被 2 填充，代码行 numbersComboBox.Items.Add(i); 中的 i=2 为循环变量的起始值。

## 9.5. Break 和 Continue 关键字

我们已在条件语句中使用过 break 关键字。它也可以以相同的方式用于循环中。当 break 关键字在循环块内部执行时，循环立即结束，即 break 关键字中断循环。

循环中还有另一个关键字：continue。continue 关键字的工作与 break 关键字类似。它停止当前循环块的执行并跳到循环开始处。break 和 continue 关键字都与循环中的条件语句一起使用。

让我们在我们的 while 循环示例中使用这些关键字。

- 1. 打开 while 循环项目并找到 populateButton_Click(...) 方法，如代码 9.25 所示。

```csharp
private void populateButton_Click(object sender, EventArgs e)
{
    int stopValueInt = Convert.ToInt32(stopValue.Text);
    int i = 0;
    while (i <= stopValueInt)
    {
        numbersComboBox.Items.Add(i);
        i++;
    }
}
```

代码 9.25（续）

- 2. 让我们使用 continue 关键字在循环变量为 3 时跳到开头：

```csharp
private void populateButton_Click(object sender, EventArgs e)
{
    int stopValueInt = Convert.ToInt32(stopValue.Text);
    int i = 0;
    while (i <= stopValueInt)
    {
        if (i==3)
        {
            continue;
        }
        numbersComboBox.Items.Add(i);
        i++;
    }
}
```

代码 9.26

- 3. 构建并运行项目。在 TextBox 中输入一个大于 3 的数字，例如 10，然后单击 Populate 按钮。你会注意到程序停止响应，因为出现了无限循环！：

Stops responding...

![](img/41d82527c4e41cdb7e56259564306ddc_249_0.png)

图 9.14. 程序处于无限循环中

我们无法通过单击其右上角的关闭按钮退出程序，因为形成了一个无限循环。我们可以从 Windows 的任务管理器中关闭程序，或单击 Visual Studio 中的停止按钮：

![](img/41d82527c4e41cdb7e56259564306ddc_250_0.png)

图 9.15. 在无限循环中停止程序

### 为什么程序会进入无限循环？

当 i=3 时，if 条件得到满足并执行 continue 命令。程序跳到循环开始处，i=3，if 条件再次以 i=3 得到满足，continue 关键字再次执行，将程序跳回循环开始处，i=3... 此过程反复进行导致无限循环。我们只需在 if 块内在 continue 命令之前更新循环变量即可消除此编程错误，如下所示

```csharp
private void populateButton_Click(object sender, EventArgs e)
{
    int stopValueInt = Convert.ToInt32(stopValue.Text);
    int i = 0;
    while (i <= stopValueInt)
    {
        if (i==3)
        {
            i++;
            continue;
        }
        numbersComboBox.Items.Add(i);
        i++;
    }
}
```

代码 9.27（续）

经过此修改后，我们可以运行程序，它工作正常。当 i=3 时，if 语句的条件得到满足，循环变量增加到 4，然后程序跳到循环开始处，使用此新的循环变量值。值 3 没有添加到 ComboBox，因为程序在 i=3 时跳到循环开始处，而没有执行 if 语句下面的代码行：

![](img/41d82527c4e41cdb7e56259564306ddc_251_0.png)

如果我们将此程序中的 continue 关键字更改为 break 会怎样：

```csharp
private void populateButton_Click(object sender, EventArgs e)
{
    int stopValueInt = Convert.ToInt32(stopValue.Text);
    int i = 0;
    while (i <= stopValueInt)
    {
        if (i==3)
        {
            i++;
            break;
        }
        numbersComboBox.Items.Add(i);
        i++;
    }
}
```

代码 9.28

在这种情况下，当循环变量取值为 3，即 i=3 时，if 块内的 break 命令执行，导致循环完全退出。因此，3 和大于 3 的数字不会添加到 ComboBox：

![](img/41d82527c4e41cdb7e56259564306ddc_252_0.png)

图 9.17. 循环在 i=3 处被中断

我们现在已在 C# 中学习了变量、条件语句和循环。在进入方法（函数）之前，我们将在下一章学习数组，数组用于保存同一变量类型的多个值。

## 第 10 章

![](img/41d82527c4e41cdb7e56259564306ddc_254_0.png)

## 数组和集合

数组是用于保存相同类型多个数据的数据结构，而集合则能够将不同类型变量一起存储。

## 10.1. 数组

数组通过以列表格式保存相同类型的数据使我们的生活更轻松，这样我们就可以使用索引轻松访问它们。我们可以想象数组的结构如下：

| 索引 | 0 | 1 | 2 | 3 | 4 | ... | n-1 |
| 元素 | 第1个元素 | 第2个元素 | 第3个元素 | 第4个元素 | 第5个元素 | ... | 第n个元素 |

表 10.1. 典型的数组结构

如你所见，数组的每个元素都有一个从 0 开始的索引。这是规则，因此对于一个 n 个元素的数组，其元素的索引将取值为 0、1、2、...、n-1。

### 10.1.1. 声明数组

数组的定义与变量类似很容易。变量类型附近的方括号告诉 C# 编译器我们正在声明一个数组：

```
variable_type[] newArray;
```

代码 10.1

在此代码行中，我们声明了一个名为 newArray 的数组，但未对其进行初始化或指定其元素数量。在这种情况下，还未为此数组分配内存位置。我们必须指定数组的元素数量才能实际创建它，如下所示：
