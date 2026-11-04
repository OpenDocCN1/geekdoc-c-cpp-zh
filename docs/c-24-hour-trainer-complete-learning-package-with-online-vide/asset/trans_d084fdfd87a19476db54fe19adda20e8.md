
由于这两个引用变量指向同一个对象，如果你使用其中一个变量修改对象，另一个变量也会看到这个修改。例如，如果你执行语句 ben.FirstName = "Ben"，那么 ann.FirstName 的值也将包含 Ben。

相反，如果你将一个值类型变量设置为等于另一个变量，第一个变量会收到第二个变量值的副本。例如，假设 cindy 和 dan 是结构类型 Person 的两个变量。Person 类型可能与 Student 类型非常相似，只不过它是结构（值类型）而不是类（引用类型）。在这种情况下，语句 dan = cindy 会使变量 dan 持有结构体 cindy 中值的副本。

图 17-2 以图形方式展示了这一操作。最初（左图），变量 cindy 和 dan 各自包含 Person 数据。这次，变量包含矩形内的所有数据；它们不仅仅是指向存储在其他地方的值的引用。在执行语句 dan = cindy 之后，两个变量包含相同数据的独立副本。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_292_0.png)

图 17-2

由于这两个值变量对应的是同一数据的不同副本，改变其中一个不会改变另一个。例如，如果你执行语句 dan.Name = "Dan"，那么 cindy.Name 的值仍将是 Cindy。

本课下载内容中提供的“结构体与类”示例程序演示了这一差异。这个问题相当重要，因此值得你花时间下载该示例并研究，直到你确信自己理解为止。

那么，应该使用结构体还是类呢？在许多程序中，这种差异并不重要。只要你意识到相关的差异，通常可以任选其一。

Microsoft 的“类与结构（C# 编程指南）”网页（msdn.microsoft.com/library/ms73109.aspx）给出了如下建议：

> 一般来说，类用于对更复杂的行为建模，或者对预期在创建类对象后会被修改的数据建模。结构体最适合那些主要包含数据、且这些数据在结构体创建后不打算被修改的小型数据结构。

如果你遵循这一建议，那么像 Person 或 Student 这类较为复杂的数据，或许应该实现为类。你可能需要随时间更新 Person 或 Student 信息，这也说明它们可能应该作为类。相比之下，假设你在编写一个烤箱控制程序，需要一种数据类型来存储温度数据。在这种情况下，你可能会将数据存储在 Temperature 结构体中。

在某种程度上，某个*温度值*发生改变是没有意义的，尽管*烤箱温度*发生改变可能是有意义的。例如，烤箱温度可能从 75° 开始，然后升温到 375°。75° 这个温度并没有改变；改变的是烤箱的温度。程序不会去更新温度变量，而是将该变量设置为新的温度值。

要理解这种差异，回想一下 Student 示例。如果 Ann 搬家了，你需要更改她的地址（假设 Student 类包含姓名、地址、电话号码和其他相关数据）。Ann 本身并没有改变，所以将 ann 变量设置为一个全新的 Student 对象实际上是没有意义的。相反，你只需更新 ann.Address 的值即可。

如果你认为我在这里只是在吹毛求疵、钻牛角尖，你说得没错。差异确实存在，但就实际用途而言，使用类还是结构体通常不会有太大区别。很多 C# 程序员基本上一直使用类而不是结构体。（我怀疑部分原因是他们不必记住值类型和引用类型之间的差异。）如果你使用的是 Microsoft 或其他程序员定义的类和结构体，那么这些差异就很重要；但在编写自己的代码时，你可以选择你认为最有意义的任何一种。

## 在何处定义结构体

你可以在几处定义结构体。

首先，你可以在类内部、但在其任何方法之外定义结构体。例如，你可以在窗体类内定义结构体。这样，该结构体只在包含它的类内部可见。如果类外部的代码不需要使用该结构体，这种限制就可以限定其可见性，从而避免外部代码可能产生的混淆。

其次，你可以在定义类的文件中、但在类代码之外定义结构体。例如，你可以将它放在类文件的底部，紧挨在结束文件顶部开始的 namespace 语句的最后一个右大括号之前。在这种情况下，该结构体对项目中的所有代码都可见（假设你给予它足够的可见性，例如 public）。

第二种方法可能有点让人困惑，因为同一个文件既定义了类又定义了结构体。第三种位置是在结构体自己的模块中定义它，供整个程序使用。最简单的方法是使用“项目”菜单中的“添加类”命令。将类命名为你想要给结构体起的名称，然后点击“添加”。Visual Studio 创建类之后，将 class 关键字改为 struct。

你可以在相同的位置定义枚举。

## 试一试

在本“试一试”练习中，你将使用一个枚举和一个结构体来创建如图 17-3 所示的通讯录。当用户点击“添加”按钮时，程序会保存输入的地址值。如果用户输入姓名并点击“查找”，程序会检索相应的地址数据。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_294_0.png)

图 17-3

## 本课要求

在本课中，你将：

- 创建如图 17-3 所示的窗体。
- 定义 ContactMethod 枚举，其值为 None、Email、Phone 和 SnailMail。
- 定义一个 Address 结构体，用于保存输入的地址信息。
- 创建一个 `Dictionary<string, Address>` 字段，用于保存地址数据。
- 添加代码，使窗体加载时初始选择 ComboBox 的 None 项（只是为了有选中项）。
- 为“添加”按钮添加代码，在 Dictionary 中创建新条目。
- 为“查找”按钮添加代码，从 Dictionary 中检索相应条目并显示它。

> 注意：你可以从网站 www.wrox.com/go/csharp24hourtrainer2e 下载本课的代码和资源。

## 分步说明

- 创建如图 17-3 所示的窗体。
  1. 我相信现在你可以自己完成这一步了。

```
newAddress.Street = streetTextBox.Text;
newAddress.City = cityTextBox.Text;
newAddress.State = stateTextBox.Text;
newAddress.Zip = zipTextBox.Text;
newAddress.Email = emailTextBox.Text;
newAddress.Phone = phoneTextBox.Text;
newAddress.PreferredMethod = (ContactMethod)preferredMethodComboBox.SelectedIndex;

// Add the name and address to the dictionary.
Addresses[nameTextBox.Text] = newAddress;

// Get ready for the next one.
nameTextBox.Clear();
streetTextBox.Clear();
cityTextBox.Clear();
stateTextBox.Clear();
zipTextBox.Clear();
emailTextBox.Clear();
phoneTextBox.Clear();
preferredMethodComboBox.SelectedIndex = 0;

nameTextBox.Focus();
}
```

为“查找”按钮添加代码，从 Dictionary 中检索相应条目并显示它。

1. 使用类似下面的代码：

```
// Look up an address.
private void findButton_Click(object sender, EventArgs e)
{
    // Get the Address.
    Address selectedAddress = Addresses[nameTextBox.Text];

    // Display the Address's values.
    nameTextBox.Text = selectedAddress.Name;
    streetTextBox.Text = selectedAddress.Street;
    cityTextBox.Text = selectedAddress.City;
    stateTextBox.Text = selectedAddress.State;
    zipTextBox.Text = selectedAddress.Zip;
    emailTextBox.Text = selectedAddress.Email;
    phoneTextBox.Text = selectedAddress.Phone;
    preferredMethodComboBox.SelectedIndex = (int)selectedAddress.PreferredMethod;
}
```

## 练习

- 1. 复制你为本课“试一试”部分构建的程序。添加一个“删除”按钮，通过调用 Dictionary 的 Remove 方法来删除条目。
- 2. 除了简单字段之外，结构体还可以包含数组。复制你在练习 1 中创建的程序，并修改 Address 结构体，让它包含一个数组，用于保存三个电话号码。
