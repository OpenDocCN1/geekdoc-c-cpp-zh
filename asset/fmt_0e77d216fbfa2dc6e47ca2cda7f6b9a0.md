
另一个提示：记得我们为匹配大括号设置的编辑器选项吗？？对于这个项目以及其他更大的项目，这可以是一个真正的头疼救星。我也会在大括号之后添加类似 `//End of Namespace` 的短注释，例如，这有助于我理解代码块并协助故障排除。这不是一个不足道的问题，非常值得花费精力。回到工作中。在事件处理程序之外输入以下代码，它是一个独立的方法。它有自己的大括号，不应与另一个事件处理程序混合。

```csharp
public void SetMyCustomFormat()
{
  // 设置 Format 类型和 CustomFormat 字符串
  dateTimePicker1.Format = DateTimeFormat.Custom;
  dateTimePicker1.CustomFormat = "MM/ dd/ yyyy";
}
```

这一行导致日期显示为例如 `03/29/2015`。当你对文件项目进行时间标记并在稍后读取文件时需要搜索和排序时，这种格式更容易处理得多。如果由于某种我无法理解的原因，你想要将月份和星期完整写出来，可以使用这种格式。

```csharp
dateTimePicker1.CustomFormat = "MMMM/ dd/ yyyy - ddddd";
```

John Queen

4855 这一行导致日期显示为格式，例如

4857 March/29/2015 Friday

```
要消除斜杠，只需按照如下方式输入：

dateTimePicker.CustomFormat = "MMMM dd yyyy - dddd";
```

每当我们需要时，只需通过输入其名称即可“调用”这种格式化方法，例如

`SetMyCustomFormat()`

## 调用此方法后使用的日期将采用简短格式。

`DatePicker` 的另一个特性是，当代码重新设置日期格式时，它会触发 `value_changed` 事件，就像[用户]选择了不同的日期一样。第一次使用此命令时，你“可能会”看到两个事件发生，即……消息框显示没有“待办事项”。在第一次发生之后，这种情况就不会再次发生了了……只是提个醒。

我提到了 `dataPicker` 控件的 `Value_Changed` 事件。我们现在将使用此事件来从待办事项文件中检索项目，并仅显示带有所选日期时间戳的项。

当 `datePicker` 出现时，显示的文本日期无法直接用于从文件中选择今天日期的项目。

### 简单的 C# 和 Visual Basic 编程……

点击向下滚动/下拉箭头，并在视觉日历月份中点击今天的日期。文本将变为我们用于保存项目时使用的格式，即 `01/26/2013`。

之后，`Select Today’s items` 按钮事件处理器就可以正常运行了。到此为止，我们的代码如下：

```
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

实际上，先编写哪一个事件处理器并不重要。我认为最好按照用户可能使用程序的顺序来思考和编写代码。一个人可能可能想做的第一件事就是建立一些被“锁定”的日期，即：这些日期无法输入待办事项。

这是另一个独立方法。它位于所有事件程序代码块之外。这简单地将信息写入文件，稍后将在某些事件程序中检索并使用。它有一个伙伴方法叫做“取消锁定日期”。事事优先。

设置要锁定的日期。使用 `dateTime`，用户将首先选择要锁定的日期，然后点击“锁定日期”。

```csharp
private void btnBlockDate_Click(object sender, EventArgs e)
{
    mySeekDay = "";
    mySeekMo = "";
    mySeekYr = "";
    mySeekDateFinal = "";
    DateTime myTestDate = Convert.ToDateTime(dateTimePicker1.Text);
    //test code
    MessageBox.Show(Convert.ToString(myTestDate), "datePicker.Text");
    mySeekDay = "";
    mySeekMo = "";
    mySeekYr = "";
    mySeekDateFinal = "";
    intIdxItemFound = 0;
    mySeekDay = Convert.ToString(myTestDate.Day);
    mySeekMo = Convert.ToString(myTestDate.Month);
    mySeekYr = Convert.ToString(myTestDate.Year);
    intLenMo = mySeekMo.Length;
    if (intLenMo == 1)
    {
        mySeekMo = "0" + mySeekMo;
    }
    intLendDay = mySeekDay.Length;
    if (intLendDay == 1)
    {
        mySeekDay = "0" + mySeekDay;
    }
    listBlocked.Visible = true;
    mySeekDateFinal = mySeekMo + "/" + mySeekDay + "/" + mySeekYr;
    StreamWriter myWrtBlock = new StreamWriter(@"C:\Target Files\BlockedDates.txt", true);
    listBlocked.Items.Add(mySeekDateFinal);
    myWrtBlock.WriteLine(mySeekDateFinal);
    myWrtBlock.Close();
    myWrtBlock.Dispose();
    listBlocked.Visible = false;
}
```

### 取消锁定日期

这同样简单地获取日期并从文件中删除该字符串以取消锁定。

```csharp
private void btnUnblockDate_Click(object sender, EventArgs e)
{
    if (File.Exists(@"C:\Target\BlockedDates.txt"))
    {
        File.Delete(@"C:\Target\BlockedDates.txt");
    }
    // 从 listBox 获取项目
    int intUnBlock = listBoxBlocked.SelectedIndex;
    string strItemUnblock = Convert.ToString(listBoxBlocked.SelectedItem);
    listBoxBlocked.Items.RemoveAt(intUnBlock);
    int intKeeper = listBoxBlocked.Items.Count;
    int ZZ = 0;
    StreamWriter myWrt = new StreamWriter(@"C:\Target\BlockedDates.txt", true);
    while (ZZ <= intUnBlock)
    {
        listBoxBlocked.SelectedIndex = ZZ;
        strItemUnblock = Convert.ToString(listBoxBlocked.SelectedItem);
        myWrt.WriteLine(strItemUnblock);
        ZZ++;
    } // End while
    myWrt.Close();
    myWrt.Dispose();
}
```

在对开放待办事项的日期设置了一些限制后，我们就可以继续了。通常在我看来，这意味着选择一个日期，输入一些项目进行保存，保存它们，检索它们并编辑它们。

```csharp
namespace VS_CS_DateTimePicker
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        public intIdxItemFound;
        public intItemFound = 0;
        public string myStrDate = "";
        public string myStrNowYear = "";
        public string myStrNowMonth = "";
        public string myStrNowDay = "";
        public string myStrFinalNow = "";
        public string myStrFinalPicked = "";
        public string myStr = "";
        public string myPath = @"C:\Target Files\ToDo.txt";
```

第一要要务是为点击 `datePicker` 触发的“Value_Changed 事件”编写一个事件处理器。

```csharp
private void dateTimePicker1_ValueChanged(object sender, EventArgs e)
{
    SetMyCustomFormat();
    myStrDate = dateTimePicker1.Text;
    txtAddInfo.Visible = true;
    btnSaveInfo.Visible = true;
} //End DateTimePicker value changed
```

### 简单的 C# 和 Visual Basic 编程……

首先，在选择日期后，保存一些待办事项。我们将使用两个（2）不同的按钮和事件处理器来保存待办事项。第一个用于保存单个项目。稍晚时候，我们将赋予用户在 3 到 36 个月的范围内多次保存项目的能力。一次只做一件事，让我们先保存一次。

双击 `<btnSaveInfo>`

输入你的代码来保存项目。

```csharp
private void btnSaveInfo_Click(object sender, EventArgs e)
{
    SetMyCustomFormat();
    // 声明选择日期变量
    mySeekDay = "";
    mySeekMo = "";
    mySeekYr = "";
    mySeekDateFinal = "";
    // 从文本中获取日期
    DateTime mySaveDate = Convert.ToDateTime(dateTimePicker1.Text);
    intIdxItemFound = 0;
    // 填充选择日期变量
    mySeekDay = Convert.ToString(mySaveDate.Day);
    mySeekMo = Convert.ToString(mySaveDate.Month);
    mySeekYr = Convert.ToString(mySaveDate.Year);
    // 在单数字日期和月份字符串前加上“0”
    intLenMo = mySeekMo.Length;
    if (intLenMo == 1)
    {
        mySeekMo = "0" + mySeekMo;
    }
    intLendDay = mySeekDay.Length;
    if (intLendDay == 1)
    {
        mySeekDay = "0" + mySeekDay;
    }
    // 定义要保存的日期字符串
    string myDateToSave = mySeekMo + "/" + mySeekDay + "/" + mySeekYr;
    // 定义要保存的字符串
    stringStringToSave = myStrDate + " " + txtAddInfo.Text;
    // 定义 StreamReader
    StreamReader mySr = new StreamReader(@"C:\Target Files\BlockedDates.txt");
    // 读取锁定日期列表
    string myStrBlockedDate = "XX";//起始避免空字符串
    while (myStrBlockedDate != "") && myStrBlockedDate!=null)
    {
        myStrBlockedDate = mySr.ReadLine();
        // 当读取为空时结束
        if (myDateToSave == " " || myStrBlockedDate == null)
        {
            //释放 StreamReader 和文件
            mySr.Close();
            mySr.Dispose();
            break;
        }
    }
    //
    // 如果选择的日期与锁定日期不匹配，则保存项目
    if (myDateToSave!=myStrBlockedDate)
    {
        StreamWriter myWrt = new StreamWriter(@"C:\Target Files\ToDo.txt", true);
        // MessageBox.Show(myStringToSave);
        myWrt.WriteLine(myStringToSave);
        //释放 StreamWriter 和文件
        myWrt.Close();
        myWrt.Dispose();
    }
}
}
```

### 简单编程 C# 和 Visual Basic...

```csharp
5123   {
5124     MessageBox.Show("This is a blocked date.\n5125 Blocked Date vs Save());
5126     textBoxAddInfo.Text = ""
5127     // cannot save to blocked date, return to
5128 user screen
5129     return;
5130 }
5131 // 将添加信息的文本框置为空
5132     textBoxAddInfo.Text = ""
5133     listBox1.Sorted = true;
5134     listBox1.Visible = true;
5135     //重新加载 ToDo Items 文件
5136     btnLoadToDoItems.PerformClick();
5137 } // End SaveInfo
```

#### 5139 保存并重复

此事件处理程序使用了添加的单选按钮和 `datePicker` 的“AddMonths”方法。

```csharp
5144
5145 private void bntSaveRepeat_Click(object sender,
5146 EventArgs e)
5147 {
5148     // 获取要保存的信息
5149     string myStrToSave = textBoxAddInfo.Text;
5150     // 确定项目的重复次数
5151     // 此数字保存于变量中，用于
5152     // 计算执行循环的次数
5153     // 并初始化变量
5154     int intCheckedRepeat = 1;
5155     if (rad3Times.Checked) {intCheckedRepeat
5156 = 3;}
5157     if (rad6Times.Checked) {intCheckedRepeat
5158 = 6;}
5159     if (rad9Times.Checked) {intCheckedRepeat
5160 = 9;}
5161     if (rad12Times.Checked)
5162     {intCheckedRepeat = 12;}
```
