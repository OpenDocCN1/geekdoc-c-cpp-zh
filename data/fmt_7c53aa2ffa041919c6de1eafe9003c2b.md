
有时你需要执行同一种操作的不同方式。例如，你在教程 3 中编写的 `BankAccount` 类有一个接受 `decimal` 参数的 `Deposit` 方法。假设你正在一个应用程序中使用该类，但需要向方法传递 `double` 变量而不是 `decimal` 变量。在此应用程序中，调用 `Deposit` 方法之前，你必须将 `double` 变量转换为 `decimal` 以便传递给方法。如果 `Deposit` 方法既能接受 `decimal` 参数又能接受 `double` 参数就好了。这样在传递给方法时就不需要转换 `double` 变量。这可以通过重载来实现。

当方法被重载时，意味着同一个类中的多个方法具有相同的名称但使用不同类型的参数。以下是在 `BankAccount` 类中重载 `Deposit` 方法的示例：

```csharp
// 存款方法
public void Deposit(decimal amount)
{
    balance += amount;
}

// 重载的 Deposit 方法
public void Deposit(double amount)
{
    balance += (decimal)amount;
}
```

# 重载构造函数

构造函数也可以被重载，这意味着同一个类中的多个方法具有相同的名称但使用不同类型的参数。以下是我们在 `BankAccount` 类中重载构造函数的示例：

```csharp
// 标准构造函数
public BankAccount(decimal startingBalance)
{
    balance = startingBalance;
}

// 重载的构造函数
public BankAccount(double startingBalance)
{
    balance = (decimal)startingBalance;
}
```

# 类与多界面项目

```cs
phones[index] = new CellPhone();
}
```

或者，你也可以在声明语句中初始化数组元素：

```cs
Cellphone[] phones = {
    new CellPhone(), new CellPhone(),
    new CellPhone(), new CellPhone()
};
```

下面显示另一个示例。此代码通过指向四个 `BankAccount` 对象的引用初始化其元素。

```cs
BankAccount[] accounts = {
    new BankAccount(1000),
    new BankAccount(2000),
    new BankAccount(3000),
    new BankAccount(4000)
};
```

这是传递给每个对象的 `BankAccount` 构造函数的参数。如果执行该代码，它将显示“The balance is 1000”、“The balance is 2000”等：

```cs
for (int index = 0; index < accounts.Length; index++) {
    MessageBox.Show("The balance is " + accounts[index].Balance);
}
```

以下代码使用 `foreach` 循环执行相同的操作：

```cs
foreach (BankAccount account in accounts) {
    MessageBox.Show("The balance is " + account.Balance);
}
```

# 类类型对象的列表

`List` 类是一个用于存储对象集合的容器。下面是如何创建一个可以包含 `CellPhone` 的 `List` 的示例：

```cs
List<CellPhone> phoneList = new List<CellPhone>();
```

该语句创建了一个由 `phoneList` 变量引用的 `List` 对象。注意 `CellPhone` 一词写在括号 `<>` 内，紧跟在 `List` 单词之后。这指定了 `List` 只能持有 `CellPhone` 类类型的对象。

要向列表添加对象，请使用 `Add` 方法。以下代码显示了一个示例：

```cs
// 创建一个用于存放 CellPhone 对象的 List。
List<CellPhone> phoneList = new List<CellPhone>();

// 创建 CellPhone 类的实例。
CellPhone phone = new CellPhone();

// 给对象的属性赋值。
phone.Brand = "Acme Electronics";
myPhone.Model = "M1000";
myPhone.Price = 199;

// 将对象添加到 List。
phoneList.Add(myPhone);
```

第 2 行的语句创建了一个名为 `phoneList` 的可以持有 `CellPhone` 对象的 `List`。

第 5 行创建一个 `CellPhone` 类的实例，由 `myPhone` 变量引用。

第 8–10 行给对象的属性赋值。第 13 行将对象添加到 `List`。

在教程 4 中，你完成了一个使用 `List` 存放 `CellPhone` 对象集合的应用程序。

# 教程 4：完成手机库存应用程序

在本节中，你将完成手机库存应用程序。图 16 显示了已完成的应用程序表单，该表单已经为你创建好了。当你运行应用程序时，你可以在 `TextBox` 控件中输入手机数据。当你点击 `Add` 按钮时，这些数据会被分配给 `CellPhone` 对象的属性，然后该对象被添加到 `List` 中。你可以根据需要多次执行此操作。每当你添加手机手机，其品牌和型号都会显示在列表框中。如果你在列表中框选择一个手机，应用程序将显示该手机的价格。

**图 16** 手机库存应用程序表单

![](img/9467d25da5679b16515c9401daaae36c_583_0.png)

图 17 显示了应用程序运行时的示例。图中已添加了五部手机，并在列表框中选择了 `Atlantic Mobile S2`。所选手机的价格显示在消息框中。

**图 17** 手机库存应用程序表单

![](img/9467d25da5679b16515c9401daaae36c_583_1.png)

# 类与多界面项目

- 步骤 1：启动 Visual Studio（或 Visual C# Express）。打开学生示例程序中 `Chap09` 文件夹下名为 `Cell Phone Inventory` 的项目。注意 `CellPhone` 类已经通过 `CellPhone.cs` 为你添加到了项目中。

- 步骤 2：在代码编辑器中打开 `Form1.cs` 文件。编写 `phoneList` 的注释和声明，这出现在程序 7 的第 14 和第 15 行。注意 `phoneList` 被声明为 `Form1` 类中的一个字段。它对类中的所有方法可用。

- 步骤 3：输入 `GetPhoneData` 方法的注释和代码，位于程序 7 的第 22–46 行。注意 `GetPhoneData` 接受一个 `CellPhone` 对象作为参数。`GetPhoneData` 方法目的是读取用户输入表单文本框的数据并将这些数据存储在对象的属性中。（这个方法看起来可能熟悉。我们在教程 2 中用过它。）

- 步骤 4：在设计器中切换到 `Form1` 并双击 `addButton` 控件。打开代码编辑器，你将看到一个名为 `addButton_Click` 的事件处理器。通过输入程序 7 中第 50–69 行的代码来完成该事件处理器。让我们来看代码：

第 51 行：该语句创建了一个由 `myPhone` 引用的 `CellPhone` 对象。

第 54 行：该语句调用了 `GetPhoneData` 方法，并将 `myPhone` 作为参数传递。

第 57 行：该语句将 `myPhone` 添加到 `phoneList`。

第 60–61 行：这些语句设置了属性。

第 64–66 行：这些语句清空 `TextBox` 控件的内容。

第 69 行：该语句将焦点置于 `brandText`。注意添加到 `phoneList` 的每个 `CellPhone` 都有对应的项。

- 步骤 5：为 `phoneListBox` 创建索引事件。回到设计器并双击 `phoneListBox` 控件。在代码编辑器中，你将看到 `SelectedIndexChange` 事件处理器。通过输入程序 7 中第 74–78 行的代码完成事件处理器。我们在步骤 4 中提到列表框中的项是通过索引相关的。当用户从列表中选择项目时，我们只需要获取该索引并使用相同的索引从 `phoneList` 获取对象。

- 步骤 6：回到设计器并双击 `exitButton` 控件。在编辑器中你将看到空的 `exitButton.Click` 事件处理器。通过输入程序 7 中第 83–84 行所示的代码完成事件处理器。

- 步骤 7：保存项目。然后，按下键盘上的 `[F5]` 或点击工具栏上的启动调试按钮来编译并运行应用程序。当应用程序运行时，在 `TextBox` 控件中输入一些数据并点击 `Add` 按钮。重复此操作输入几组数据。每次你添加手机，都应该在列表中看到它的品牌和型号。当你输入了多部手机的数据后，点击列表中的项查看每部手机的价格。完成后点击 `Exit` 按钮。

程序 7 手机库存应用程序中 `Form1` 的完成代码

```cs
1 using System;
2 using System.Collections.Generic;
3 using System.ComponentModel;
4 using System.Data;
5 using System.Drawing;
6 using System.Linq;
7 using System.Text;
8 using System.Windows.Forms;
9
10 namespace Cell_Phone_Inventory
11 {
12 public partial class Form1 : Form
13 {
14 // 用于存放 CellPhone 对象的 List
15 List<CellPhone> phoneList = new List<CellPhone>();

16 public Form1()
InitializeComponent();

// GetPhoneData 方法接受一个 CellPhone 对象
// 作为参数。它将用户输入的数据赋值给
// 对象的属性。
private void GetPhoneData(CellPhone phone)
// 用于存储价格的临时变量。
decimal price;
// 获取手机的品牌。
phone.Brand = brandText.Text;
// 获取手机的型号。
phone.Model = modelTextBox.Text;
// 获取手机的价格。
if (decimal.TryParse(priceTextBox.Text, out price))
phone.Price = price;
}
}
}
```

# 类与多形式项目

```csharp
else 
{
    // 显示错误消息。
    MessageBox.Show("Invalid price");
}

private void addButton_Click(object sender, EventArgs e)
{
    // 创建一个 CellPhone 对象。
    CellPhone myPhone = new CellPhone();

    // 获取手机数据。
    GetData(myPhone);

    // 将 CellPhone 对象添加到列表。
    phoneList.Add(myPhone);

    // 向列表框中添加一个项。
    phoneList.Items.Add(myPhone.Brand + " " + myPhone.Model);

    // 清空 TextBox 控件。
    brandTextBox.Clear();
    modelTextBox.Clear();
    priceTextBox.Clear();

    // 重置焦点。
    brandTextBox.Focus();
}

private void phoneList_SelectedIndexChanged(object sender, EventArgs e)
{
    // 获取选中项的索引。
    int index = phoneList.SelectedIndex;

    // 显示选中项的价格。
    MessageBox.Show(phoneList[index].Price.ToString("c"));
}

private void exitButton_Click(object sender, EventArgs e)
{
    // 关闭表单。
    this.Close();
}
```

![](img/9467d25da5679b16515c9401daaae36c_586_0.png)

### 检查点

- 当你创建一个类类型的数组时，数组的每个元素将用什么值初始化？

- 你如何使用指向类对象的引用来初始化类类型的数组？

- 你如何指定 List 可以包含的类类型？

# 在问题中寻找类及其职责

在开发面向对象的程序时，你的首要任务之一是识别你需要创建的类。通常，你的目标是识别问题中存在的不同类型的现实世界对象，然后在应用程序中为这些类型的对象创建类。

多年来，软件专业人员开发了许多在给定问题中寻找类的技术。一种简单且流行的技术涉及以下步骤：

1. 获取关于该领域的的书面描述。

2. 识别描述中所有的名词（包括代词和名词短语）。每一个名词都是一个潜在的类。

3. 精炼列表，只包含与问题相关的类。

让我们详细查看这些步骤中的每一步。

# 编写问题领域的描述

问题领域是与问题相关的现实世界对象、参与方重大事件的集合。如果你充分理解你正在尝试解决的问题本质，你可以自己编写问题领域的描述。如果你不彻底理解问题的本质，那么你应该让专家为你编写该描述。

例如，假设我们正在为 Joe 的汽车修理店编写一个管理程序，为客户打印服务报价。以下是由专家（可能是 Joe 本人）编写的描述：

> Joe 的汽车修理店负责汽车维修，专门负责奔驰、保时捷和宝马汽车。当客户把汽车带到店里时，经理获取客户的姓名、地址和电话号码。经理确定汽车的品牌、型号和年份，并给客户提供服务报价。服务报价显示了预计的零件费用、预计的工费、销售税和总预估费用。

问题描述应该包含以下任何内容：

- 物理对象，如车辆、机器或产品

- 人所扮演的角色，例如经理、员工、客户、学生等

- 业务事件的结果，例如客户订单，或在本例中为服务报价

- 记录维护项，例如客户历史和薪资记录

# 识别所有名词

下一步是识别所有的名词和名词短语。（如果描述中包含代词，也请包含它们。）这里再次查看之前的问题描述——这次名词和名词短语以粗体显示。

> Joe 的汽车修理店负责汽车维修，专门负责奔驰、保时捷和宝马汽车。当客户把汽车带到店里时，经理获取客户的姓名、地址和电话号码。经理确定汽车的品牌、型号和年份，并给客户提供服务报价。服务报价显示了预计的零件费用、预计的工费、销售税和总预估费用。

# 类与多形式项目

注意某些名词是重复的。以下列表显示了所有名词，且没有重复任何项。

- address（地址）

- BMW（宝马）

- car（汽车）

- cars（汽车）

- customer（客户）

- estimated labor charges（预计工费）

- estimated parts charges（预计零件费用）

- foreign cars（外车）

- Joe's Automotive Shop（Joe 的汽车修理店）

- make（品牌）

- manager（经理）

- Mercedes（奔驰）

- model（型号）

- name（姓名）

- Porsche（保时捷）

- sales tax（销售税）

- service quote（服务报价）

- shop（修理店）

- telephone number（电话号码）

- total estimated charges（总预估费用）

- year（年份）

# 精炼名词列表

出现在问题描述中的名词仅仅是候选者。下一步是精炼列表，只包含与问题相关的类。让我们详细查看这些步骤中的每一步。

- address

- BMW

- car

- cars

- customer

- estimated labor charges

- estimated parts charges

- foreign cars

- Joe's Automotive Shop

- make

- manager

- Mercedes

- model

- name

- Porsche

- sales tax

- service quote

- shop

- telephone number

- total estimated charges

- year

（注：OCR 文本在此似乎存在重复/对齐错误，我将根据提供的逻辑流进行重构。）

# 类与多形式项目

或可以存储在变量中的数值值。以下是更新后的潜在类列表：

```
address
BMW
car
ens
customer
estimated labor charges
estimated parts charges
foreign cars
Joe's Automotive Shop
make
manager
Mercedes
model
name
Porsche
sales tax
service quote
shop
phone number
total estimated charges
year
```

我们已经删除了地址、预估工时费、预估零件费、品牌（make）、型号（model）、名称、销售税、电话、总预估费用和年份作为类，因为它们代表了可以存储在变量中的简单值。
