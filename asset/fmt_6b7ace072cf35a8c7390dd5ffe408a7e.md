
| `Min` | 检索 `SortedSet<T>` 集合中的最小值，该值由 `comparer` 属性定义。 |

| 表 32.32：`SortedSet<T>` 类值得注意的方法 |

| 方法 | 描述 |

| `Add()` | 将指定的项添加到 `SortedSet<T>` 对象 |

| `Clear()` | 从 `SortedSet<T>` 集合中移除所有元素 |

| `Contains()` | 确定 `SortedSet<T>` 对象是否包含指定的项 |

| `CopyTo()` | 将 `SortedSet<T>` 对象的元素复制到数组中 |

| `IntersectWith()` | 修改当前的 `SortedSet<T>` 对象，使其仅包含同时存在于自身和指定集合中的元素 |

| `IsProperSubsetOf()` | 确定 `SortedSet<T>` 对象是否是指定集合的真子集 |

| `IsProperSupersetOf()` | 确定 `SortedSet<T>` 对象是否是指定集合的真超集 |

| `IsSubsetOf()` | 确定 `SortedSet<T>` 对象是否是指定集合的子集 |

| `IsSupersetOf()` | 确定 `SortedSet<T>` 对象是否是指定集合的超集 |

| `Overlaps()` | 确定当前 `SortedSet<T>` 对象是否与指定集合重叠 |

| `Remove()` | 从 `SortedSet<T>` 对象中移除指定的项 |

| `RemoveWhere()` | 从 `SortedSet<T>` 对象中移除所有与指定条件匹配的元素 |

| `SetEquals()` | 确定 `SortedSet<T>` 对象和指定集合是否包含相同的元素 |

| `SymmetricExceptWith()` | 修改当前的 `SortedSet<T>` 对象，使其仅包含存在于自身或指定集合中但不同时存在于两者中的元素 |

| `UnionWith()` | 修改当前的 `SortedSet<T>` 对象，使其包含同时存在于对象本身和指定集合中的所有元素 |

现在让我们学习泛型中的协变和逆变。

## 泛型中的协变和逆变

在编程语言的类型系统中，协变和逆变是两种使类型能够从窄到宽以及从宽到窄排序的机制。C# 支持对数组类型、委托类型和泛型类型的隐式转换的协变和逆变机制。术语 variance 是指泛型类型定义与其特定泛型类型参数之间的关系。C# 支持以下类型的变体：

- 协变 – 将较窄的类型（例如 `float`）转换为较宽的类型（例如 `double`）
- 逆变 – 将较宽的类型（例如 `double`）转换为较窄的类型（例如 `float`）
- 不变 – 不转换类型的顺序

### NOTE

> 在类型理论中，如果类型 `S` 是类型 `T` 的子类型或派生自 `T` 类型，则类型 `T` 比类型 `S` 更宽或更大（>`）。

以下代码片段显示了对象赋值、协变和逆变之间的区别：

```
// Assignment compatibility.
string mystr = "teststring";
object myobj = mystr;

// Covariance.
IEnumerable<string> strings = new List<string>();
IEnumerable<object> objects = strings;

// Contravariance.
Action<object> actobject = Setobject;
Action<string> actstring = actobject;
```

`.NET Framework 4.0` 引入了一些语言关键字（`out` 和 `in`）来控制协变和逆变机制。`out` 关键字用于协变，以便将类型视为派生程度较低。以下代码片段显示了如何使用协变将字符串的 `IEnumerable` 视为派生程度较窄的对象的 `IEnumerable`：

```
public interface IEnumerable<out T>
{
    IEnumerator<T> GetEnumerator();
}
public interface IEnumerator<out T>
{
    T Current { get; }
    bool MoveNext();
}
// Types can be treated as less derived
IEnumerable<string> strings = GetStrings();
IEnumerable<object> objects = strings;
```

`in` 关键字用于逆变，以便将数组视为派生程度更宽的类型。以下代码片段显示了如何使用逆变：

```
public interface IComparer<in T>
{
    int Compare(T x, T y);
}
// Types can be treated as more derived
IComparer<object> objComp = GetComparer();
IComparer<string> strComp = objComp;
```

请注意，未标记为协变（`out`）或逆变（`in`）的泛型类型参数是不变的。

现在，让我们继续 Immediate Solutions 部分，在该部分中我们将实现 In Depth 部分中描述的概念。

## Immediate Solutions

### 使用集合类

在 In Depth 部分中，您已学习如何处理分组数据，大多数情况下简单的数组就足够了。然而，`.NET` 集合类比数组提供更多功能，例如排序和搜索操作。在本节中，您将学习使用以下类：

- `ArrayList`
- `Hashtable`
- `SortedList`
- `Stack`
- `Queue`
- `BitArray`

让我们一个一个地学习如何使用这些类。

### 使用 ArrayList 类

如 In Depth 部分所述，`ArrayList` 类为数组提供了一个易于使用的替代品。它提供了各种方法，例如 `Sort` 和 `Reverse`，并且允许您动态更改对象的大小。让我们创建一个名为 `ArrayListSample` 的 Windows 窗体应用程序，也可在 CD-ROM 上获得，以学习如何使用 `ArrayList` 类。该应用程序包含一个示例用户界面窗体，其中有三个按钮——Create and add 10 items、`Sort` 和 `Search`，以及一个 `ListBox` 控件。

执行以下步骤以创建并向 `ArrayList` 对象添加元素：

1. 在 `ArrayListSample` 应用程序中，将 `Form1` 的 `Text` 属性设置为 `ArrayList Sample`。
2. 将 `ListBox`、`GroupBox` 和三个 `Button` 控件拖放到窗体上。
3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `Sort`，`button3` 设置为 `Search`。
4. 在 `Form1.cs` 文件中添加 Listing 32.1 中的代码：

#### Listing 32.1: Showing the Code of the ArrayListSample Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Collections;

namespace ArrayList_Sample
{
    public partial class Form1 : Form
    {
        private ArrayList ArrLst;
        public Form1()
        {
            InitializeComponent();
        }

        private void LoadArrList()
        {
            listBox1.Items.Clear();
            for (int i = 0; i < ArrLst.Count; i++)
            {
                listBox1.Items.Add(ArrLst[i]);
            }
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            button2.Enabled = false;
            button3.Enabled = false;
        }
        private void button1_Click(object sender, EventArgs e)
        {
            ArrLst = new ArrayList(10);
            ArrLst.Add("White");
            ArrLst.Add("Black");
            ArrLst.Add("Blue");
            ArrLst.Add("Yellow");
            ArrLst.Add("Green");
            ArrLst.Add("Red");
            ArrLst.Add("Orange");
            ArrLst.Add("Purple");
            ArrLst.Add("Magenta");
            ArrLst.Add("Brown");
            LoadArrList();
            button2.Enabled = true;
            button3.Enabled = true;
        }
        private void button2_Click(object sender, EventArgs e)
        {
            if (ArrLst.Count > 0)
            {
                ArrLst.Sort();
                LoadArrList();
            }
        }
        private void button3_Click(object sender, EventArgs e)
        {
            string tempKey = Microsoft.VisualBasic.Interaction.InputBox("Enter a color to search for", "", "", -1, -1);
            int ArrIndex = ArrLst.BinarySearch(tempKey);
            if (ArrIndex < 0)
            {
                MessageBox.Show("The color does not exist in the list");
            }
            else
            {
                MessageBox.Show("The color " + tempKey + " exists at index : " + ArrIndex);
            }
        }
    }
}
```

在 Listing 32.1 中，我们创建了一个 `ArrayList` 类的集合对象 `ArrLst`。`Add` 方法用于在 `ArrLst` 对象中添加不同颜色的名称。`button1` 的单击事件代码将颜色名称添加到 `ArrLst` 对象中，`button2` 的单击事件对对象的元素进行排序，`button3` 的单击事件在对象中搜索特定颜色名称。

5. 按 `F5` 键执行应用程序。首次加载表单时，注意到 Create and add 10 items 按钮已启用，而其余按钮均被禁用，如图 32.3 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1534_0.png)

### Figure 32.3: Displaying the Output of the ArrayListSample Application

当你点击 Create and add 10 items 按钮时，`ArrayList` 对象中添加的颜色名称会显示在给定的列表框中，如图 32.4 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1534_1.png)

### Figure 32.4: Adding Color Names in a List box

在图 32.4 中，你可以看到 `Sort` 和 `Search` 按钮也已启用。如果点击 `Sort` 按钮，颜色名称将被排序，如图 32.5 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1534_2.png)

### Figure 32.5: Sorting the Colors List

当你点击 `Search` 按钮时，会出现一个输入框，你可以在其中输入要在 `ArrayList` 对象中搜索的颜色名称，如图 32.6 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1535_0.png)

Figure 32.6: Entering a Color Name for Search

图 32.7 显示了在 `ArrayList` 对象中搜索颜色 Blue 的索引值后的消息框：

![](img/e073a4882197be4ab61103cbe0bcb394_1535_1.png)

Figure 32.7: Displaying the Index at which the Item Exists

## Using the Hashtable Class

如前所述，`Hashtable` 类允许你创建存储键值对的集合。使用 `Hashtable` 类，你可以通过与之关联的键检索对象。让我们创建一个名为 `HashtableSample` 的 Windows 窗体应用程序，也可在 CD-ROM 上获得，以了解 `Hashtable` 类的使用方法。该应用程序包含一个用户界面表单，其中有三个按钮--Create and add 10 items、`ContainsKey` 和 `ContainsValue`，以及一个 `ListView` 控件。

执行以下步骤以创建并向 `Hashtable` 对象添加元素：

- 1. 将 `Form1` 的 `Text` 属性设置为 `Hashtable Sample`。
- 2. 将 `ListView`、`GroupBox` 和三个 `Button` 控件拖放到表单上。
- 3. 将 `GroupBox` 控件的 `Text` 属性设置为 `Noteworthy Operations`，并将 `button1` 的 `Text` 属性设置为 `Create and add 10 items`，`button2` 设置为 `Contains Key`，`button3` 设置为 `Contains Value`。
- 4. 通过在属性窗口中点击 `ListView` 控件的 `Columns` 属性的省略号按钮 (...) 来向 `ListView` 控件添加列。`ColumnHeader Collection Editor` 对话框出现（图 32.8）。

5. 点击 `Add` 按钮向 `ListView` 控件添加一列。将该列的 `Name` 属性设置为 `Key`，`Text` 属性设置为 `Keys`。同样地，向 `ListView` 控件添加另一列，名称设为 `Value`，文本设为 `Values`，如图 32.8 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1536_0.png)

### Figure 32.8: Displaying the ColumnHeader Collection Editor Dialog Box

6. 点击 `OK` 按钮关闭 `ColumnHeader Collection Editor` 对话框（图 32.8）。
7. 将 `ListView` 控件的 `View` 属性设置为 `Details`。
8. 在 `HashtableSample` 应用程序的 `Form1.cs` 文件中添加 Listing 32.2 中给出的代码：

### Listing 32.2: Showing the Code of the Form1.cs File of the HashtableSample Application
