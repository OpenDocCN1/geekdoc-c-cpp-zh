

## 第21章

### 处理 Play 菜单事件

`playMenuItem_Click()` 处理程序应为当前可见的选项卡上的按钮创建一个新的值集合。回想一下本章前面，你将 TabControl 控件中选项卡的 (Name) 属性值设置为 lottoTab 和 euroTab。如果你查看现在内容丰富的 Form1 类定义，你会找到两个类型为 TabPage^ 的变量，其名称与此相同。类型为 TabPage 的对象具有类型为 bool 的 Visible 属性，如果页面可见则值为 true，如果不可见则为 false。这正是实现 Play 菜单项处理程序所需的。

处理程序的大致逻辑可以使用选项卡页面的 Visible 属性值，如下所示：

```cpp
private: System::Void playMenuItem_Click(System::Object^ sender,
    System::EventArgs^ e)
{
    if(lottoTab->Visible)
    {
        // Generate and set values for Lotto entry
    }
    else if(euroTab->Visible)
    {
        // Generate and set values for Euromillions entry
    }
}
```

如果 lottoTab 页面的 Visible 属性为 true，你就创建一个新的 Lotto 彩票条目，如果 euroTab 页面的 Visible 属性为 true，你就创建一个 Euromillions 彩票条目。虽然两个选项卡不能同时可见，但最好对两个选项卡页面都进行正向测试，因为用户可能会在 Web Page 选项卡可见时单击 Play 菜单项。

为两种彩票生成一组值的过程有一些共同点。对于 lotto，你必须在给定范围内生成六个不同的随机整数。对于 Euromillions，你必须在给定范围内生成五个不同的整数，然后在另一个范围内生成两个不同的整数。一个用于在给定范围内生成任意数量整数的辅助函数会很有用。你可以像这样定义这样的函数：

```cpp
void GetValues(array<int>^ values, int min, int max)
{
    // Fill the array with different random integers from min to max...
}
```

values 数组的 Length 属性告诉你需要生成多少个值。调用函数只需创建一个适当大小的数组并将其作为第一个参数传递给 GetValues() 函数。第二和第三个参数指定要生成的值的限制。

将 GetValues() 函数作为 Form1 类的私有成员添加并完成定义如下：

```cpp
void GetValues(array<int>^ values, int min, int max)
{
    values[0] = random->Next(min, max);    // Generate first random value
    // Generate remaining random values
    for(int i = 1 ; i < values->Length ; i++)
```

```cpp
{
    // Generate and set values for Euromillions entry
    values = gcnew array<int>(euroValuesCount);
    GetValues(values, euroUserMinimum, euroUserMaximum);
    SetValues(values, euroValues);
    values = gcnew array<int>(euroStarsCount);
    GetValues(values, euroStarsUserMinimum, euroStarsUserMaximum);
    SetValues(values, euroStars);
}
```

Lotto 条目创建分为三个步骤：

- 创建保存值的数组。
- 通过调用 GetValues() 函数生成值。
- 通过调用 SetValues() 函数将值作为文本设置在按钮上。

对于 Euromillions 彩票条目，步骤序列重复两次：一次用于五个值的集合，再一次用于两个星号的集合。

在实现 SetValues() 函数时，你可以利用按钮包含在 GroupBox 控件中的事实。GroupBox 对象的 Controls 属性返回已添加到该对象的所有控件的集合。由 GroupBox 的 Controls 属性返回的集合本身具有默认的索引属性，可访问集合中的控件。该集合像栈一样是后进先出，因此属性访问的索引值以与你将它们添加到组框的顺序相反的顺序访问控件。你可以像这样将 SetValues() 函数实现为 Form1 类的私有成员：

```cpp
// Set values as text on buttons in a GroupBox control
void SetValues(array<int>^ values, GroupBox^ groupBox)
{
    Array::Sort(values); // Sort values in ascending sequence
    int count = values->Length - 1;
    for(int i = 0 ; i < groupBox->Controls->Count ; i++)
        safe_cast<Button^>(groupBox->Controls[i])->Text = values[count-i].ToString();
}
```

在对值数组排序后，你将 count 变量设置为数组中最后一个元素的索引值。然后循环以相反的顺序将值的字符串表示形式存储在每个 Button 控件的 Text 属性中。表达式 groupBox->Controls[i] 生成类型为 Control^ 的句柄，引用集合中索引 i 对应的控件，然后你将其强制转换为类型 Button^，在访问 Text 属性以设置其值之前。

你不必使用 GroupBox 对象来实现 SetValues() 函数提供的功能。所有按钮都是 Form1 类的显式成员，因此你也可以采用笨拙的方法，直接访问它们来设置 Text 属性的值。你至少需要两个单独的函数——一个用于 Lotto 条目，一个用于 Euromillions 条目，尽管后者可能更方便地拆分为两个函数，总共三个。以下是设置 Lotto 条目值的函数可能的样子：

```cpp
void SetNewValues(array<int>^ values)
{
    Array::Sort(values);
    lottoValue1->Text = values[0].ToString();
    lottoValue2->Text = values[1].ToString();
    lottoValue3->Text = values[2].ToString();
    lottoValue4->Text = values[3].ToString();
    lottoValue5->Text = values[4].ToString();
    lottoValue6->Text = values[5].ToString();
}
```

此函数使用每个按钮的句柄来设置其 Text 属性。用于设置 Euromillions 条目 Text 属性的函数可以以本质相同的方式实现。然后你需要修改 playMenuItem_Click() 处理程序函数以调用这些函数来设置值。

现在你可以重新编译 Ex21_01 来查看是否一切正常。如果你在输入代码时没有拼写错误，你应该能够生成如图 21-18 所示的 Lotto 条目。

![](img/2359b0c604600c58fba3539c738a356e_1096_0.png)

图 21-18

按钮上的数字按升序排列，因此看起来整洁有序。如果它们没有按顺序出现，可能是因为你没有按有序的方式将按钮添加到 GroupBox 控件中。

该程序还生成了如图 21-19 所示的 Euromillions 彩票条目。

![](img/2359b0c604600c58fba3539c738a356e_1097_0.png)

**图 21-19**

现在基本功能已经具备，是时候进一步开发应用程序了。

### 处理 Limits 菜单的事件

`Limits` 菜单上有三个菜单项，你需要为每个菜单项的 `Click` 事件提供一个处理程序。依次双击每个菜单项以生成处理程序函数并将它们各自注册为处理 `Click` 事件。

Reset 菜单项的 `Click` 事件处理程序将是最容易实现的，因为它所要做的只是将用户限制设置回与当前可见的彩票所施加的限制相同。其他两个菜单项的 `Click` 事件处理程序将涉及更多的工作。你必须为限制值提供某种输入方式，而最明显的方法是在单击菜单项时显示一个对话框。显然，开发应用程序的下一步需要了解如何创建对话框。

### 创建对话框

`Toolbox` 窗口提供了一些标准对话框；它们都相当花哨，但在这个例子中都不合适。因为你需要在这个程序中实现非常具体的内容，所以你必须自己创建对话框。对话框只是一个 `FormBorderStyle` 属性值设置为 `FixedDialog` 的窗体，因此在创建对话框时你会得到 Form Designer 的大量帮助。

在主菜单上选择 `Project > Add New Item`，或按 `Ctrl+Shift+A` 显示如图 21-20 所示的对话框。

从右窗格的 `Categories:` 列表中选择 UI，并将模板选择为 `Windows Form`，并按如图 21-20 所示输入名称。这是你在设置 Lotto 条目的上限或下限时显示的对话框窗口。你稍后会为 Euromillions 彩票条目创建另一个对话框窗体。当你单击 Add 按钮时，一个新窗体将被添加到项目中并在编辑器窗口中显示。新对话框的类类型是你提供的名称，`LottoLimitsDialog`。

