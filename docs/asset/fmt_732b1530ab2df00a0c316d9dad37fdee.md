
```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Collections;

namespace HashtableSample
{
    public partial class Form1 : Form
    {
        private Hashtable HTbl;
        public Form1()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, EventArgs e)
        {
            HTbl = new Hashtable(10);
            HTbl.Add(100, "white");
            HTbl.Add(101, "black");
            HTbl.Add(102, "blue");
            HTbl.Add(103, "yellow");
            HTbl.Add(104, "green");
            HTbl.Add(105, "red");
            HTbl.Add(106, "orange");
            HTbl.Add(107, "purple");
            HTbl.Add(108, "magenta");
HTbl.Add(109, "Brown");
LoadHshTable();
button2.Enabled = true;
button3.Enabled = true;
}
private void Form1_Load(object sender, EventArgs e)
{
    button2.Enabled = false;
    button3.Enabled = false;
}
private void LoadHshTable()
{
    listview1.Items.Clear();
    foreach (object obj in HTbl.Keys)
    {
        ListviewItem lItem = listview1.Items.Add(obj.ToString());
        lItem.SubItems.Add(HTbl[obj].ToString());
    }
}
private void button2_Click(object sender, EventArgs e)
{
string tempKey = Microsoft.VisualBasic.Interaction.InputBox("Enter the key to look up", "", "", -1, -1);
if (HTbl.ContainsKey(Convert.ToInt32(tempKey))) {
    MessageBox.Show("The hashtable contains the specified key");
}
else
{
    MessageBox.Show("The hashtable does not contain the specified key");
}
}
private void button3_Click(object sender, EventArgs e)
{
string tempValue = Microsoft.VisualBasic.Interaction.InputBox("Enter the value to look up", "", "", -1, -1);
if (HTbl.ContainsValue(tempValue))
{
    MessageBox.Show("The hashtable contains the specified value");
}
else
{
    MessageBox.Show("The hashtable does not contain the specified value");
}
}
}
```

在 Listing 32.2 中，使用`Add`方法向`Hashtable`类的对象添加键/值对。`Add`方法接受两个参数，第一个为键，第二个为值。这两个参数可以是任何类型；并且无论将何种类型的数据添加到集合中，所有元素都以相同的方式添加到集合中。`button1`的`Click`事件使用`Hashtable`类的`Add`方法向集合添加具有键/值对的元素。`button2`的`Click`事件使用`ContainsKey`方法确定`Hashtable`对象是否包含特定键。如果`Hashtable`对象包含指定的键，则该方法返回`true`；否则返回`false`。同样，`button3`的`Click`事件使用`ContainsValue`方法确定`Hashtable`对象是否包含特定值。该方法也返回`true`或`false`值。

## NOTE

你需要在项目中添加`Microsoft.VisualBasic`程序集的引用以便于使用输入框。

9. 按`F5`键执行应用程序。当表单出现时，点击 Create and add 10 items 按钮。`ListView`控件会填充 10 个颜色名称及其键值，如图 32.9 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1538_0.png)

### Figure 32.9: Creating and Adding 10 Elements to the Hashtable Object

当你点击`ContainsKey`按钮时，会出现一个输入框提示你输入要检查的键。你可以输入一个键并点击`OK`按钮，如图 32.10 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1538_1.png)

### Figure 32.10: Displaying the Prompt for Searching a Key

如果在`Hashtable`对象中找到该键，则会出现一个消息框并确认指定键的存在，如图 32.11 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1538_2.png)

### Figure 32.11: Displaying a Message Box to Confirm the Presence of a Key

同样，你可以通过点击`ContainsValue`按钮来搜索颜色名称。图 32.12 显示了一个输入框，提示你在`Hashtable`对象中输入要搜索的值：

### Figure 32.12: Displaying the Prompt for Searching a Value

在我们的例子中，我们输入了`Blue`颜色名称并点击了`OK`按钮。然后出现一个消息框，指示该值存在，如图 32.13 所示：

### Figure 32.13: Displaying a Message Box to Confirm the Presence of a Value

## Using the SortedList Class

`SortedList`类允许你创建键值对的集合。让我们创建一个名为`SortedListSample`的应用程序，也可在 CD-ROM 上获得，以学习如何使用`SortedList`类。该应用程序包含一个示例用户界面表单，其中有三个按钮--Create and add 10 items、Index of Key 和 Index of Value，以及一个`ListView`控件。

执行以下步骤以创建并向`SortedList`对象添加元素：

- 1. 将`Form1`的`Text`属性设置为 SortedList Sample。

- 2. 将`ListView`、`GroupBox`和三个`Button`控件拖放到表单上。

- 3. 将`GroupBox`控件的`Text`属性设置为 Noteworthy Operations，并将`button1`的`Text`属性设置为 Create and add 10 items，`button2`设置为 Index of Key，`button3`设置为 Index of Value。

- 4. 通过在属性窗口中点击`ListView`控件的`Columns`属性的省略号按钮 (...) 来向`ListView`控件添加列。ColumnHeader Collection Editor 对话框出现。

- 5. 点击`Add`按钮向`ListView`控件添加一列。将该列的`Name`属性设置为`Key`，`Text`属性设置为`Keys`。同样向`ListView`控件添加另一列，名称设为`Value`，文本设为`Values`，然后在 ColumnHeader Collection Editor 对话框中点击`OK`按钮。

- 6. 将`ListView`控件的`View`属性设置为`Details`。

- 7. 在`SortedListSample`应用程序的`Form1.cs`文件中添加 Listing 32.3 中给出的代码：

### Listing 32.3: Showing the Code of the SortedListSample Application

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

using System.Collections;

namespace SortedListSample

{

    public partial class Form1 : Form

    {

        private SortedList SLst;

        public Form1()

        {

            InitializeComponent();

        }

        private void button1_Click(object sender, EventArgs e)

        {

            SLst = new SortedList(10);

            SLst.Add(100, "White");

            SLst.Add(101, "Black");

            SLst.Add(102, "Blue");

            SLst.Add(103, "Yellow");

            SLst.Add(104, "Green");

            SLst.Add(105, "Red");

            SLst.Add(106, "Orange");

            SLst.Add(107, "Purple");

            SLst.Add(108, "Magenta");

            SLst.Add(109, "Brown");

            LoadSrtList();

            button2.Enabled = true;

            button3.Enabled = true;

        }

        private void LoadSrtList()

        {

            for (int i = 0; i < SLst.Count; i++)

            {

                listview1.Items.Add(SLst.GetKey(i).ToString());

                listview1.Items[i].SubItems.Add(SLst[SLst.GetKey(i)].ToString());

            }

        }

        private void Form1_Load(object sender, EventArgs e)

        {

            button2.Enabled = false;

            button3.Enabled = false;

        }

        private void button2_Click(object sender, EventArgs e) {

        string tempkey = Microsoft.VisualBasic.Interaction.InputBox("Enter the key to find the index of", "", "", -1, -1);

        int tempindex = SLst.IndexOfKey(Convert.ToInt32(tempKey));

        if (tempindex < 0)

        {

            MessageBox.Show("The key does not exist in the sortedlist.");

        }

        else

        {

            MessageBox.Show("The key in the sortedlist has an index : " + tempindex + ".");

        }

        }

        private void button3_Click(object sender, EventArgs e)

        {

        string tempvalue = Microsoft.VisualBasic.Interaction.InputBox("Enter the value to find the index of", "", "", -1, -1);

int tempindex = SLst.IndexOfValue(tempvalue.ToString());

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

在清单 32.3 中，使用了`Add`方法向集合添加键/值对。`button1`的`Click`事件使用`Add`方法向集合添加具有键/值对的元素。`button2`的`Click`事件使用`IndexOfKey`方法从集合中检索指定键的索引。类似地，`button3`的`Click`事件使用`IndexOfValue`方法检索特定值的索引。

8. 按`F5`键执行应用程序。当窗体出现时，单击 Create and add 10 items 按钮。`ListView`控件会填充 10 个颜色名称及其键值，如图 32.14 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1541_0.png)

### 图 32.14：向 SortedList 对象创建并添加 10 个元素

当您单击 Index of Key 按钮时，会出现一个输入框，提示您输入要查找其索引的键，如图 32.15 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1541_1.png)

### 图 32.15：显示用于搜索键索引的输入框

会出现一个消息框，显示`SortedList`对象中指定键的索引值，如图 32.16 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1542_0.png)

### 图 32.16：显示消息框以显示键的索引

类似地，您可以通过单击 Index Of Value 按钮来查找颜色名称的索引值。图 32.17 显示了一个输入框，提示您输入颜色名称以查找其在`SortedList`对象中的索引值：

![](img/e073a4882197be4ab61103cbe0bcb394_1542_1.png)

### 图 32.17：显示用于搜索值索引的输入框

在我们的例子中，我们输入了`Purple`颜色名称并单击了`OK`按钮。然后会出现一个消息框，显示所输入颜色名称的索引值，如图 32.18 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1542_2.png)

### 图 32.18：显示消息框以显示颜色名称的索引

## 使用 Stack 类

`Stack`类允许您创建集合，其中对象像堆栈一样堆叠，使得最后添加到集合中的对象最先被检索。让我们创建一个名为`StackSample`的 Windows 窗体应用程序，也可在 CD-ROM 上获得，以了解`Stack`类的使用。该应用程序包含一个示例用户界面窗体，其中有三个按钮——Create and add 10 items、Push 和 Pop，以及一个`ListBox`控件。

按照以下步骤创建 StackSample 应用程序：

- 1. 在`StackSample`应用程序中将`Form1`的`Text`属性设置为 Stack Sample。

- 2. 将`ListBox`、`GroupBox`和三个`Button`控件拖放到窗体上。
