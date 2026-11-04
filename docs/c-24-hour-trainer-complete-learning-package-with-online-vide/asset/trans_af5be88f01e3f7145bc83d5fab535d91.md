
类继承了 Shape 类的 Draw 方法，因此椭圆将在 PictureBox 上绘制为矩形。别担心。我们将在下一课的练习中修复这个问题。）

7. [Graphics, Hard] 复制你在练习 6 中编写的程序并添加一个 Circle 类，该类继承自 Ellipse。为新类提供以下签名的构造函数：

```
public Circle(Pen pen, Brush brush, Point center, int radius)
```

使此构造函数通过调用父类构造函数来初始化对象。

8. [Graphics] 复制你在练习 7 中编写的程序并修改它，使 Shape 类存储两个名为 Foreground 和 Background 的 Color 属性，而不是 Pen 和 Brush。还添加一个新的整数 Thickness 属性以及类构造函数中对应的参数。（你需要对继承自 Shape 的类进行类似的更改。）

修改 Draw 方法，使其使用适当的颜色和线条粗细填充并绘制 Shape。要填充 Shape，请创建一个新的 SolidBrush 对象。要描边 Shape，请创建一个新的 Pen 对象。包含 using 语句以自动释放画刷和画笔。

最后，更新主程序以使用新的构造函数并创建具有不同颜色和线条粗细的示例形状。

9. [Graphics] 复制你在练习 8 中编写的程序并修改 Draw 方法，使其使用虚线。为此，将 Pen 对象的 DashStyle 属性设置为 System.Drawing.Drawing2D.DashStyle.Dash。（这是制作虚线画笔的唯一方法。诸如 Pens.Blue 和 Pens.Chartreuse 之类的标准 Pen 对象是实心的且宽度为一个像素。）

> 注 请在 www.wrox.com/go/csharp24hourtrainer2evideos 在线选择第 24 课的视频。

## 25 精细调整类

在第 24 课中，你学习了如何构建构造函数和析构函数，这些特殊方法在对象创建或销毁时执行。在本课中，你将学习可以赋予类的其他特殊方法。你将学习如何重载和重写类方法。

### 方法重载

第 24 课提到，只要它们具有不同的参数列表，你就可以为一个类提供任意数量的构造函数。例如，通常会为一个类提供一个不带参数的无参数构造函数和一个或多个带参数的其他构造函数。

使用相同名称但参数列表不同的多个方法称为重载。C# 使用参数列表来决定在调用方法时使用哪个版本。

例如，假设你正在构建一个课程作业应用程序，并且你已经构建了 Student、Course 和 Instructor 类。你可以为 Student 类提供两个版本的 Enroll 方法，一个以学生所修课程的名称作为参数，另一个以 Course 对象作为参数。

你可以为 Instructor 类提供类似版本的 Teach 方法，使讲师可以通过名称或 Course 对象来教授课程。

最后，你可以为 Course 类提供不同的 Report 方法，这些方法：
- 如果没有参数，则在对话框中显示报告。
- 如果方法接收到 FileStream 作为参数，则将报告追加到文件末尾。
- 如果方法接收到字符串（文件名）作为参数，则将报告保存到新文件中。

制作重载方法非常容易，几乎没有其他需要说明的地方。唯一的限制（而且是很小的限制）是你需要确保参数列表在数量、类型或排列上必须不同。例如，考虑以下两个方法声明：

```csharp
public void MakeReport(string fileToCreate)
{
    ...
}

public void MakeReport(string fileToAppend)
{
    ...
}
```

你可能打算第一个版本在文件中创建报告，第二个版本将报告追加到文件末尾。然而就 C# 而言，它们都接受单个 `string` 作为参数。即使参数名称不同，C# 也无法在不同情况下判断使用哪一个。例如，语句 `MakeReport("MyReport.txt")` 应该使用哪个版本？

### 方法重写

当一个类继承自另一个类时，你可以向新类添加新的属性、方法和事件，以赋予它父类未提供的功能。

偶尔也很有用，可以用新版本替换父类提供的方法。这称为 *重写* 父类的方法。

在重写方法之前，你应该用 `virtual` 关键字标记父类中的方法，以便允许其被重写。接下来，在派生类的方法版本中添加 `override` 关键字，以表示它重写了父类的方法版本。

例如，假设 `Person` 类定义了通常的属性集合：`FirstName`、`LastName`、`Street`、`City` 等等。假设它还提供了以下 `GetAddress` 方法，该方法以适合打印在信封上的格式返回 `Person` 的姓名和地址：

```csharp
// Return the Person's address.
public virtual string GetAddress()
{
    return FirstName + " " + LastName + "\n" +
        Street + "\n" + City + "  " + State + "   " + Zip;
}
```

现在假设你从 `Person` 派生出 `Employee` 类。`Employee` 的地址看起来与 `Person` 的地址一样，只是还包括 `MailStop`。`MailStop` 属性由 `Employee` 类添加，用来指示公司内部投递邮件的位置。

以下代码展示了 `Employee` 类如何重写 `GetAddress` 方法以返回 `Employee` 风格的地址：

```csharp
// Return the Employee's address.
public override string GetAddress()
{
    return base.GetAddress() + "\n" + MailStop;
}
```

注意方法如何调用基类版本的 GetAddress 以重用该方法版本并避免重复代码。

> 注 IntelliSense 可以帮助你构建重写的方法。例如，当你在 Employee 类中输入 public override 后加一个空格时，IntelliSense 会列出你可能想要重写的虚拟方法。如果选择其中一个，IntelliSense 会为新方法填充默认实现。以下文本显示了 IntelliSense 为 GetAddress 方法生成的代码：
> 
> ```
> public override string GetAddress()
> {
>     return base.GetAddress();
> }
> ```

关于重写虚拟方法最神奇的事情是，即使你从基类调用该方法，对象也会使用该方法。例如，假设你有一个指向 Employee 对象的 Person 变量。记住 Employee 是一种 Person，因此 Person 变量可以引用 Employee，如以下代码所示：

```
Employee bob = new Employee();
Person bobAsAPerson = bob;
```

现在如果代码调用 bobAsAPerson.GetAddress()，结果是 Employee 版本的 GetAddress。

> 注 你可以将 virtual 关键字视为在基类中为方法创建一个槽。当你重写方法时，派生类用新版本的方法填充此槽。现在即使你从基类调用方法，它也会使用槽中的内容。

### 重写 ToString

重写类的 ToString 方法特别有用。所有类都从 System.Object（所有其他类的最终祖先）继承 ToString 方法，但 ToString 的默认实现并不总是很有用。对于你定义的类，例如 Person 和 Employee，ToString 的默认版本只是返回类的名称。例如，在名为 ListPeople 的程序中，Employee 类的 ToString 方法将返回 "ListPeople.Employee。"

虽然这正确地报告了对象的类，但如果它返回包含对象属性信息的某些内容会更有用。在此示例中，如果它返回 Employee 对象的名字和姓氏就不错了。

幸运的是 ToString 方法是虚拟的，因此你可以重写它。以下代码显示了如何重写 ToString 方法以返回 Employee 的名字和姓氏：

```
// Return first and last name.
public override string ToString()
{
    return FirstName + " " + LastName;
}
```

这更有意义。现在你的程序可以使用 Employee 对象的 ToString 方法来了解该对象。

重写 ToString 对 Windows Forms 开发也有一个不错的副作用。某些控件和 Visual Studio 的某些部分使用对象的 ToString 方法来决定显示什么。例如，ListBox 和 ComboBox 控件显示项目列表。如果这些项目不是简单的字符串，控件会使用项目的 ToString 方法生成输出。

如果列表中充满了 Employee 对象，并且你重写了 Employee 类的 ToString 方法，ListBox 或 ComboBox 可以显示员工姓名。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_403_0.png)

图 25-1

图 25-1 所示的 ListPeople 示例程序（并且作为本课代码下载的一部分提供）演示了方法重写。

启动时，ListPeople 程序使用以下代码用两个 Student 对象和两个 Employee 对象填充其 ListBox。这两个类都继承自 Person。

```
private void Form1_Load(object sender, EventArgs e)
{
    // Make some people.
    peopleListBox.Items.Add(new Student("Ann", "Archer", "101 Ash Ave",
        "Debugger", "NV", "72837"));
    peopleListBox.Items.Add(new Student("Bob", "Best", "222 Beach Blvd",
        "Debugger", "NV", "72837"));
    peopleListBox.Items.Add(new Employee("Cat", "Carter", "300 Cedar Ct",
        "Debugger", "NV", "72837", "MS-1"));
    peopleListBox.Items.Add(new Employee("Dan", "Dental", "404 Date Dr",
        "Debugger", "NV", "72837", "MS-2"));
}
```

Employee 类重写了其 ToString 方法，因此你可以在图 25-1 中看到员工姓名而不是类名。Student 类未重写其 ToString 方法，因此图 25-1 为 Student 对象显示类名。

如果你在此程序中选择一个人并单击“显示地址”按钮，程序将执行以下代码：

// Display the selected Person's address.
private void showAddressButton_Click(object sender, EventArgs e)
