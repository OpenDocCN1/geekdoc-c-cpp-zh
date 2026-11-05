
- 2. 给定 `delegate` 声明

  `delegate void PerformsSomeTask(int arg1, double arg2);`

  以下哪条语句看起来会创建 `PerformsSomeTask()` 的 `delegate` 实例且没有语法错误？

    - a. `PerformsSomeTask task1 = new PerformsSomeTask(CalculateThis);`
    - b. `PerformsSomeTask task1 = new PerformsSomeTask(CalculateThis());`
    - c. `PerformsSomeTask() task1 = new PerformsSomeTask(CalculateThis());`
    - d. `PerformsSomeTask() task1 = new PerformsSomeTask(CalculateThis(int, double));`
    - e. `PerformsSomeTask task1 = new PerformsSomeTask(CalculateThis(int arg1, double arg2));`

- 3. 给定 `delegate` 声明

  `delegate void PerformsSomeTask(int arg1, double arg2);`

  以下哪项表示可与该 `delegate` 关联的方法标头？

    - a. `int CalculateThis(int value1, double value2)`
    - b. `double CalculateThis(int value1, double value2)`
    - c. `void CalculateThis(int value1, double value2)`
    - d. `int CalculateThis()`
    - e. 以上都是

- 4. 方法的签名仅包括：

    - a. `return` 类型、方法名、参数数量和参数的数据类型
    - b. 方法名和 `return` 类型
    - c. 参数数量和参数的数据类型
    - d. 方法名、参数数量和参数的数据类型
    - e. `return` 类型、参数数量和参数的数据类型

- 5. 多播 `delegate` 是指：

    - a. 包装了多个方法
    - b. 有多个参数
    - c. 在程序中创建了自身的多个实例
    - d. 有多个 `return` 类型
    - e. 以上都不是

- 6. 以下哪项陈述最能概括委托与事件的关系：

    - a. 委托是事件的实例。
    - b. 委托用于调用事件处理程序方法。
    - c. 委托必须注册到事件。
    - d. 事件在程序中维护一个委托列表。
    - e. 以上都是

- 7. `ListBox` 控件对象与 `ComboBox` 控件对象之间的一个显著区别是：

    - a. ListBox 对象可进行多项选择。
    - b. ComboBox 对象仅用于输出。
    - c. ComboBox 对象可以看到滚动条。
    - d. 为 ComboBox 对象的事件处理程序方法编程更容易。
    - e. 以上都不是

- 8. `ListBox` 对象的默认事件处理程序方法是：

    - a. `KeyPress()`
    - b. `Click()`
    - c. `SelectedItem()`
    - d. `SelectedIndexChanged()`
    - e. `Selected()`

- 9. 返回 `ListBox` 对象所选索引集合的属性是：

    - a. `SelectedIndex`
    - b. `SelectedIndices`
    - c. `Text`
    - d. `Items`
    - e. `SelectedItems`

- 10. ComboBox 对象比 `ListBox` 对象提供的额外功能是：

    - a. 允许在运行时移除值
    - b. 允许进行多项选择
    - c. 包含用于向下移动项的滚动条
    - d. 包含用于在运行时输入值的文本框
    - e. 以上都不是

- 11. 假设 comboBoxData 实例化为 ComboBox，以下哪条语句会获取其选定内容并放入字符串变量？

    - a. `string s = ComboBox.Selection;`
    - b. `string s = ComboBox.comboBoxData.Text;`
    - c. `string s = comboBoxData.Text;`
    - d. `string s.Text = comboBoxData.Text;`
    - e. 以上都不是

- 12. 使用 MainMenu 控件为菜单键入文本后，在窗体上看到该菜单之前还必须完成什么？

    - a. 将窗体上的 Menu 属性设置为菜单的名称。
    - b. 将菜单上的 Form 属性设置为窗体的名称。
    - c. 创建从属于该菜单的 menuItems。
    - d. 为每个 menuItem 编写事件处理程序方法。
    - e. 以上都是

- 13. 当你为 Help 菜单选项键入文本时，以下哪项会为 Help 创建 Alt+P 快捷方式？

    - a. Help(Alt p)
    - b. `&Help`
    - c. `&Help&`
    - d. `Help&p`
    - e. `Help(Alt &p)`

- 14. 如果你希望所有选项都显示在屏幕上，但只允许选择其中一个选项，通常使用哪种类型的结构？

    - a. 复选框
    - b. 组合框
    - c. 菜单
    - d. 单选按钮
    - e. 文本框

- 15. CheckBox 和 RadioButton 对象使用哪个属性来确定其选项是否被选中？

    - a. `Selected`
    - b. `SelectedIndex`
    - c. `SelectedItem`
    - d. `Checked`
    - e. 以上都不是

- 16. 将事件处理程序连接到多个对象涉及：

    - a. 使用同一个方法来处理多个对象触发的事件
    - b. 为每个事件处理程序方法选择相同的对象属性
    - c. 创建执行相同任务的多个方法
    - d. 用 & 符号命名对象的 Event 属性
    - e. 以上都不是

- 17. GroupBox 为哪种类型的对象提供更多功能？

    - a. ComboBox
    - b. ListBox
    - c. CheckBox
    - d. RadioButton
    - e. TextBox

- 18. `Click()` 事件是哪种类型对象的默认事件？

    - a. Button
    - b. RadioButton
    - c. MenuItem
    - d. CheckBox
    - e. 以上都是

- 19. 如果没有可用的 Visual Studio“属性”窗口，C# 中可以使用哪条语句将 ListBox 对象的选择模式设置为 MultiExtended？该 ListBox 对象的名称为 ListBox1。

    - a. `listBox1.SelectionMode = SelectionMode.MultiExtended;`
    - b. `listBox1 = MultiExtended;`
    - c. `SelectionMode = MultiExtended;`
    - d. `SelectionMode.MultiExtended;`
    - e. 以上都是

- 20. 可以设置窗体的哪个属性，使 Enter 键对选定的 Button 对象起到类似鼠标单击的作用？

    - a. Enter
    - b. Button_Click
    - c. EnterKey
    - d. AcceptButton
    - e. AcceptKey

- 21. 描述需要什么才能使菜单选项可点击或复选框正常工作。

- 22. 什么时候首选 RadioButton 控件而不是 CheckBox 控件？什么时候首选 ComboBox 控件而不是 ListBox 控件？

- 23. 委托与事件有何关系？

- 24. 对于下表，指出哪些属性可用于为控件设置给定值。

| 期望操作 | 属性 |
|---|---|
| 从 ComboBox 对象获取选定项 | |
| 更改分组框上的标签 | |
| 按升序排列列表框中的项 | |
| 更改标签中文本的颜色 | |
| 更改窗体标题栏中显示的文本 | |
| 将主菜单关联到窗体 | |

- 25. 从以下部分代码清单中，指出需要编写的事件处理程序方法的名称。它们连接到哪些对象？

```
public class Question : System.Windows.Forms.Form
{
    private System.Windows.Forms.Label label1;
    private System.Windows.Forms.TextBox textBox1;
    private System.Windows.Forms.CheckBox ckBoxSwim;
    private System.Windows.Forms.CheckBox ckBoxSnorkel;
    private System.Windows.Forms.TextBox txtResult;
    :   // Colon indicates items missing.

    private void InitializeComponent()
    {
        this.label1 = new System.Windows.Forms.Label();
        this.ckBoxSwim = new System.Windows.Forms.CheckBox();
        this.ckBoxSnorkel = new
            System.Windows.Forms.CheckBox();
        this.listBox1.SelectedIndexChanged += new
            System.EventHandler
            (this.listBox1_SelectedIndexChanged);
    :   // Colon indicates items missing.

        this.label2.Size = new
            System.Drawing.Size(120, 24);
        this.txtBoxResult.Location = new
            System.Drawing.Point(-2, 240);
```

