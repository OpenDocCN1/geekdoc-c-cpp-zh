
## 4. Add the code given in Listing 32.15 to the Form1.cs file of the GenericHashSetSample application:

### Listing 32.15: Showing the Code of the GenericsSample Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace GenericsSample
{
    public partial class Form1 : Form
    {
        private MyGenericCollection<Arithmetic> MGColA;
        public Form1()
        {
            InitializeComponent();
        }
        private void Button1_Click(object sender, EventArgs e)
        {
            if (((Button)sender).Text == "Release All")
            {
                ((Button)sender).Text = "Add Items";
                listBox1.Items.Clear();
```

```
TextBox1.Text = "";

Button3.Enabled = false;

Button2.Enabled = false;

Button4.Enabled = false;

ReleaseAll();

}

else

{

    ((Button)sender).Text = "Release All";

    Button3.Enabled = true;

    Button2.Enabled = true;

    Button4.Enabled = true;

    DoDeclaration();

}

}

private void Button2_Click(object sender, EventArgs e)

{

    Arithmetic objA1 = MGC01A.GetItems(0);

    Arithmetic objA2 = MGC01A.GetItems(1);

    TextBox1.Text = Sum(objA1, objA2);

}

private void Button3_Click(object sender, EventArgs e)

{

    if (listBox1.SelectedIndices.Count != 0)

    {

        TextBox1.Text = "";

        foreach (int indice in listBox1.SelectedIndices)

        {

            TextBox1.Text += MGC01A.GetItems(indice);

        }

    }

    else

    {

        MessageBox.Show("Please select some items in the listboxes first.");

    }

}

private void Button4_Click(object sender, EventArgs e)

{

    object tempval = Microsoft.VisualBasic.Interaction.InputBox("Value to Look up", "", 1, -1, -1);

    int tempIndex = 0;

    tempIndex = MGC01A.ContainsValue(new Arithmetic(Convert.ToInt32(tempval)));

    MessageBox.Show((tempIndex == -1) ? "The collection does not contain the specified value" : "The collection contains the specified value at index " + tempIndex.ToString());

}

private void ReleaseAll()

{

    MGC01A = null;

    GC.Collect();

}

private void DoDeclaration()

{

    MGC01A = new MyGenericCollection<Arithmetic>(4);

    MGC01A.SetItems(0, new Arithmetic(1000));
```

```
MGColA.SetItems(1, new Arithmetic(2000));
MGColA.SetItems(2, new Arithmetic(3000));
MGColA.SetItems(3, new Arithmetic(4000));
MGColA.SetItems(4, new Arithmetic(5000));
for (int i = 0; i <= 4; i++)
{
    listBox1.Items.Add(MGColA.GetItems(i));
}
}
public string Sum<T>(T val1, T val2) where T : IBase
{
    return val1.AddIt(val2);
}

public void Display<T>(T val1)
{
    MessageBox.Show(val1.ToString());
}
}
public interface IBase
{
    string AddIt(IBase obj1);
}
public class MyGenericCollection<Tp>
{
    private Tp[] Arr;
    public MyGenericCollection(int size)
    {
        Arr = new Tp[size + 1];
    }
    public Tp GetItems(int index)
    {
        return Arr[index];
    }
    public void SetItems(int index, Tp value)
    {
        Arr[index] = value;
    }
    public int ContainsValue(Tp obj)
    {
        for (int i = 0; i < Arr.Length; i++)
        {
            if (((IEquatable<IBase>)Arr[i]).Equals(obj))
            {
                return i;
            }
        }
        return -1;
    }
}
public class Arithmetic : IEquatable<IBase>, IBase
{
    private int nm;
    public Arithmetic()
    {
        nm = 0;
    }
    public Arithmetic(int Number)
{
    nm = Number;
}
public override bool Equals(object obj)
{
    Arithmetic bobj = obj as Arithmetic;
    return bobj != null && Equals(bobj);
}
public bool Equals(IBase oth)
{
    return oth != null && nm == ((Arithmetic)oth).nm;
}
public string AddIt(IBase obj1)
{
    return ((int)this.Number + (int)((Arithmetic)obj1).Number).ToString();
}
public static string operator +(string obj1, Arithmetic obj2)
{
    if (obj1 != "")
    {
        return (Convert.ToInt32(obj1) + (int)obj2.Number).ToString();
    }
    return obj2.Number.ToString();
}
public static string operator +(Arithmetic obj1, Arithmetic obj2)
{
    if (obj1 != null)
    {
        return (((int)obj1.Number + (int)obj2.Number).ToString();
    }
    return obj2.Number.ToString();
}
public override string ToString()
{
    return nm.ToString();
}
public object Number
{
    get
    {
        return nm;
    }
    set
    {
        nm = (int)value;
    }
}
```

在清单 32.15 中，一个名为 `Arithmetic` 的类实现了 `IEquatable<IBase>` 和 `IBase` 接口。接下来，创建了一个名为 `MyGenericCollection<Arithmetic>` 的用户定义泛型类及其对象 `MGColA`。`button1` 控件的 `Click` 事件会添加 `MGColA` 对象中的元素。`button2` 的 `Click` 事件使用 `Sum` 泛型方法并将 `MGColA` 对象中前两个元素存储的数字相加。`button3` 控件的 `Click` 事件会将 `MGColA` 对象中指定元素存储的数字相加。最后，`button4` 的 `Click` 事件会显示应用程序执行时指定的元素的索引值。

## 5. 按 `F5` 键执行应用程序。在输出中，您可以看到 Generics Sample 窗口，如图 32.47 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1575_0.png)

### 图 32.47：显示 Generics Sample 窗口

+ 6. 单击 Add Items 按钮在 Integer Collection 列表框中添加项目，如图 32.48 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1575_1.png)

### 图 32.48：在 Integer Collection 列表框中添加项目

您可以单击 Add First Two 按钮来添加前两个数字，或单击 Add All Selected 按钮来添加在 Integer Collection 列表框中显示的所选数字。结果数字将显示在 Addition Results 文本框中。图 32.49 显示了通过单击 Add All Selected 按钮添加所选数字的结果：

![](img/e073a4882197be4ab61103cbe0bcb394_1575_2.png)

### 图 32.49：显示所选数字的和

此外，您可以单击 Search in Collection 按钮来搜索特定数字的索引号。例如，我们已搜索数字 4000 的索引号，如图 32.50 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1576_0.png)

### 图 32.50：搜索值的索引号

现在，结果显示如下，如图 32.51 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1576_1.png)

### 图 32.51：显示值的索引号

4000 的索引号为 3，因为索引号从零开始。

让我们学习如何在泛型中实现协变和逆变。

## 在泛型中实现协变和逆变

在本节中，您将学习如何创建一个名为 `GenericContravarianceCovariance` 的控制台应用程序，该应用程序也可在 CD-ROM 上获得，以了解 C# 泛型类中使用协变和逆变的用法。

### 清单 32.16：显示 GenericContravarianceCovariance 应用程序的 Program.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace GenericContravarianceCovariance
{
    class Vehicle { }
    class Car : Vehicle { }
    class Program
    {
        delegate T Func1<out T>();
        delegate void Action1<in T>(T a);
        static void Main(string[] args)
        {
            Func1<Car> c = () => new Car();
            Func1<Vehicle> vehi = c;

            Action1<Vehicle> v2 = (vehi2) => { Console.WriteLine(vehi2); };
            Action1<Car> c1 = v2;
        }
    }
}
```

```
Console.WriteLine(vehi());
c1(new Car());
}
}
```

在清单 32.16 中，`Vehicle` 是基类，`Car` 是其派生类。接下来，声明了一个返回类型 `T` 的委托。接下来，将 `T` 初始化为类型 `Car` 并将其分配给创建一个名为 `c` 的实例并返回它的 lambda。这意味着我们可以将 `c` 对象分配给返回 `Vehicle` 对象的委托。类型参数中的 `out` 关键字表示协变，而类型参数中的 `in` 关键字表示逆变。

按 `CTRL+F5` 键组合执行 `GenericContravarianceCovariance` 应用程序。图 32.52 显示了清单 32.16 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1577_0.png)

### 图 32.52：显示 GenericContravarianceCovariance 应用程序的输出

现在，让我们总结本章讨论的主要主题。

## 摘要

在本章中，您已学习了 C# 中的集合和泛型。本章从集合的概念和各种集合类开始，例如 `ArrayList`、`Hashtable`、`Stack` 和 `Queue`。接下来，您学习了 C# 中的泛型。您还学习了各种泛型类，例如 `List<T>`、`Dictionary<TKey, TValue>` 和 `HashSet<T>`。此外，您还学习了泛型中的协变和逆变机制。在 Immediate Solutions 部分，您学习了如何在 C# 应用程序中实现集合和泛型。

在下一章中，您将学习 .NET 程序集、程序集的组件、程序集的类型以及这些程序集的各种属性和强名称。

## 33

## .NET 程序集

| 如果您需要立即解决以下问题： | 请参见页码： |
|---|---|
| 创建共享程序集 | 1549 |
| 创建简单客户端 | 1551 |
| 创建共享程序集的新版本 | 1552 |
| 创建私有程序集 | 1556 |
| 创建多文件程序集 | 1557 |
| 原生映像生成 | 1560 |
| 延迟签名 | 1561 |
| 配置程序集查找 | 1562 |
| 创建发布者策略 | 1566 |

![](img/e073a4882197be4ab61103cbe0bcb394_1578_0.png)

## 深入探讨

程序集可以定义为部分编译的代码库，由有关应用程序的所有信息或元数据组成，例如其名称、版本号、模块、资源文件和代码文件。存储在程序集中的元数据是部署应用程序所必需的；因此，程序集也被称为部署的基本单元。在 .NET 中，程序集中有关应用程序的元数据由一个或多个可执行文件（EXE）或动态链接库（DLL）文件表示。与 Microsoft 中间语言（MSIL）代码相比，程序集可以存储更多信息，MSIL 代码由公共语言运行时（CLR）编译和运行。事实上，程序集可以被视为一个或多个模块和类编译为 MSIL、描述程序集本身的元数据以及程序集类的功能的集合。根据您创建的应用程序类型，.NET Framework 允许您创建静态或动态程序集。静态程序集以便携式可执行（PE）文件的形式永久存储在磁盘上；而动态程序集可以直接从内存运行，并在执行前不会保存到磁盘。执行后，您可以将动态程序集保存到磁盘。

在本章中，我们首先讨论程序集的概念和组件。在后面的部分中，我们将讨论不同类型的程序集、程序集属性、程序集签名、程序集存储、程序集信息文件和程序集配置文件。让我们从探索 .NET 程序集的概念开始。

## .NET 程序集
