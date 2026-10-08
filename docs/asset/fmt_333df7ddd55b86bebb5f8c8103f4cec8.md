
| `menuEditEntree_Click` | `ToolStripMenuItem` | `menuEditEntree` |
| `menuEditSpecial_Click` | `ToolStripMenuItem` | `menuEditSpecial` |
| `menuExit_Click` | `ToolStripMenuItem` | `menuExit` |
| `menuPlaceOrder_Click` | `ToolStripMenuItem` | `menuPlaceOrder` |

### 编码标准

如在前一节中所讨论，对于添加到 Windows 表单的控件遵循一致的命名标准非常重要。在注册事件（如按钮点击事件）之前，请为它们命名。

## 资源

你可能想要探索的额外网站：

- 事件与 Visual Studio “坑”：http://www.uga.edu/~VisualStudioGotchas
- .NET 中的委托和事件：http://www.microsoft.com/en-us/dotnet/framework/delegates-and-events
- C# 程序员参考：http://www.akademia.com/
- ListBox 和 CheckedListBox：http://www.geeksforgeeks.org/tutorial/
- 使用 C# 创建动态菜单：http://www.codeguru.com/csharp

# 快速复

1. 委托是存储方法的特殊类型。
2. 委托的声明看起来更像方法。每个委托都有签名。
3. 多路委托连接到多个方法，当事件触发时，这些方法依次执行。
4. 在程序中响应事件需要两件事。首先，你必须注册感兴趣的事件，然后生成事件处理方法。这个过程被称为事件处理。
5. 所有事件处理方法都有相同的签名。它们不返回任何内容；类型为 `void`。它们有两个参数。
6. `ListBox` 用于显示用户从中选择的项目列表。可以进行单选或多选。如果项目总数超过显示数量，控件会自动添加滚动条。
7. 在设计时或运行时，你可以动态向列表中添加或删除项。
8. `ListBox` 对象的默认事件是 `SelectedChanged( )` 事件。当 `ListBox` 对象的选择发生变化时，触发该事件。
9. `ListBox` 类有很多有趣的属性，包括 `Items`，它可以获取列表。`SelectedIndex` 和 `SelectedItem` 属性获取或设置选中项。
10. `ListBox` 和 `ComboBox` 对象是零索引结构。`SelectedIndex` 和 `SelectedIndices` 属性通过索引位置访问对象。
11. `Text` 属性是最常用的属性。它接收当前选中项的文本。
12. `ListBox` 控件和 `ComboBox` 对象共享许多相同的属性和方法。`ComboBox` 对象包含了自己的文本字段，这使得在运行时添加新值变得容易。
13. 当用户按下键时，会发生 `KeyPress( )` 事件。实际上，每次按键都会触发事件。此事件处理方法有时与 `ComboBox` 对象配合使用。

# 第 10 章 基于事件的编程

16. 使用 Visual Studio 窗口和 `MenuStrip` 类，可以轻松地将 `MenuStrip` 控件对象绘制并拖到表单（Form）上。
17. 你可以为菜单选项创建快捷键。使用 Alt 键创建快捷键既快速又方便。当你输入要在菜单中显示的文本时（使用 `Text` 属性），在字符前加上安培符 (&) 即可允许按下 Alt 键加上显示为快捷键的键。
18. 如果你正在使用 `MainMenu` 对象，为了让菜单显示在表单上，你需要将 Form 的 `Menu` 属性设置为 `MainMenu` 对象的名称。
19. 有许多预配置的对话框可以添加到菜单中。它们包括类似于标准 Windows 文件打开、文件保存、文件打印、打印预览、字体格式和颜色格式的对话框。你可以通过将控件对象拖放到表单上将其添加到你的应用程序中。
20. 复选框（Check boxes）以小方框的形式出现，允许用户进行“是/否”或“真/否”的选择。`CheckBox` 对象的默认事件处理方法是 `Changed()`。`Click()` 事件也可以连接到 `CheckBox` 对象上。双击其中一个 `CheckBox` 对象将为该对象注册一个 `Changed()` 事件。
21. 从视觉外观考虑，可以使用 `GroupBox` 控件将 `CheckBox` 对象分组。这种分组设计允许你将所有对象作为一个整体移动。然而，分组并没有为 `Check` 对象提供任何额外的功能。
22. 对于单选按钮（radio buttons），应该在表单上放置一个 `GroupBox`。单选按钮允许用户在两个或更多多个选项之间进行选择。请记住，选择多个 `CheckBox` 对象是合适的，但 `RadioButton` 对象则不然。
23. 多个单选按钮可以连接到同一个事件处理方法。
24. Windows Presentation Foundation (WPF) 应用程序创建一个特殊的 XAML 文件，使用标签来控制应用程序的外观。`No_designer.cs` 是
25. `TabControl` 对象在表单上显示多个标签页，类似于文件柜中一组文件夹的标签。每个标签页存储不同的控件，并有一个 `Click` 事件。

## 练习题

- 1. 委托（Delegates）存储：
  - a. 数据签名的地址
  - b. 关于程序中事件的数据和方法
  - c. 事件
  - d. 方法的地址
  - e. 以上所有

# 练习题 635

2. 给定委托声明：

`delegate void PerformsSomeTask(int arg1, double arg2);`

下列哪项语句似乎可以创建一个 `PerformsSomeTask()` 的委托实例且没有语法错误？

- a. `PerformsSomeTask task1 = new PerformsSomeTask(CalculateThis);`
- b. `PerformsSomeTask task1 = new PerformsSomeTask(CalculateThis());`
- c. `PerformsSomeTask( ) task1 = new PerformsSomeTask(CalculateThis());`
- d. `PerformsSomeTask( ) task1 = new PerformsSomeTask(CalculateThis(int, double));`
- e. `PerformsSomeTask task1 = new PerformsSomeTask(CalculateThis(int arg1, double arg2));`

3. 给定委托声明：

`delegate void PerformsSomeTask(int arg1, double arg2);`

下列哪项代表了可以与该委托关联的方法头定义？

- a. `int CalculateThis(int value1, double value2)`
- b. `double CalculateThis(int value1, double value2)`
- c. `void CalculateThis(int value1, double value2)`
- d. `int CalculateThis( )`
- e. 以上所有

4. 方法的签名仅包括：

返回类型、方法名、参数个数以及参数的数据类型

- a. 方法名和返回类型
- b. 参数的个数和参数的数据类型
- c. 方法名、参数个数和参数的数据类型
- e. 返回类型、参数个数和参数的数据类型

5. 多路委托（A multicast delegate）是指具有以下特征之一的：

- a. 了多个方法
- b. 具有多个参数
- c. 在程序中创建了多个自身的实例
- d. 具有多个返回类型
- e. 以上都不是

# 第 10 章 基于事件的编程

- 6. 下述语句最准确地总结了委托与事件的关系：
  a. 委托是事件的实例。
  b. 委托用于调用事件处理方法。
  c. 委托必须与事件注册。
  d. 事件在程序中维护一个委托列表。
  e. 以上所有

- 7. `ListBox` 控件对象和 `ComboBox` 控件对象的一个区别特征是：
  a. `ListBox` 对象可以多项选择。
  b. `ComboBox` 对象仅用于输出。
  c. `ComboBox` 对象可以看到滚动条。
  d. 编写 `ComboBox` 对象的事件处理方法更简单。
  e. 以上都不是

- 8. `ListBox` 对象的默认事件处理方法是：
  a. `KeyPress()`
  b. `Click()`
  c. `SelectedItem()`
  d. `SelectedIndexChanged()`
  e. `Selected()`

- 9. 返回 `ListBox` 对象所选索引集合的属性是：
  a. `SelectedIndex`
  b. `SelectedIndices`
  c. `Text`
  d. `Items`

- 10. `ComboBox` 对象相比 `ListBox` 对象提供的额外功能是：
  a. 允许在运行时删除值
  b. 允许多项选择
  c. 在程序中创建了多个自身的实例
  d. 具有多个返回类型
  e. 以上都不是

- 10. `ComboBox` 对象相比 `ListBox` 对象提供的额外功能是：
  a. 允许在运行时删除值
  b. 允许多项选择
  c. 在程序中创建了多个自身的实例
  d. 具有多个返回类型
  e. 以上都不是

11. 假设 `comboBoxData` 已经实例化，以下哪项在字符串变量中检索选择内容？

- a. `SelectionMode.Text;`
- b. `SelectedData.Text;`
- c. `SelectedText;`
- d. `SelectedItem.Text;`

12. 在输入菜单文本后，还需要做什么才能在表单上看到它？

- a. 将菜单属性设置为表单。
- b. 设置表单的名称。
- c. 创建菜单。
- d. 编写 `menu`。
- e. 以上所有

13. 当输入菜单文本时，使用的是哪一个？

a. `Help(P)`
b. `Help`
c. `Help&`
d. `Help&`
e. `Help(p)`

14. 如果你想显示选择框，使用的是哪一个？

a. check box
b. combo box
c. menu
d. radio button

15. 使用哪个属性来确定 `CheckBox` 和 `RadioButton` 是否被选中？

a. `Selected`
b. `SelectedIndex`
c. `SelectedItem`
d. `Checked`

# 第 10 章 基于事件的编程

16. 将事件连接到多个：

a. 相同的方法
b. 相同的属性
c. 创建多个方法
d. 使用安培符命名对象
e. 以上都不是

17. `GroupBox` 为哪些对象提供了更多功能？

a. `ComboBox`
b. `ListBox`
c. `CheckBox`
d. `RadioButton`

18. `Click` 事件是哪个类型的默认事件？

a. `Button`
b. `RadioButton`
c. `MenuItem`
d. `CheckBox`
e. 以上所有

19. 如果没有 Visual Studio 窗口，使用哪条语句可以设置 `ListBox` 模式？

a. `ListBox1.SelectionMode = SelectionMode;`
b. `ListBox1 = SelectionMode;`
c. `SelectionMode = SelectionMode;`
d. `SelectionMode = ListBox1;`
e. 以上所有

20. 哪个属性可以使 `Enter` 键像点击一样？

a. `Enter`
b. `Button_Click`
c. `Enter`
d. `AcceptButton`

# 练习题 639

21. 描述使菜单选项可点击或使选择框功能化所需的条件。
22. 什么情况下使用 `RadioButton` 比于 `CheckBox`？什么情况下使用 `ComboBox` 比于 `ListBox`？
23. 委托与事件是什么关系？
24. 对于下表，识别哪些属性可以设置给定值。

| 预期操作 | 属性 |
|---|---|
| 从 ComboBox 获取选中项 | |
| 分组框标签 | |
| 升序排列列表框中的项目 | |
| 更改文本颜色 | |
| 设置主菜单到表单 | |

25. 从以下部分代码列表中，识别需要编写的事件处理方法的名称。它们连接到哪些对象上？

# 第10章 基于事件编程

```csharp
this.btnNew.Text = "Add New One";
this.btnNew.Click += new System.EventHandler(this.btnNew_Click);
this.AutoScaleBase = new System.Drawing.Size(8, 19);
this.BackColor = System.Drawing.FromArgb(
    ((System.Byte)(128)), ((System.Byte)(128)),
    ((System.Byte)(255)));
this.ClientSize = new System.Drawing.Size(292, 273);
this.Controls.Add(
    new System.Windows.Forms[] {
        this.btnNew,
        this.txtBoxNewAct,
        this.label3,
        this.label1,
        this.txtBoxResult,
        this.label2,
        this.lstBoxEvents
    }); // 表示缺少项目。
```

## 编程练习

- 1. 创建一个图形用户界面，允许用户输入姓名、电子邮件地址和电话号码。添加一个具有三个功能的菜单选项。第一个在消息框中显示用户输入的信息；第二个清除输入内容以便输入新值；第三个菜单选项关闭应用程序。
- 2. 创建一个消息显示器，包含一个 `ComboBox` 对象，其中列出四种你最喜欢的运动。在你的设计中，包含允许用户输入自己的格言的能力。当做出选择或输入新条目时，在表单的 `Label` 上显示该选择。
- 3. 在练习2的应用程序中添加一个菜单，至少包含“格式 (Format)”和“帮助 (Help)”菜单选项。在“格式”选择下，包含“字体 (Font)”和“颜色 (Color)”选项。使用字体和颜色选项调用 Windows 预定义的字体和颜色对话框，当值发生变化时，显示格言的 `Label` 对象中的文本也会随之改变。
- 4. 创建一个图形用户界面，包含五种不同运动名称的单选按钮。其中只能有一个被选中。编写你的事件处理方法，以便每次选择不同的运动时显示一条消息。例如，如果其中一种运动是滑雪，消息可能是“穿上暖衣服！”增强功能是在表单上包含一个 `PictureBox` 对象来显示运动项目的图片。当选择特定运动时，使 `PictureBox` 可见。你可以在互联网上找到免费图形供你的应用程序使用。
- 5. 创建一个 Windows 应用程序，用作 Flyers 运动俱乐部滑雪设备的报名表。该俱乐部以极廉的价格向成员提供滑雪设备。为了确定成员在即将到来的旅行中可能需要的类型，他们要求你设计并实现一个需求表。包含 Check 对象以允许用户选择旅行所需的装备类型。根据你的判断，包含滑雪板、护雪镜、耳罩和其他项目的选择。在完成所有选择后，显示一条消息指示已选择了哪些项目。你可能希望包含菜单选项来显示和清除供下一个用户的订单。还要包含一个允许用户退出应用程序的选项。
- 6. 创建一个用于购买地毯的 Windows 应用程序。允许输入房间的长度和宽度。设置一个显示不同地毯价格的控件。例如，每平方码码 $21.95。在用户输入房间尺寸和地毯价格后，显示铺设房间的总成本。包含一个清除选择的选项。
- 7. 创建一个允许购买包的订单表。共有六种不同类型：全装饰型、珠绣型、针线设计型、流苏珠型和纯色型。为不同的样式创建一个 List 对象。在用户做出选择后，显示一条消息指示选择了哪种类型。包含一个清除选择的选项。
- 8. 在练习7的应用程序中添加一个允许用户输入所需数量的控件。包含一组单选按钮，包含隔夜、三日和标准运输选项。每只包的价格如下：全装饰型—$50.00；珠绣型—$45.00；针线设计型—$40.00；流苏型—$25.00；流苏型—$30.00；以及纯色型—$20.00。运费根据购买总量计算。使用以下百分比：隔夜—10%；三日—7%；标准—5%。在消息框中显示带有带有选择、数量和总成本的运费。
- 9. 电脑俱乐部销售 T 恤。创建一个吸引的用户界面，允许用户选择尺寸（S, M, L 和 XL）和数量。哪些控件最合适？记住，用户需要的按键次数越少越好。通过“处理 (Process)”菜单选项显示用户所做的选择。包含一个退出应用程序的选项。
- 10. 在练习9的解决方案中增加两个尺寸，XSmall 和 XXLarge。添加通过计算总成本来处理订单的语句。每件衬恤 $16，但 XSmall 和 XXLarge 除外；它们的特殊价格每个为 $20.00。显示选择的总成本。包含一个显示说明的“帮助 (Help)”菜单选项。你可以通过允许用户在同一份订单中购买不同尺寸来增强你的解决方案。

# 11 高级面向对象编程特性

在本章中，你将：

- 学习面向对象语言的主要特性
- 使用基于组件开发的方法设计和开发多层应用程序
- 使用继承来扩展类的功能
- 创建抽象类
- 区分密封 (sealed) 和抽象 (abstract)
- 设计并实现接口
- 理解为什么多态是 .NET 的一个共同目标
- 探索泛型并学习如何创建类
- 调查静态类型与动态类型
- 通过编程示例说明概念

在本章中，你将通过探索面向对象设计的高级特性来扩展编程知识。你将接触基于组件开发，并学习如何创建自己的类库。你将调查构成框架的 2000 多个类。
