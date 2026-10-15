
在清单 32.8 中，我们创建了一个 `LinkedList<T>` 类的对象 `LnLstStr`。`button1` 控件的 `Click` 事件使用 `LinkedList<T>` 类的 `AddLast` 方法向 `LnLstStr` 对象添加元素。接下来，`button2` 和 `button3` 控件的 `Click` 事件分别使用 `AddFirst` 和 `AddLast` 方法在 `LnLstStr` 对象的第一和最后位置添加元素。`button5` 和 `button6` 控件的 `Click` 事件分别使用 `AddAfter` 和 `AddBefore` 方法在 `LnLstStr` 对象中指定的元素之后或之前添加一个元素。最后，`button4` 和 `button7` 控件的 `Click` 事件分别使用 `RemoveFirst` 和 `RemoveLast` 方法从 `LnLstStr` 对象的第一和最后位置移除一个元素。

5. 按 `F5` 键执行应用程序。当窗体出现时，单击 `Create and add 10 items` 按钮。`ListBox` 控件会填充 10 个颜色名称，如图 32.32 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1556_0.png)

你可以单击 `AddFirst` 和 `AddLast` 按钮分别在列表的第一或最后位置添加项目。对于 `AddBefore` 和 `AddAfter` 按钮用于在列表中指定的项目之前或之后添加项目。例如，我们已选择 `Pink` 颜色在 `Purple` 颜色之前显示，如图 32.33 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1556_1.png)

图 32.34 显示了在 `Purple` 颜色前添加 `Pink` 颜色后更新的列表：

![](img/e073a4882197be4ab61103cbe0bcb394_1556_2.png)

此外，你可以单击 `RemoveFirst` 和 `RemoveLast` 按钮分别从列表的第一和最后位置移除一个元素。

## Using the SortedList<TKey, TValue> Class

如 In Depth 部分所述，`SortedList<TKey, TValue>` 类允许你创建键/值对的泛型集合。它们的工作方式类似于键/值对的数组，因此可以通过键或索引检索值。

让我们创建一个名为 `GenericSortedListSample` 的应用程序，也可在 CD-ROM 上获得，以了解 `SortedList<TKey, TValue>` 类的使用。该应用程序包含一个示例用户界面窗体，其中有三个按钮——`Create and add 10 items`、`Index of Key` 和 `Index of Value`，以及一个 `ListView` 控件。

按以下步骤创建 `GenericSortedListSample` 应用程序：

- 1. 在 `GenericSortedListSample` 应用程序中，将 `Form1` 的 `Text` 属性设置为 `Generic SortedList Sample`。
- 2. 将一个 `ListView`、一个 `GroupBox` 和三个 `Button` 控件拖放到窗体上。
- 3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `Index Of Key`，`button3` 设置为 `Index Of Value`。
- 4. 通过在属性窗口中单击 `ListView` 控件的 `Columns` 属性的省略号按钮 `...` 来向 `ListView` 控件添加列。`ColumnHeader Collection Editor` 对话框出现。
- 5. 在 `ColumnHeader Collection Editor` 对话框中单击 `Add` 按钮向 `ListView` 控件添加一列。将此列的 `Name` 属性设置为 `Key`，`Text` 属性设置为 `Keys`。同样，为 `ListView` 控件添加另一列，名称设为 `Value`，文本设为 `Values`，然后单击 `OK` 按钮。
- 6. 将清单 32.9 中给出的代码添加到 `GenericSortedListSample` 应用程序的 `Form1.cs` 文件中：

### Listing 32.9: Showing the Code of the GenericSortedListSample Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace GenericSortedListSample
{
public partial class Form1 : Form
{
    SortedList<int, string> SListStr = new SortedList<int, string>();
    public Form1()
    {
        InitializeComponent();
    }
    private void Form1_Load(object sender, EventArgs e)
    {
        button2.Enabled = false;
        button3.Enabled = false;
    }
    private void button1_Click(object sender, EventArgs e)
    {
        SListStr.Add(100, "white");
        SListStr.Add(101, "Black");
        SListStr.Add(102, "Blue");
        SListStr.Add(103, "Yellow");
```

# 立即可用的解决方案

```
SLListStr.Add(104, "Green");
SLListStr.Add(105, "Red");
SLListStr.Add(106, "Orange");
SLListStr.Add(107, "Purple");
SLListStr.Add(108, "Magenta");
SLListStr.Add(109, "Brown");
LoadSrtList();
button2.Enabled = true;
button3.Enabled = true;
```

```
private void LoadSrtList()
{
	listView1.Items.Clear();
	for (int i = 0; i < SListStr.Count; i++)
	{
		ListViewItem lItem = listView1.Items.Add(SListStr.Keys[i].ToString());
		lItem.SubItems.Add(SListStr.Values[i]);
	}
}
```

```
private void button2_Click(object sender, EventArgs e)
{
	string tempkey = Microsoft.VisualBasic.Interaction.InputBox("Enter the key to find the index of", "", "", -1, -1);
	int tempindex = SListStr.IndexOfKey(Convert.ToInt32(tempKey));
	if (tempindex < 0)
	{
		MessageBox.Show("The key does not exist in the sortedlist.");
	}
	else
	{
		MessageBox.Show("The key in the sortedlist has an index : " + tempindex + ".");
	}
}
```

```
private void button3_Click(object sender, EventArgs e)
{
	string tempValue = Microsoft.VisualBasic.Interaction.InputBox("Enter the value to find the index of", "", "", -1, -1);
	int tempindex = SListStr.IndexOfValue(tempValue.ToString());
	if (tempindex < 0)
	{
		MessageBox.Show("The value does not exist in the sortedlist.");
	}
	else
	{
		MessageBox.Show("The value in the sortedlist has an index : " + tempindex + ".");
	}
}
```

在清单 32.9 中，我们创建了一个 `SortedList<TKey, TValue>` 类的对象 `SListStr`。接下来，`button1` 控件的 `Click` 事件使用 `Add` 方法向 `SListStr` 对象中添加元素。接下来，`button2` 和 `button3` 控件的 `Click` 事件分别使用 `IndexOfKey` 和 `IndexOfValue` 方法查找指定键或值的索引值。

7. 按 `F5` 键执行应用程序。表单出现后，单击 `Create and add 10 items` 按钮。`ListView` 控件填充了 10 个颜色名称，如图 32.35 所示：

# 第 32 章：集合和泛型

![](img/e073a4882197be4ab61103cbe0bcb394_1559_0.png)

## 图 32.35：向 SortedList<TValue> 对象添加 10 个元素

您可以单击 `Index Of Key` 按钮和 `Index Of Value` 按钮分别查找特定键或值的索引值。例如，我们已单击 `Index Of Value` 按钮来查找 `Blue` 颜色的索引，如图 32.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1559_1.png)

## 图 32.36：查找 Blue 颜色的索引

会出现一个消息框，显示指定颜色的索引值，如图 32.37 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1559_2.png)

## 图 32.37：显示指定颜色的索引值

## 使用 Dictionary<TValue> 类

`Dictionary<TValue>` 类允许您创建存储键值对的泛型集合。您可以使用与之关联的键检索对象。让我们创建一个名为 `GenericDictionarySample` 的应用程序，也可在 CD-ROM 上获得，以了解 `Dictionary<TValue>` 类的使用。该应用程序包含一个示例用户界面表单，其中有三个按钮——`Create and add 10 items`、`ContainsKey` 和 `ContainsValue`，以及一个 `ListView` 控件。

按照以下步骤创建 `GenericDictionarySample` 应用程序：

- 1. 将 `Form1` 的 `Text` 属性设置为 `Generic Dictionary Sample`。
- 2. 将 `ListView`、`GroupBox` 和三个 `Button` 控件拖放到表单上。
- 3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `ContainsKey`，`button3` 设置为 `ContainsValue`。
- 4. 通过在属性窗口中单击 `ListView` 控件的 `Columns` 属性的省略号按钮 `...` 为 `ListView` 控件添加列。`ColumnHeader Collection Editor` 对话框出现。
- 5. 在 `ColumnHeader Collection Editor` 对话框中单击 `Add` 按钮向 `ListView` 控件添加一列。将此列的 `Name` 属性设置为 `Key`，`Text` 属性设置为 `Keys`。同样，为 `ListView` 控件添加另一列，名称设为 `Value`，文本设为 `Values`，然后单击 `OK` 按钮。
- 6. 将清单 32.10 中给出的代码添加到 `GenericDictionarySample` 应用程序的 `Form1.cs` 文件中：

```
Listing 32.10: Showing the Code of the GenericDictionarySample Application

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace GenericDictionarySample
{
    public partial class Form1 : Form
    {
        Dictionary<int, string> dictStr = new Dictionary<int, string>();
        public Form1()
        {
            InitializeComponent();
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            button2.Enabled = false;
            button3.Enabled = false;
        }
        private void button1_Click(object sender, EventArgs e)
        {
            dictStr.Add(100, "White");
            dictStr.Add(101, "Black");
            dictStr.Add(102, "Blue");
            dictStr.Add(103, "Yellow");
            dictStr.Add(104, "Green");
            dictStr.Add(105, "Red");
            dictStr.Add(106, "Orange");
            dictStr.Add(107, "Purple");
            dictStr.Add(108, "Magenta");
            dictStr.Add(109, "Brown");
            LoadDictionary();
            button2.Enabled = true;
            button3.Enabled = true;
        }
        private void LoadDictionary()
        {
            listview1.Items.Clear();
            foreach (object obj in dictStr.Keys)
```

```
{
    ListViewItem lItem = listView1.Items.Add(obj.ToString());
    lItem.SubItems.Add(DictStr[(int)obj]);
}
}
private void button2_Click(object sender, EventArgs e)
{
string tempKey = Microsoft.VisualBasic.Interaction.InputBox("Enter the key to look up", "", "", -1, -1);
if (DictStr.ContainsKey(Convert.ToInt32(tempKey)))
{
    MessageBox.Show("The dictionary contains the specified key");
}
else
{
    MessageBox.Show("The dictionary does not contain the specified key");
}
private void button3_Click(object sender, EventArgs e)
{
string tempKey = Microsoft.VisualBasic.Interaction.InputBox("Enter the value to look up", "", "", -1, -1);
if (DictStr.ContainsValue(tempKey))
{
    MessageBox.Show("The dictionary contains the specified value");
}
else
{
    MessageBox.Show("The dictionary does not contain the specified value");
}
}
}
```
