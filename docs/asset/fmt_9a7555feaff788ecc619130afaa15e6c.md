
- 5. 按 `F5` 键执行应用程序。表单出现后，单击 `Create and add 10 item` 按钮。`BitArray` 对象被创建并向其中添加了 10 个元素，你可以在 `ListView` 控件中看到它们，如图 32.27 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1550_0.png)

### Figure 32.27: Creating and Adding 10 Elements to the BitArray Object

现在，单击 `Xor` 按钮对每个元素值与指定的值 `True` 执行 XOR 操作。结果显示如下，如图 32.28 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1550_1.png)

### Figure 32.28: Displaying the Result of the XOR Operation

此外，如果你单击 `Not` 按钮，所有位值都会被反转，如图 32.29 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1550_2.png)

### Figure 32.29: Displaying the Result of the NOT Operation

让我们现在学习如何使用泛型集合类。

## Working with Generic Collection Classes

`.NET Framework` 提供了 `System.Collections.Generic` 命名空间，其中包含许多泛型集合类。许多泛型集合类型与非泛型类型有直接对应关系。例如，`List<T>` 类是 `ArrayList` 集合类的泛型版本。你会发现 `SortedList` 类的泛型和非泛型版本，它是 `Dictionary<T>` 和 `List<T>` 类的组合。`Dictionary<T>` 类是 `Hashtable` 类的泛型版本。`Queue<T>` 和 `Stack<T>` 类是 `Queue` 和 `Stack` 集合类的泛型版本。现在，让我们详细讨论这些泛型类。

## Using the List<T> Class

`List<T>` 类包含作为数组起作用的属性。不同之处在于，它会在添加元素时自动扩展。你也可以通过使用 `TrimToSize` 方法或 `Capacity` 属性来缩小该类的对象大小。你可以使用其索引值访问 `List<T>` 对象的每个项目。让我们创建一个名为 `GenericListSample` 的 Windows 窗体应用程序，也可在 CD ROM 上获得，以展示 `List<T>` 类的使用。此应用程序包含一个示例用户界面表单，其中有四个按钮——`Create and adds 10 elements`、`Insert`、`Remove` 和 `Reverse`，以及一个 `ListBox` 控件。

按以下步骤创建此应用程序：

- 1. 在 `GenericListSample` 应用程序中，将 `Form1` 的 `Text` 属性设置为 `Generic List Sample`。
- 2. 将 `ListBox`、`GroupBox` 和四个 `Button` 控件拖放到表单上。
- 3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `Insert`，`button3` 设置为 `Remove`，`button4` 设置为 `Reverse`。
- 4. 将清单 32.7 中给出的代码添加到 `GenericListSample` 应用程序的 `Form1.cs` 文件中：

### Listing 32.7: Showing the Code of the GenericListSample Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace GenericListSample
{
public partial class Form1 : Form
{
    List<string> LstStr = new List<string>();
    public Form1()
    {
        InitializeComponent();
    }
    private void Form1_Load(object sender, EventArgs e)
    {
        button2.Enabled = false;
        button3.Enabled = false;
        button4.Enabled = false;
    }
    private void button1_Click(object sender, EventArgs e)
    {
        LstStr.Add("white");
        LstStr.Add("Black");
        LstStr.Add("Blue");
        LstStr.Add("Yellow");
        LstStr.Add("Green");
```

```
LstStr.Add("Red");
LstStr.Add("Orange");
LstStr.Add("Purple");
LstStr.Add("Magenta");
LstStr.Add("Brown");
LoadList();
button2.Enabled = true;
button3.Enabled = true;
button4.Enabled = true;
}
private void LoadList()
{
    listBox1.Items.Clear();
    for (int i = 0; i < LstStr.Count; i++)
    {
        listBox1.Items.Add(LstStr[i]);
    }
}
private void button2_Click(object sender, EventArgs e)
{
string tempvalue = Microsoft.VisualBasic.Interaction.InputBox("Enter a color to insert in the list", "", "", -1, -1);
string tempindex=Microsoft.VisualBasic.Interaction.InputBox("Enter the index of the color to insert at", "", "", -1, -1);
LstStr.Insert(Convert.ToInt32 ( tempindex), tempvalue);
LoadList();
}
private void button3_Click(object sender, EventArgs e) {
if (listBox1.SelectedIndex > -1) {
    LstStr.RemoveAt(listBox1.SelectedIndex);
    LoadList();
}
else {
    MessageBox.Show("Select a value to be removed from the ListBox");
}
}
private void button4_Click(object sender, EventArgs e)
{
LstStr.Reverse();
LoadList();
}
}
```

在清单 32.7 中，我们创建了一个 `List<T>` 类的对象 `LstStr`。`button1` 控件的 `Click` 事件使用 `List<T>` 类的 `Add` 方法向 `LstStr` 对象添加元素。接下来，`button2` 和 `button3` 控件的 `Click` 事件分别使用 `Insert` 和 `RemoveAt` 方法从指定的索引号插入和移除一个元素。最后，`button4` 控件的 `Click` 事件使用 `Reverse` 方法反转 `LstStr` 对象的元素顺序。

5. 按 `F5` 键执行应用程序。当窗体出现时，单击 `Create and add 10 items` 按钮。`ListBox` 控件会填充 10 种颜色的名称，如图 32.30 所示：

### Figure 32.30: Adding 10 Elements to the List<T> Object

你可以单击 `Insert` 和 `Remove` 按钮分别插入新项目或从列表中移除项目。例如，项目名称 `Purple` 已从列表中移除，如图 32.31 所示：

### Figure 32.31: Removing an Element from the List<T> Object

你可以单击 `Reverse` 按钮反转 `ListBox` 控件中显示的颜色名称的顺序。

## Using the LinkedList<T> Class

在本节中，你将学习如何使用 `LinkedList<T>` 类，它是一个泛型类，允许你创建双向链表形式的集合。让我们创建一个名为 `GenericLinkedListSample` 的应用程序，也可在 CD-ROM 上获得，以展示 `LinkedList<T>` 类的使用。该应用程序包含一个示例用户界面窗体，其中有七个按钮——`Create and adds 10 elements`、`AddFirst`、`AddLast`、`RemoveFirst`、`AddAfter`、`AddBefore` 和 `RemoveLast`，以及一个 `ListBox` 控件。

按以下步骤创建 `GenericLinkedListSample` 应用程序：

- 1. 在 `GenericLinkedListSample` 应用程序中，将 `Form1` 的 `Text` 属性设置为 `Generic LinkedList Sample`。
- 2. 向 `Form1` 窗体添加一个 `ListBox`、一个 `GroupBox` 和七个 `Button` 控件。
- 3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `AddFirst`，`button3` 设置为 `AddLast`，`button4` 设置为 `RemoveFirst`，`button5` 设置为 `AddAfter`，`button6` 设置为 `AddBefore`，`button7` 设置为 `RemoveLast`。
- 4. 将清单 32.8 中给出的代码添加到 `GenericLinkedListSample` 应用程序的 `Form1.cs` 文件中：

### Listing 32.8: Showing the Code of the GenericLinkedListSample Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace GenericLinkedListSample
{
public partial class Form1 : Form
{
    LinkedList<string> LnLstStr = new LinkedList<string>();
    public Form1()
    {
        InitializeComponent();
    }
    private void Form1_Load(object sender, EventArgs e)
    {
        button2.Enabled = false;
        button3.Enabled = false;
        button4.Enabled = false;
        button5.Enabled = false;
        button6.Enabled = false;
        button7.Enabled = false;
    }
    private void button1_Click(object sender, EventArgs e)
    {
        LnLstStr.AddLast("white");
        LnLstStr.AddLast("Black");
        LnLstStr.AddLast("Blue");
        LnLstStr.AddLast("Yellow");
        LnLstStr.AddLast("Green");
        LnLstStr.AddLast("Red");
        LnLstStr.AddLast("Orange");
        LnLstStr.AddLast("Purple");
        LnLstStr.AddLast("Magenta");
        LnLstStr.AddLast("Brown");
        LoadLnkdList();
        button2.Enabled = true;
        button3.Enabled = true;
        button4.Enabled = true;
        button5.Enabled = true;
        button6.Enabled = true;
        button7.Enabled = true;
    }
    private void LoadLnkdList() {
        listBox1.Items.Clear();
        foreach (string StrObj in LnLstStr)
        {
            listBox1.Items.Add(StrObj);
        }
    }
    private void button2_Click(object sender, EventArgs e)
    {
        string tempStr = Microsoft.VisualBasic.Interaction.InputBox("Enter a value for the color to be added.", "", "", -1, -1);
```

```
LnLstStr.AddFirst(tempStr);
LoadLnkdList();
}
private void button3_Click(object sender, EventArgs e)
{
string tempStr = Microsoft.VisualBasic.Interaction.InputBox("Enter a value for the color to be added.", "", "", -1, -1);
LnLstStr.AddLast(tempStr);
LoadLnkdList();
}
private void button4_Click(object sender, EventArgs e)
{
if (listBox1.Items.Count > 0)
{
LnLstStr.RemoveFirst();
LoadLnkdList();
}
}
private void button5_Click(object sender, EventArgs e) {
if (listBox1.SelectedItems.Count > 0) {
string tempStr = Microsoft.VisualBasic.Interaction.InputBox("Enter a value for the color to be added.", "", "", -1, -1);
LnLstStr.AddAfter(LnLstStr.Find(listBox1.SelectedItem.ToString()), tempStr);
LoadLnkdList();
}
else {
MessageBox.Show("Please select an item from the list first.");
}
}
private void button6_Click(object sender, EventArgs e)
{
if (listBox1.SelectedItems.Count > 0)
{
string tempStr = Microsoft.VisualBasic.Interaction.InputBox("Enter a value for the color to be added.", "", "", -1, -1);
LnLstStr.AddBefore(LnLstStr.Find(listBox1.SelectedItem.ToString()), tempStr);
LoadLnkdList();
}
else
{
MessageBox.Show("Please select an item from the list first.");
}
}
private void button7_Click(object sender, EventArgs e)
{
LnLstStr.RemoveLast();
LoadLnkdList();
}
}
```
