
注意你可以将任何一个集合放在`ListBox`对象中。

# 列表 8-3: 集合示例程序 (`frmMain.cs`)

```csharp
using System;
using System.Windows.Forms;

public class frmMain
{
    private Button btnCalc;
    private Button btnClose;
    private ListBox lstTest;
    #region Windows code

    public frmMain()
    {
        InitializeComponent();
    }

    public static void Main()
    {
        frmMain main = new frmMain();
        Application.Run(main);
    }

    private void btnClose_Click(object sender, EventArgs e)
    {
        Close();
    }

    private void btnCalc_Click(object sender, EventArgs e)
    {
        int[] days = new int[] { 0, 28, 30, 30, 30, 31, 31 };
        string[] weekDays = new string[] { "Monday", "Tuesday", "Thursday", "Friday", "Saturday", "Sunday" };

        foreach (string str in weekDays)
        {
            lstTest.Items.Add(str);
        }
        foreach (int val in days)
        {
            lstTest.Items.Add(val.ToString());
        }
    }
}
```

### 工作原理

程序的代码在列表 8-3 所示。

这两个数组在按钮点击事件方法中定义。注意在遍历集合的循环中使用了 `foreach` 关键字：

```csharp
foreach (string str in weekDays)
{
    lstTest.Items.Add(str);
}
foreach (int val in days)
{
    lstTest.Items.Add(val.ToString());
}
```

`foreach` 循环专门设计用于遍历对象集合。它与标准的 `for` 循环相似，在标准的 `for` 循环中，第一个表达式 `expression1` 总是被设置为集合中的第一个对象，而循环通过 `for` 循环中的表达式 3 逐个遍历数组中的所有元素。循环的数据类型必须与集合中的数据类型匹配。这就是为什么在第一个循环中 `str` 是 `string` 类型，而在第二个循环中 `val` 是 `int` 类型。

你应该将 `foreach` 循环视为一个只读循环。也就是说，你不应该使用 `foreach` 循环来更改集合中任何对象的值。集合提供了一种方便的方法通过遍历它们来查看对象，但你不应该尝试在 `foreach` 循环中更改这些对象。

# `ARRAYLIST` 对象

到目前讨论的数组被称为静态数组。这是因为当你设置它们的元素时，大小是更改的。事实上，在确定其维度或多个维度之前，你无法使用静态数组。然而，生活并非那么简单。通常你会遇到这样一种情况：你需要在数组中存储数据，但不知道可能需要多少个元素。例如，你可能会编写一个程序，在对象数组中记录朋友的名字和地址。当你运行程序时，你可能需要 50 个数组元素，但另一个人可能只需要 20 个元素。问题是：“你如何决定为数组分配多少元素？”

对于静态数组，通常的解决方案是妥协最坏情况的设计。最坏情况的设计是你尝试获取数组大小上可能需要的最大合理值。这可能是低效的，因为在大多数情况下，你都会高估数组所需的大小。静态数组的局限性。`ArrayList` 对象具有创建动态数组的效果，你不需要指定大小。现在来看看这个操作。

`ArrayList` 对象提供了一些简单数组不具备的功能。这对于在编译时不知道数组大小的数组来说尤其如此。“尝试一试”展示了你如何在程序中使用 `ArrayList`。

# 尝试一试 `ArrayList` 示例 (`Chapter8ProgramArrayList.zip`)

编写一个简单的程序，能够在对象数组中记录朋友的名字和地址。运行程序时，你可能需要 50 个数组元素，但另一个人可能只需要 20 个元素。问题是：“你如何决定为数组分配多少元素？”

- 1. 按照通常方式创建一个新的 `ArrayList`。
- 2. 在列表 8-4 所示中创建一个 `ArrayList` 实例、文本框对象、按钮对象以及列表框对象。
- 3. 在图 8-1 所示中使用 `ArrayList`。
