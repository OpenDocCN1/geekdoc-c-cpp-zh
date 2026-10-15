

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

在清单 32.9 中，我们创建了一个 SortedList<TKey, TValue> 类的对象 SListStr。接下来，button1 控件的 Click 事件使用 Add 方法向 SListStr 对象中添加元素。接下来，button2 和 button3 控件的 Click 事件分别使用 IndexOfKey 和 IndexOfValue 方法查找指定键或值的索引值。

7. 按 F5 键执行应用程序。表单出现后，单击 Create and add 10 items 按钮。ListView 控件填充了 10 个颜色名称，如图 32.35 所示：

# 第 32 章：集合和泛型

![](img/e073a4882197be4ab61103cbe0bcb394_1559_0.png)

## 图 32.35：向 SortedList<TValue> 对象添加 10 个元素

您可以单击 Index Of Key 按钮和 Index Of Value 按钮分别查找特定键或值的索引值。例如，我们已单击 Index Of Value 按钮来查找 Blue 颜色的索引，如图 32.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1559_1.png)

## 图 32.36：查找 Blue 颜色的索引

会出现一个消息框，显示指定颜色的索引值，如图 32.37 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1559_2.png)

## 图 32.37：显示指定颜色的索引值

## 使用 Dictionary<TValue> 类

Dictionary<TValue> 类允许您创建存储键值对的泛型集合。您可以使用与之关联的键检索对象。让我们创建一个名为 GenericDictionarySample 的应用程序，也可在 CD-ROM 上获得，以了解 Dictionary<TValue> 类的使用。该应用程序包含一个示例用户界面表单，其中有三个按钮——Create and add 10 items、ContainsKey 和 ContainsValue，以及一个 ListView 控件。

按照以下步骤创建 `GenericDictionarySample` 应用程序：

- 1. 将 Form1 的 Text 属性设置为 Generic Dictionary Sample。
- 2. 将 ListView、GroupBox 和三个 Button 控件拖放到表单上。
- 3. 将 GroupBox 控件的 Text 属性设置为 Noteworthy Operations，并将 button1 的 Text 属性设置为 Create and add 10 items，button2 设置为 ContainsKey，button3 设置为 ContainsValue。
- 4. 通过在属性窗口中单击 ListView 控件的 Columns 属性的省略号按钮 (...) 为 ListView 控件添加列。ColumnHeader Collection Editor 对话框出现。
- 5. 在 ColumnHeader Collection Editor 对话框中单击 Add 按钮向 ListView 控件添加一列。将此列的 Name 属性设置为 Key，Text 属性设置为 Keys。同样，为 ListView 控件添加另一列，名称设为 Value，文本设为 Values，然后单击 OK 按钮。
- 6. 将清单 32.10 中给出的代码添加到 GenericDictionarySample 应用程序的 Form1.cs 文件中：

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

在清单 32.10 中，我们创建了一个 Dictionary<TKey, TValue> 类的对象 DictStr。接下来，在 button1 的 Click 事件中，我们使用 Add 方法向 DictStr 对象中添加元素。然后，在 button2 和 button3 的 Click 事件中，我们分别使用 ContainsKey 和 ContainsValue 方法在 Dictionary<TKey, TValue> 对象中搜索元素键或值。

- 7. 按 F5 键执行应用程序。表单出现后，单击 Create and add 10 items 按钮。Dictionary<TKey, TValue> 对象被创建并存储了 10 个元素，ListView 控件填充了这些元素，如图 32.38 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1561_0.png)

图 32.38：向 Dictionary<TKey, TValue> 对象添加元素

您可以单击 ContainsKey 和 ContainsValue 按钮来确定键或值是否存在于 Dictionary<TKey, TValue> 对象的元素中。

## 使用 SortedDictionary<TKey, TValue> 类

SortedDictionary<TKey, TValue> 类是 Dictionary<TKey, TValue> 类的排序版本。所有字典集合都允许您创建键值对，其中键与对象关联并用于检索对象。但是，使用 SortedDictionary<TKey, TValue> 类时，您将对象添加到集合中时，它们会根据关联的键进行添加和排列。

让我们创建一个名为 GenericSortedDictionarySample 的应用程序，也可在 CD-ROM 上获得，以了解 SortedDictionary<TKey, TValue> 类的使用。该应用程序包含一个示例用户界面表单，其中有三个按钮——Create and add 10 items、ContainsKey 和 ContainsValue，以及一个 ListView 控件。

按照以下步骤创建 GenericSortedDictionarySample 应用程序：

- 1. 在 GenericSortedDictionarySample 应用程序中将 Form1 的 Text 属性设置为 Generic SortedDictionary Sample。
- 2. 将 ListView、GroupBox 和三个 Button 控件拖放到表单上。
- 3. 将 GroupBox 控件的 Text 属性设置为 Noteworthy Operations，并将 button1 的 Text 属性设置为 Create and add 10 items，button2 设置为 ContainsKey，button3 设置为 ContainsValue。
- 4. 通过在属性窗口中单击 ListView 控件的 Columns 属性的省略号按钮 (...) 为 ListView 控件添加列。ColumnHeader Collection Editor 对话框出现。
- 5. 在 ColumnHeader Collection Editor 对话框中单击 Add 按钮向 ListView 控件添加一列。将此列的 Name 属性设置为 Key，Text 属性设置为 Keys。同样，为 ListView 控件添加另一列，名称设为 Value，文本设为 Values，然后单击 OK 按钮。
- 6. 将清单 32.11 中给出的代码添加到 GenericSortedDictionarySample 应用程序的 Form1.cs 文件中：

## 清单 32.11：显示 GenericSortedDictionarySample 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace GenericSortedDictionarySample
{
public partial class Form1 : Form
{
    SortedDictionary<int, string> SDictStr = new SortedDictionary<int, string>();
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
        SDictStr.Add(100, "white");
```

