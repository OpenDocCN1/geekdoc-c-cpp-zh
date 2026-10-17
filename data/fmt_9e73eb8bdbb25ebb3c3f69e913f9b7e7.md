
```csharp
using System;
using System.IO;
using System.IO.StreamReader;
using System.IO.StreamWriter;
using System.Text;

public class Form1
{
    private void btnReadFile_Click(object sender, EventArgs e)
    {
        // 清空保留列表
        listBoxKeep.Items.Clear();

        // 准备读取文件
        StreamReader rdr = new System.IO.StreamReader(@"C:\App Target Files\File IO With Visual Basic.txt");
        int NameCount = 0;
        string myStrFromFile = ""; // 注意引号内的空格，字符串不为空
        int intKeeperCount = 0;
        // 直到 myStr 等于空
        while (myStrFromFile != "")
        {
            myStrFromFile = rdr.ReadLine();
            if (myStrFromFile != "")
            {
                listBoxNames.Items.Add(myStrFromFile);
                NameCount++; // 计算读取的行数
            }
        }
        // 释放资源和文件
        rdr.Close();
        rdr.Dispose();
        lblKeepCount.Text = "There are " + Convert.ToString(intKeeperCount) + " Keepers";
        lblReadCount.Text = NameCount.ToString() + " Names were loaded.";
    }

    private void btnExit_Click(object sender, EventArgs e)
    {
        Application.Exit();
    }

    // 获取用户输入以添加到文件的名称
    private void btnAddNewName_Click(object sender, EventArgs e)
    {
        string myStrName;
        myStrName = txtBoxName.Text;
        int intStrLength = myStrName.Length;
        if (intStrLength == 0)
        {
            MessageBox.Show("No name was entered for addition to file.", "Check name to add");
            return;
        }

        // 准备将新名称写入文件
        StreamWriter myFileWtr = new StreamWriter(@"C:\App Target Files\File IO With Visual Basic.txt", True);
        myFileWtr.WriteLine(myStrName);
        myFileWtr.Close();
        myFileWtr.Dispose();
        listBoxNames.Items.Add(myStrName);
        int intNamesShown = listBoxNames.Items.Count;
        lblReadCount.Text = "There are " + Convert.ToString(intNamesShown) + " names in the file now.";
        txtBoxName.Text = "";
    }

    // 清空 ListBoxes
    private void btnClearList_Click(object sender, EventArgs e)
    {
        listBoxNames.Items.Clear();
        listBoxKeep.Items.Clear();
    }

    // 删除一个名称
    private void btnDeleteName_Click(object sender, EventArgs e)
    {
        // 清空保留列表
        listBoxKeep.Items.Clear();

        // 选择要删除的名称
        string strToDelete = listBoxNames.SelectedItem.ToString();
        // 获取选中名称的索引
        int intIdx = listBoxNames.SelectedIndex;
        int intCmp;
        int keepCounters;
        string strTarget = "";
        // 读取并与要删除的名称进行行
        StreamReader rdr = new System.IO.StreamReader(@"C:\App Target Files\File IO With Visual Basic.txt");
        int intKeepers2 = 0;
        // 开始从文件读取并比较字符串
        while (strTarget != "")
        {
            strTarget = rdr.ReadLine();
            intCmp = String.Compare(strTarget, strToDelete); // 比较
            if (intCmp != 0 && strTarget != "")
            {
                intKeepers2++; // 计算保留的行数
                // 如果 strToDelete 不等于从文件中读取的行，则添加到保留列表
                listBoxKeep.Items.Add(strTarget);
            }
        }
        // 显示保留的数量
        lblKeepCount.Text = "There were " + Convert.ToString(intKeepers2) + " names.";
        // 释放读取器和文件
        rdr.Close();
        rdr.Dispose();
        // 如果存在，删除旧的名称文件
        bool myboolean = File.Exists(@"C:\App Target Files\File IO With Visual Basic.txt");
        if (myboolean == true)
        {
            File.Delete(@"C:\App Target Files\File IO With Visual Basic.txt");
        }

        // 将保留的名称写入新文件
        StreamWriter myFileWtr = new StreamWriter(@"C:\App Target Files\File IO With Visual Basic.txt", True);
        // 遍历保留名称列表并写入文件
        int intStart = 0;
        int intStop = listBoxKeep.Items.Count - 1;
        string strToWrite;
        int keepersCount = 0;
        for (intStart = 0; intStart <= intStop; intStart++)
        {
            listBoxKeep.SelectedIndex = intStart;
            strToWrite = listBoxKeep.SelectedItem.ToString();
            // 测试代码 MessageBox.Show(strToWrite)
            myFileWtr.WriteLine(strToWrite);
            keepersCount++;
        }
        // 释放资源和文件
        myFileWtr.Close();
        myFileWtr.Dispose();
        // 更新保留计数标签
        lblKeepCount.Text = "There are " + Convert.ToString(keepersCount) + " keeper Names";
        // 更新名称计数标签
        lblReadCount.Text = "There are " + Convert.ToString(keepersCount) + " Names in the file.";
        // 从 listBox 中删除删除的名称
        listBoxNames.Items.RemoveAt(intIdx);
    }
}
```

## 简单编程 C# 和 Visual Basic

这是一个完整的、可运行的 IO 应用。获取这段代码，更改文件名和一些控件属性，你就为另一个用户和场景拥有了另一个应用程序。组织工作是代码复用的重要部分。

仅仅编写 C# 和 Visual Basic……

这种能力甚至更加繁琐，而且在我看来，不值得花费精力。

在我看来，更好的选择是它的表哥——即 `DateTimePicker` 控件。

你可以滚动到过去的月份或现在的月份。属性可以在设计视图中通过属性窗口进行设置。该控件无法同时显示多个月份，但具有滚动到过去或未来月份的能力，效果同样很好。此外，点击向下的箭头可以显示日历日期。这可以在需要时为用户的屏幕留出空间以显示其他项目。

最有用的事件是 `Value_changed` 事件。无法设置/选择日期范围。在我看来，这并不是什么大损失。

它具有我们可以利用来编写外围支持代码的属性和事件。例如，点击一个日期并使用“Value Changed”事件保存一个待办事项（ToDo item），或者点击一个日期查看该日期的计划活动列表。

结合通常的控件，我们可以使用 `DateTimePicker` 在保存项目之前对项目进行时间标记。稍后我们可以使用这些信息在 `listBox` 控件中根据日期对项目进行排序。

此外，我们还可以按照需要格式化显示和使用的日期……我们并不受限于那些可能在一生从未销售过或实现过应用程序的开发者想法。

`<View>` -or- `<Tool Box>` + `<DatePicker>`

`<View>` -or- `<Tool Box>` + `<Button>`

我通过痛苦且沮折的方法了解到，`DatePicker` 控件有一个令人恼火的行为：在程序启动时立即将控件中的日期选择为今天。到目前为止还好……但默认情况下，它会触发 `Value_changed` 事件。如果你在那个事件处理程序中编写了代码，无论是否想要，代码都会执行。关键点是确保代码执行的是你想要的……不多也不少。

好了，让我们开始写代码吧！！！

## C#

在设计视图的表单上，“双双击”一个空白处，进入 `Form_Load` 事件处理程序代码。或者，点击解决方案管理器窗口中的“代码图标”。PS……我总是让解决方案管理器保持可见状态。

当我们完成工作时，你将开发出 16 个事件处理程序，加上 2 个独立方法，总共 18 个代码块。这可不是一个小项目。它让书中到目前为止涵盖的所有内容派上了用场。

我再怎么强调注释代码以及充分利用 MVS IDE 的所有功能对你好处也不为不过。如果你找不到正在寻找的示例代码，那它还不如根本不存在。

你会反复回来使用这个示例作为参考……确保它通过注释和大括号匹配是可以满足该用途的。

需要的控件……

- 3 个标签 `labels`。3 个按钮 `buttons`，6 个单选框框按钮 `radio buttons`，2 个文本框 `textBoxes`，3 个列表框 `listBoxes`，1 个日期选择器 `datePicker`。

你的名称不需要我使用的那些，但请记住你的事件处理程序将使用“你”定义的名称。

名称属性；

| | ListBoxes | Labels |
|---|---|---|
| 1)btnLoadToDoItems | ListBox1 | lblWordSeek |
| 2)btnLoadToDoItems | ListBox2 | lblAddInfo |
| 3)btnLoadSelDayItems | ListBlocked | lbl1 |
| 4)btnClearTodayItems | | |
| 5)ClearToDoItems | | |
| 6)btnSaveInfo | | |
| 7)btnDeleteItem | | |
| 8)btnWordSearch | | |
| 9)btnBlockDate | | |
| 10)btnHideDates | | |
| 11)btnDeleteItem | | |
| 12)SelectedDayItems | | |
| 13)btnNextMonth | | |
| 14)btnThisMonth | | |
| 15)btnSaveAndRepeat | | |
| 16)btnRepeat3Times | | |
| 17)btnRepeat6Times | | |
| 18)btnRepeat9Times | | |
| 19)btnRepeat12Times | | |
| 20)btnRepeat24Times | | |
| 21)btnRepeat36Times | | |

提示：在工具箱上……双击 `Double_Click` 你要添加的控件。每次双击都会添加一个该控件，例如，要添加按钮，然后将它们拖到我想要的地方。这样不那么繁琐而且可以节省一些时间。当你双击控件时，控件会以堆叠方式添加到表单中……拖动上面的，然后是其它的。最后添加的是可见的。给它们命名。再多说一句……在这个项目中我们将使用大量的“读取器 `Readers`”、“写入器 `Writers`”和 `while` 语句来读取文件、评估字符串内容并决定应该采取什么行动。务必花时间彻底理解循环的结构。`while` 循环内部有几个 `if` 语句，因为我们需要对处理的逐项信息采取行动，例如，从文件中读取一行并决定如何处理它。在循环中使用并随后关闭/释放“Stream”对象是**非常重要**的，原因有两个……其一是释放系统资源，二是释放我们正在操作的文件。文件在不先关闭的情况下无法进行读取后进行写入，反之亦然。当你以后处理新的事件处理程序块时，这个错误可能很难找到。我们将在文中讨论去调试和错误捕获。

首先，让我们获取此项目所需的库

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
```

这些可能是为你添加的。但请确保它们在那里。滚动到顶部的行，在“初始化”大括号之后，我们在几个事件处理程序中需要这些变量。

```csharp
public int intLastLoaded;
public int intIdx;
public int intFound = 0;
public string myStrDate = " ";
public string myStrNowYear = " ";
public string myStrNowMonth = " ";
public string myStrNowDay = " ";
public string myStrFinalNow = " ";
public string myStrPicked = " ";
public string myStrFinalDate = " ";
public string mySeekMo = " ";
public string mySeekDay = " ";
public string myStr =
```

在 `Form_Load` 事件处理程序内部（双击表单上的空白处）；

`intLastLoaded =` //这是一个我们将稍后使用的标记。

我们所要做的就是检查标记的值 `0`。//当我们在事件处理程序内部时，日期选择器显示今天的日期作为其文本，但没有触发 `Value_changed` 事件。待办事项加载是因为我们在代码中执行了 "`btnLoadToDoItems.performClick`" 命令。
