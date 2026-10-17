
```csharp
class Coin
{
    // 用于表示朝上一面的字段；
    private string sideUp;

    // 构造函数
    public Coin() {
        sideUp = "Heads";
    }

    // Toss 方法模拟抛掷硬币。
    public void Toss() {
        // 创建一个 Random 对象。
        Random rand = new Random();

        // 使用随机数来确定
        // 硬币朝上的哪一面。
        // // 0 = 正面, 1 = 反面
        if (rand.Next(2) == 0) {
            sideUp = "Heads";
        } else {
            sideUp = "Tails";
        }
    }

    // GetSideUp 方法返回
    // sideUp 字段的值。
    public string GetSideUp() {
        return sideUp;
    }
}
```

第一行是类头。它指定了类的名称为 `Coin`。第 2 行和第 37 行的大括号包围了类的内容。让我们仔细查看类内部的内容：

### 第 4 行
该语句声明了一个名为 `sideUp` 的字段。`sideUp` 字段是一个字符串变量，指示硬币的哪一面朝上。如果是正面朝上，则将字符串 `"Heads"` 赋值给该字段。注意，字段声明以关键字 `private` 开始。`private` 关键字是一个访问修饰符，指定该字段不能在类外部直接访问。通过使用 `private` 访问修饰符，类可以向外部代码隐藏其数据。当类的字段对外部代码隐藏时，数据就能防止被损坏。将所有类的字段设为 `private` 并通过方法提供这些访问是一种常用做法。

### 第 7-10 行
这段代码定义了一个特殊的方法——构造函数。构造函数是在对象创建时自动执行的方法。在许多情况下，构造函数用于初始化一个具有初始值的对象字段。此构造函数执行了一个简单的任务。在第 9 行，它将字符串 `"Heads"` 赋值给 `sideUp` 字段。结果是每当我们创建一个 `Coin` 类的对象时，该对象的 `sideUp` 字段最初会被赋值为 `"Heads"`。注意第 7 行中的构造函数头：
- 构造函数的名称与类名相同。
- 构造函数没有返回值。
- 构造函数可以接受参数。

### 第 13-29 行
这段代码定义了 `Toss` 方法。它模拟抛掷硬币。在第 15 行，创建一个 `Random` 对象。在第 18-22 行，使用随机数来确定硬币朝上的哪一面。如果 `rand.Next(2)` 等于 0，则将 `sideUp` 设为 `"Heads"`；否则，设为 `"Tails"`。

### 第 33-36 行
这段代码定义了 `GetSideUp` 方法。它返回 `sideUp` 字段的值。

## 同一源文件中的 Coin 类与 Form1 类

```cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;

namespace Example
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        // Form1's methods and event handlers appear here.
    }

    class Coin
    {
        // Coin class's members appear here.
    }
}
```

Visual Studio 自动化了向项目添加新类的过程。当你准备好编写新类时，按照以下步骤为该类创建源文件：

1. 在 Visual Studio 中打开项目，点击菜单栏上的 `Project`；然后选择 `Add Class....`。如图 5 所示。

图 5 在项目菜单上选择“添加类……”

![](img/9467d25da5679b16515c9401daaae36c_559_0.png)

2. 应该出现图 6 所示的“新建项”。确保选择项类型为 `Class`。注意图中 `Name` 文本框中出现了 `Class1.cs`。这是 Visual Studio 提供的默认文件名。更改名称以匹配你正在创建的类名。

## 类与多表单项目

图 6 “新建项”窗口

![](img/9467d25da5679b16515c9401daaae36c_560_0.png)

匹配你正在创建的类。例如，如果你正在创建一个名为 `Coin` 的类，则将名称更改为 `Coin.cs`。确保文件名以 `.cs` 扩展结尾。

3. 点击 `Add` 按钮。

执行这些步骤后，将在项目中创建指定的源代码文件，并在代码编辑器中显示。该源文件已经包含了几个 `using` 指令和一个你可以编辑的空类定义。图 7 显示了一个示例。你还会在解决方案管理器 `Solution Explorer` 中看到新源文件的条目，如图 8 所示。

## 图 7 在代码编辑器中显示的新类文件

![](img/9467d25da5679b16515c9401daaae36c_560_1.png)

## 类与多表单项目

**图 8** 解决方案管理器窗口

![](img/9467d25da5679b16515c9401daaae36c_561_0.png)

教程 1 将引导你通过应用程序创建 `Coin` 类，该程序用于模拟可以掷出的硬币。

## 教程 1: 创建和使用 Coin 类

在本教程中，你将完成硬币抛掷应用程序。应用程序的功能已经为你创建，如图 9 所示。当你运行应用程序时，可以点击“掷五次”按钮，应用程序将模拟硬币抛掷五次。每次抛掷的结果将显示在列表框中。

**图 9** 硬币抛掷程序的表单

![](img/9467d25da5679b16515c9401daaae36c_561_1.png)

- **步骤 1：** 启动 Visual Studio 或 Visual C#。打开 Student Sample Programs 中 `Chap09` 文件夹下名为 `Coin Toss` 的项目。
- **步骤 2：** 点击 Visual 菜单栏上的 `Project`；选择 `Add Class....`。将出现“新建项”。确保选择项类型为 `Class`。注意默认文件名出现了 `Class1.cs`。如图 10 所示将名称更改为 `Coin.cs`，然后点击 `Add` 按钮。这将向项目添加一个名为 `Coin.cs` 的源文件。
- **步骤 3：** `Coin.cs` 文件现在应显示在代码编辑器中，如图 11 所示。注意文件已包含几个 `using` 指令并创建了一个空类。在 Program 1 中输入第 10-44 行来完成类的命名。

**图 10** 文件名更改为 `Coin.cs`

![](img/9467d25da5679b16515c9401daaae36c_562_0.png)

**图 11** 代码编辑器中的 `Coin.cs` 文件

```csharp
Coin.cs > Form1.cs [Design]
Coin_Toss
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Coin_Toss
{
    class Coin
    {
        // You will add code to the Coin class.
    }
}
```

- **步骤 4：** 接下来，为按钮控件创建 Click 事件处理器。点击代码编辑器上方显示 `Form1.cs [Design]` 的标签页，将视图切换到设计器中的 `Form1` 表单。或者，你可以双击解决方案管理器中的 `Form1.cs` 项。
- **步骤 5：** 在设计器中双击 `Form1.cs`。这将在设计器中打开 `Form1` 表单。

## 将对象传递给方法

当你开发处理对象的应用程序时，通常需要编写接受对象作为参数的方法。例如，以下代码显示了一个名为 `ShowCoinStatus` 方法，它接受一个硬币对象作为参数：

```
private void ShowCoinStatus(Coin coin)
{
    MessageBox.Show("This side of the coin is up: " + 
    coin.GetSideUp());
}
```

以下代码展示了我们如何创建一个 `Coin` 对象并将其作为参数传递给 `ShowCoinStatus` 方法：

```
Coin myCoin = new Coin();
ShowCoinStatus(myCoin);
```

由于类是引用类型，因此类实例的对象总是通过引用传递的。当你将作为类实例的对象作为参数传递时，传递到参数变量的是指向该对象的引用。因此，接收该对象作为参数的方法可以访问实际对象，而不是对象的副本。例如，查看 `Flip` 方法：

```
private void Flip(Coin coin)
{
    coin.Toss();
}
```

该方法接受一个 `Coin` 对象作为参数，并调用该对象的 `Toss` 方法。以下代码演示了该方法的调用：

```
// 创建一个 Coin 对象。
Coin myCoin = new Coin();
// // 这将显示 "Heads"。
MessageBox.Show(myCoin.GetSideUp());
// // 将对象传递给 Flip 方法。
Flip(myCoin);
// // 这可能会显示 "Heads"，也可能
// // 显示 "Tails"。
MessageBox.Show(myCoin.GetSideUp());
```

第 2 行的语句创建了一个由变量 `myCoin` 引用的 `Coin` 对象。第 5 行显示 `myCoin` 对象 `sideUp` 字段的值。由于对象的构造函数将 `sideUp` 字段设置为 `"Heads"`，我们知道第 5 行将显示字符串 `"Heads"`。第 8 行调用了 `Flip` 方法，通过引用将硬币对象作为参数传递。在 `Flip` 方法内部，调用了 `myCoin` 对象的 `Toss` 方法。第 12 行显示 `myCoin` 对象的 `sideUp` 字段的值。这一次，我们无法预测会显示 `"Heads"` 还是 `"Tails"`，因为 `myCoin` 对象的 `Toss` 方法已经被调用。

### 检查点
- 1. 类是如何像蓝图的？
- 2. 简述编写类声明的过程！
- 3. 什么是构造函数？

## 类与多形式项目
- 4. 列出向 Visual C# 项目添加新类文件的三个步骤。
- 5. 当你将作为类实例的对象作为参数传递时，传递到参数变量的是什么？

## 属性

概念：属性是类成员，用于持有关于对象的部分数据。属性实现为特殊的方法，用于设置和获取相应字段的值。

属性是类的一种特殊类型，允许对象存储和检索部分数据。你已经非常熟悉属性了，因为你在创建表单时广泛使用了它们。GUI 控件具有决定其特征的属性。例如，`Label` 控件的 `Text` 属性定义了控件显示的文本。

在代码中，你处理属性的方式与处理变量的方式相同。例如，假设 `messageLabel` 是一个 `Label` 控件的名称。你可以为控件的 `Text` 属性分配一个特定值，如下：

```
messageLabel.Text = "Hello";
```

此外，你也可以将属性赋值给变量。以下语句使用 `messageLabel` 控件的 `Text` 属性初始化变量 `str`：

```
string str = messageLabel.Text;
```

从这些示例中你可以看到属性是一个类似于字段的类成员。然而，它不是公共字段。它是一组特殊的方法，称为访问器 `accessors`，它们与私有字段配合工作。

来看一个带有属性的简单类示例。假设你想创建一个名为 `Pet` 的类来表示家庭宠物。该类将有一个 `Name` 属性来存储宠物的名字。以下代码显示了 `Pet` 类可能的编写方式：

```csharp
class Pet
{
    // 用于存储名字的字段
    private string _name;

    // 构造函数
    public Pet()
    {
        _name = "";
    }

    // Name 属性
    public string Name
    {
        get
        {
            return _name;
        }
        set
        {
            _name = value;
        }
    }
}
```

让我们仔细观察类内部的代码：

第 4 行的语句声明了一个名为 `_name` 的私有字符串字段。`_name` 字段是 `Name` 属性的底层字段。当值赋值给 `Name` 属性时，它存储在 `_name` 字段中。

注意我们在字段开头使用了下划线。这不是强制要求的，但某些程序员会在底层字段名的开头使用下划线，以消除字段和属性之间的混淆。

第 7 行构造函数将 `_name` 字段初始化为空字符串。

第 13 行是属性声明。

第 15-18 行的 `getter` 返回私有 `_name` 字段的值。

第 20-23 行的 `setter` 将新值赋值给私有 `_name` 字段。

# 类与多窗体项目

这种方法是可能的，但不推荐。类字段几乎总是声明为 `private`，以防止它们被意外损坏。当类外部的代码访问字段时，它是通过公共方法，如果是属性，则通过访问器来实现的。这确保了拥有字段的对象对对其进行的所有更改具有控制权。

# 将属性作为参数

你可以将属性作为参数传递给方法。例如，在下面的代码示例第 8 行中，将一个 `Pet` 对象的 `Name` 作为参数传递给 `MessageBox.Show` 方法。

```csharp
// 创建一个 Pet 对象。
Pet myDog = new Pet();

// 设置对象的 Name 属性。
myDog.Name = "Fido";

// 显示 Name 属性。
MessageBox.Show(myDog.Name);
```

当你将属性作为参数传递给方法时，有一个限制：属性只能按值传递。如果你尝试传递 `ref` 或 `out` 参数，将会发生错误。

教程 2 将引导你完成创建一个带有属性的类。你将在一个简单的应用程序中使用该类，该程序创建该类的对象并测试其属性。

#### 教程 2：创建和使用 CellPhone 类

假设你是一家销售手机和无线服务的公司的程序员。你的部门正在创建一个应用程序来管理公司的手机库存。你被要求创建一个表示手机的类。该类应该保留有关手机的以下数据：
- 手机的品牌名称
- 手机的型号
- 手机的零售价格

该类应该具有以下公共属性：
- `Brand`--一个字符串属性，用于存储手机的品牌名称
- `Model`--一个字符串属性，用于存储手机的型号
- `Price`--一个十进制类型 `decimal` 属性，用于存储手机的零售价格

该类应该具有以下私有字段：
- `_brand`--一个字符串，作为 `Brand` 属性的底层字段
- `_model`--一个字符串，作为 `Model` 属性的底层字段
- `_price`--一个十进制类型，作为 `Price` 属性的底层字段

该类还应该有一个构造函数来初始化私有字段。`_brand` 和 `_model` 字段将初始化为空字符串，`_price` 字段将初始化为值 0。

你在一个项目中创建 `CellPhone` 类，该项目会创建该类的对象并测试对象的属性。该项目命名为 `Cell Phone Test` 并且已经为你启动；它位于学生示例程序中的 `Chap09` 文件夹中。图 14 显示了应用程序的表单。在运行时，你在文本框中输入手机数据，然后点击“Create Object”按钮。应用程序创建一个 `CellPhone` 类对象，并将文本框中的数据分配给对象的属性。然后它在 `brandLabel`、`modelLabel` 和 `priceLabel` 控件中渲染并显示对象属性的值。

**图 14** Cell Phone Test 应用程序的表单

![](img/9467d25da5679b16515c9401daaae36c_570_0.png)

- **步骤 1：** 启动 Visual Studio 或 Visual C# Express。打开学生示例程序中 `Chap09` 文件夹中名为 **Cell Phone Test** 的项目。
