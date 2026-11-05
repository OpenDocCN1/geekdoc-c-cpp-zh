
- 16. 将事件处理程序连接到多个对象涉及：
  - a. 使用相同的方法来处理一个以上对象触发的事件
  - b. 为每个事件处理程序方法选择同一对象的属性
  - c. 创建多个执行相同任务的方法
  - d. 用与号命名对象的 Event 属性
  - e. 以上都不是

- 17. GroupBox 为哪种类型的对象提供更多功能？
  - a. ComboBox
  - b. ListBox
  - c. CheckBox
  - d. RadioButton
  - e. TextBox

- 18. Click() 事件是哪种对象的默认事件？
  - a. Button
  - b. RadioButton
  - c. MenuItem
  - d. CheckBox
  - e. all of the above

- 19. 如果没有 Visual Studio 的属性窗口可用，在 C# 中可以使用哪条语句将 ListBox 对象的选择模式设置为 MultiExtended？ListBox 对象的名称为 lstBox1。
  - a. lstBox1.SelectionMode = SelectionMode.MultiExtended;
  - b. lstBox1 = MultiExtended;
  - c. SelectionMode = MultiExtended;
  - d. SelectionMode.MultiExtended;
  - e. all of the above

- 20. 可以为窗体设置哪个属性，以便使 Enter 键像鼠标单击所选 Button 对象一样工作？
  - a. Enter
  - b. Button_Click
  - c. EnterKey
  - d. AcceptButton
  - e. AcceptKey

- 21. 描述使菜单选项可点击或复选框功能正常所需的内容。

- 22. 在什么情况下更倾向于使用 RadioButton 控件而不是 CheckBox 控件？在什么情况下更倾向于使用 ComboBox 控件而不是 ListBox 控件？

- 23. **委托**与事件有何关系？

- 24. 对于下表，确定可用于为控件设置给定值的属性。

| 期望的操作 | 属性 |
| --- | --- |
| 从 ComboBox 对象获取选中的项 | |
| 更改组框上的标签 | |
| 按升序排列列表框中的项目 | |
| 更改标签中文本的颜色 | |
| 更改窗体标题栏中显示的文本 | |
| 将主菜单关联到窗体 | |

© 2013 Cengage Learning

- 25. 从以下部分代码列表中，确定需要编写的事件处理程序方法名称。它们连接到哪些对象？

```csharp
public class Question : System.Windows.Forms.Form
{
    private System.Windows.Forms.Label label1;
    private System.Windows.Forms.TextBox txtBActivity;
    private System.Windows.Forms.CheckBox ckbxSwim;
    private System.Windows.Forms.CheckBox ckbxSnorkel;
    private System.Windows.Forms.TextBox txtBResult;
    :   // Colon indicates items missing.

    private void InitializeComponent()
    {
        this.label1 = new System.Windows.Forms.Label();
        this.ckbxSwim = new System.Windows.Forms.CheckBox();
        this.ckbxSnorkel = new
            System.Windows.Forms.CheckBox();
        this.lstBxEvents.SelectedIndexChanged += new
            System.EventHandler
            (this.lstBxEvents_SelectedIndexChanged);

        :    // Colon indicates items missing.

        this.label2.Size = new
            System.Drawing.Size(120, 24);
        this.txtBxResult.Location = new
            System.Drawing.Point(-2, 240);
        this.btnNew.Text = "Add New One";
        this.btnNew.Click +=
            new System.EventHandler(this.btnNew_Click);
        this.AutoScaleBaseSize = new
            System.Drawing.Size(8, 19);
        this.BackColor = System.Drawing.Color.FromArgb
            (((System.Byte) (128)), ((System.Byte) (128)),
            ((System.Byte) (255)));
        this.ClientSize =
            System.Drawing.Size(292, 273);
        this.Controls.AddRange(
            new System.Windows.Forms.Control[]
                                 {this.btnNew,
                                  this.txtBxNewAct,
                                  this.label3,
                                  this.label1,
                                  this.txtBxResult,
                                  this.label2,
                                  this.lstBxEvents } );

        :    // Colon indicates items missing.
    }
}
```

## 编程练习

- 1. 创建一个图形用户界面，允许用户输入个人信息，例如姓名、电子邮件地址和电话号码。包含一个提供至少四个功能的菜单。第一个在消息框中显示用户输入的信息。第二个清除条目，以便可以输入新值。第三个菜单选项显示有关应用程序的信息，例如谁开发了它以及它是什么版本。另一个菜单选项关闭应用程序。发挥创意，确保使用 Visual Studio 中的格式菜单选项制作美观的设计。

- 2. 创建一个 Windows 应用程序，可用作 Flyers 体育俱乐部的滑雪设备报名表。俱乐部拥有滑雪设备，以最低费用提供给会员。为了确定会员在即将到来的旅行中可能需要什么类型的设备，他们要求您设计并实现一个设备需求表单。包含 CheckBox 对象，允许用户选择他们需要为旅行购买的装备类型。包括雪手套、滑雪板、护目镜、耳罩以及您认为合适的其他物品的选择。在您的应用程序中至少包含一张图片。完成所有选择后，显示一条消息，指示选择了哪些项目。您可能希望包含菜单选项以显示和清除订单，以便下一位用户使用。还包括一个允许用户退出应用程序的选项。

- 3. 创建一个图形用户界面，供社区团体使用，使青少年能够报名参加不同的体育赛事。包含带有五个不同运动名称的单选按钮。其中只有一个应可选择。编写事件处理程序方法，以便在每次选择不同运动时显示一条消息。例如，如果其中一项运动是滑雪，消息可能说，“Bring warm clothes！”还在窗体上包含一个 PictureBox `object` 以显示体育赛事的图片。当选择特定运动时，使 PictureBox 可见。您可以在互联网上找到免费图形用于您的应用程序。提示：一种将文件关联到 PictureBox 控件的方法是从 Image 属性导入图像。

- 4. 创建一个消息显示器，其中有一个 ComboBox `object`，其中包含至少四条您最喜欢的格言的列表。在您的设计中，包含让用户输入自己的格言的功能。当做出选择或输入新条目时，在窗体上的 Label `object` 上显示所选内容。向应用程序添加一个菜单，其中至少包括 Format 和 Help 菜单选项。在 Format 选择下，包含 Font 和 Color 选项。将 Font 和 Color 选项连接到 Windows 预定义的 Font 和 Color 对话框，以便当其值更改时，显示格言的 Label `object` 中的文本会更改。

- 5. 创建一个订单表单，允许购买包。有六种不同类型：full decorative、beaded、pirate design、fringed、leather、和 plain。创建 ListBox `object` 用于不同样式。包含数量的 ComboBox。应提供最多 10 的数量。用户做出选择后，显示一条消息，指示做出了哪个选择。包含清除选择的选项。当未做出选择时，提供适当的错误消息。

- 6. 通过包含一个允许用户确定所需运送类型的控件，对练习 5 中的应用程序进行补充。包含一组单选按钮，其中包含隔夜、三天和标准运送选项。按如下方式将每个包的价格添加到列表框选择中：full decorative—$50.00；beaded—$45.00；pirate design—$40.00；fringed—$25.00；leather—$80.00；和 plain—$20.00。按排序显示项目。使用字符串类的 方法，从列表框中检索并使用价格。运费基于总购买额。使用的百分比如下：隔夜—10%；三天—7%；和标准—5%。在消息框中显示运费以及选择、数量和总成本。
