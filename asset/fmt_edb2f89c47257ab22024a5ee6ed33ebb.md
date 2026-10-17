
在清单 32.10 中，我们创建了一个 `Dictionary<TKey, TValue>` 类的对象 `DictStr`。接下来，在 `button1` 的 `Click` 事件中，我们使用 `Add` 方法向 `DictStr` 对象中添加元素。然后，在 `button2` 和 `button3` 的 `Click` 事件中，我们分别使用 `ContainsKey` 和 `ContainsValue` 方法在 `Dictionary<TKey, TValue>` 对象中搜索元素键或值。

- 7. 按 `F5` 键执行应用程序。表单出现后，单击 `Create and add 10 items` 按钮。`Dictionary<TKey, TValue>` 对象被创建并存储了 10 个元素，`ListView` 控件填充了这些元素，如图 32.38 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1561_0.png)

图 32.38：向 `Dictionary<TKey, TValue>` 对象添加元素

您可以单击 `ContainsKey` 和 `ContainsValue` 按钮来确定键或值是否存在于 `Dictionary<TKey, TValue>` 对象的元素中。

## 使用 SortedDictionary<TKey, TValue> 类

`SortedDictionary<TKey, TValue>` 类是 `Dictionary<TKey, TValue>` 类的排序版本。所有字典集合都允许您创建键值对，其中键与对象关联并用于检索对象。但是，使用 `SortedDictionary<TKey, TValue>` 类时，您将对象添加到集合中时，它们会根据关联的键进行添加和排列。

让我们创建一个名为 `GenericSortedDictionarySample` 的应用程序，也可在 CD-ROM 上获得，以了解 `SortedDictionary<TKey, TValue>` 类的使用。该应用程序包含一个示例用户界面表单，其中有三个按钮——`Create and add 10 items`、`ContainsKey` 和 `ContainsValue`，以及一个 `ListView` 控件。

按照以下步骤创建 `GenericSortedDictionarySample` 应用程序：

- 1. 在 `GenericSortedDictionarySample` 应用程序中将 `Form1` 的 `Text` 属性设置为 `Generic SortedDictionary Sample`。
- 2. 将 `ListView`、`GroupBox` 和三个 `Button` 控件拖放到表单上。
- 3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `ContainsKey`，`button3` 设置为 `ContainsValue`。
- 4. 通过在属性窗口中单击 `ListView` 控件的 `Columns` 属性的省略号按钮 `...` 为 `ListView` 控件添加列。`ColumnHeader Collection Editor` 对话框出现。
- 5. 在 `ColumnHeader Collection Editor` 对话框中单击 `Add` 按钮向 `ListView` 控件添加一列。将此列的 `Name` 属性设置为 `Key`，`Text` 属性设置为 `Keys`。同样，为 `ListView` 控件添加另一列，名称设为 `Value`，文本设为 `Values`，然后单击 `OK` 按钮。
- 6. 将清单 32.11 中给出的代码添加到 `GenericSortedDictionarySample` 应用程序的 `Form1.cs` 文件中：

### 清单 32.11：显示 GenericSortedDictionarySample 应用程序的代码

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

SDictStr.Add(101, "Black");
SDictStr.Add(102, "Blue");
SDictStr.Add(103, "Yellow");
SDictStr.Add(104, "Green");
SDictStr.Add(105, "Red");
SDictStr.Add(106, "Orange");
SDictStr.Add(107, "Purple");
SDictStr.Add(108, "Magenta");
SDictStr.Add(109, "Brown");
LoadSrtdDictionary();
button2.Enabled = true;
button3.Enabled = true;
}
private void LoadSrtdDictionary()
{
    listview1.Items.Clear();
    foreach (object obj in SDictStr.Keys)
    {
        ListviewItem lItem = listview1.Items.Add(obj.ToString());
        lItem.SubItems.Add(SDictStr[(int)obj]);
    }
}
private void button2_Click(object sender, EventArgs e)
{
string tempKey = Microsoft.VisualBasic.Interaction.InputBox("Enter the key to look up", "", "", -1, -1);
if (SDictStr.ContainsKey(Convert.ToInt32(tempKey)))
{
    MessageBox.Show("The sorted dictionary contains the specified key");
}
else
{
    MessageBox.Show("The sorted dictionary does not contain the specified key");
}
}
private void button3_Click(object sender, EventArgs e)
{
string tempKey = Microsoft.VisualBasic.Interaction.InputBox("Enter the value to look up", "", "", -1, -1);
if (SDictStr.ContainsValue(tempKey))
{
    MessageBox.Show("The sorted dictionary contains the specified value");
}
else
{
    MessageBox.Show("The sorted dictionary does not contain the specified value");
}
}
}
```

在清单 32.11 中，我们创建了一个 `SortedDictionary<TKey, TValue>` 类的对象 `SDictStr`。接下来，在 `button1` 的 `Click` 事件中，我们使用 `Add` 方法向 `SDictStr` 对象中添加元素。然后，在 `button2` 和 `button3` 的 `Click` 事件中，我们分别使用 `ContainsKey` 和 `ContainsValue` 方法在 `SDictStr` 对象中搜索元素键或值。

- 7. 按 `F5` 键执行应用程序。表单出现后，单击 `Create and add 10 items` 按钮。`SortedDictionary<TKey, TValue>` 对象被创建并向其中添加了 10 个元素。然后，`ListView` 控件被这些元素填充，如图 32.39 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1564_0.png)

图 32.39：向 `SortedDictionary<TKey, TValue>` 对象添加元素

您可以单击 `ContainsKey` 和 `ContainsValue` 按钮来确定键或值是否存在于 `Dictionary<TKey, TValue>` 对象的元素中。

## 使用 Stack<T> 类

如前所述，`Stack<T>` 类允许您创建集合，其中对象像堆栈一样堆叠，使得最后添加到集合中的对象最先被检索。

让我们创建一个名为 `GenericStackSample` 的应用程序，也可在 CD-ROM 上获得，以学习如何使用 `Stack<T>` 类。该应用程序包含一个示例用户界面表单，其中有三个按钮——`Create and add 10 items`、`Push` 和 `Pop`，以及一个 `ListBox` 控件。

按以下步骤创建 `GenericStackSample` 应用程序：

- 1. 在 `GenericStackSample` 应用程序中将 `Form1` 的 `Text` 属性设置为 `Generic Stack Sample`。
- 2. 将 `ListBox`、`GroupBox` 和三个 `Button` 控件拖放到表单上。
- 3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `Push`，`button3` 设置为 `Pop`。
- 4. 将清单 32.12 中给出的代码添加到 `GenericStackSample` 应用程序的 `Form1.cs` 文件中：

### 清单 32.12：显示 GenericStackSample 应用程序的代码

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace GenericStackSample
{
public partial class Form1 : Form
{
    Stack<string> sStr = new Stack<string>();
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
    SStr.Push("white");
    SStr.Push("black");
    SStr.Push("blue");
    SStr.Push("Yellow");
    SStr.Push("Green");
    SStr.Push("Red");
    SStr.Push("Orange");
    SStr.Push("Purple");
    SStr.Push("Magenta");
    SStr.Push("Brown");
    LoadS();
    button2.Enabled = true;
    button3.Enabled = true;
    }
    private void LoadS()
    {
    listBox1.Items.Clear();
    string[] objArr = SStr.ToArray();
    for (int i = 0; i < SStr.Count; i++)
    {
        listBox1.Items.Add(objArr[i]);
    }
    }
    private void button2_Click(object sender, EventArgs e)
    {
    string tempStr = Microsoft.VisualBasic.Interaction.InputBox("Enter the value for the item to be pushed.", "", "", -1, -1);
    SStr.Push(tempStr);
    LoadS();
    }
    private void button3_Click(object sender, EventArgs e)
    {
    MessageBox.Show(SStr.Pop().ToString(), "Item Popped.");
    LoadS();
    }
}
}
```

在清单 32.12 中，我们创建了一个 `Stack<T>` 类的对象 `SStr`，并在 `button1` 的 `Click` 事件中使用 `Push` 方法向其填充了 10 个元素。接下来，在 `button2` 和 `button3` 的 `Click` 事件中，我们使用 `Push` 和 `Pop` 方法从 `SStr` 对象的开头添加或移除元素。

- 5. 按 `F5` 键执行应用程序。表单出现后，单击 `Create and add 10 items` 按钮。`Stack<T>` 对象被创建并向其中添加了 10 个元素，然后 `ListBox` 控件被这些元素填充，如图 32.40 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1566_0.png)

图 32.40：向 `Stack<T>` 对象添加元素

您可以单击 `Push` 和 `Pop` 按钮来从 `ListBox` 控件中显示的颜色列表顶部添加或移除元素。例如，我们通过单击 `Pop` 按钮从 `ListBox` 控件中移除了 `Brown` 颜色，如图 32.41 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1566_1.png)

图 32.41：移除颜色名称后 `ListBox` 控件的显示

## 使用 Queue<T> 类

`Queue<T>` 类允许您创建集合，其中对象像队列一样排队，使得最先添加到集合中的对象最先被检索。

让我们创建一个名为 `GenericQueueSample` 的应用程序，也可在 CD-ROM 上获得，以学习如何创建 `Queue<T>` 对象并向其中添加元素。该应用程序包含一个示例用户界面表单，其中有三个按钮—`Create and add 10 items`、`Enqueue` 和 `Dequeue`，以及一个 `ListBox` 控件。

按以下步骤创建 `GenericQueueSample` 应用程序：

- 1. 在 `GenericQueueSample` 应用程序中将 `Form1` 的 `Text` 属性设置为 `Generic Queue Sample`。
- 2. 将 `ListBox`、`GroupBox` 和三个 `Button` 控件拖放到表单上。
- 3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `Enqueue`，`button3` 设置为 `Dequeue`。
- 4. 将清单 32.13 中给出的代码添加到 `GenericQueueSample` 应用程序的 `Form1.cs` 文件中：

### 清单 32.13：显示 GenericQueueSample 应用程序的代码
