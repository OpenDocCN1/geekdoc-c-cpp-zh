

# 核心术语

图形控制元素，或者更简单地称为“控件”，是用户与 GUI 程序交互的组件。

小部件（Widgets）是 GUI 控件。

链接标签（Link label）是一种带有文本的控件，可以将用户链接到其他资源如网页或文件。

控件（Control）的默认事件是在 IDE 中设计控件时双击该控件时生成的事件，它是你使用该控件时最可能修改的方法，也是用户在运行应用程序中遇到该控件时最期望生成的事件。

复选框（Check box）是用户可以点击或取消选择某个选项的 GUI。

单选按钮（Radio button）是一组中的选项，其中一次只能选择一个——选择任何单选按钮都会自动取消其他按钮。

访问键（Access key）提供了使用键盘进行选择的快捷方式。

图片框（Picture box）是一个可以显示图形的 GUI 元素。

列表框（List box）是一个显示用户可以通过点击选择的项目列表 GUI 元素。

组合框（Combo box）是列表框和编辑控件的组合 GUI 元素，允许用户从列表中选择或输入新文本。

对齐线（Snap lines）出现在设计环境中，帮助你将新控件与已有的其他控件对齐。

分组框（Group box）是一个包含其他 GUI 元素的 GUI 元素；它类似于没有滚动条且可以包含标题的面板。

面板（Panel）是一个包含其他 GUI 元素的 GUI 元素；它类似于没有标题但可以包含滚动条的分组框。

菜单条（Menu strip）是出现在表单（Form）或窗口标题栏下的通用选项水平列表。

模态窗口（Modal window）是一个从主窗口接管控制权的次级窗口，用户在继续操作之前必须处理它。

# 复习题

+ 1. 标签、按钮和复选框都是
   a. GUI 对象
   c. 小部件
   b. 控件
   d. 以上所有

# 第 12 章 使用控件

+ 2. 所有的控件对象都继承自 ____________________。
a. Form c. ButtonBase
b. Component
d. 以上所有

+ 3. 下列哪项与单选按钮（RadioButton）最相似？
a. ListControl c. 图片框
b. CheckedListBox
d. 按钮

+ 4. 下列哪项项不是常用的控件属性？
a. BackColor c. 语言 (Language)
b. Location
d. Size

+ 5. 你经常用于为另一个控件对象提供描述性文本的控件是 ________________。
a. 标签 (Label) c. 复选框 (CheckBox)
b. 表单 (Form)
d. 消息框 (MessageBox)

+ 6. 下列哪项创建了 firstLabel？
a. firstLabel = new firstLabel();
b. Label = new firstLabel();
c. firstLabel = new Label();
d. firstLabel = Label();

+ 7. 决定用户在 Label 上阅读内容的属性是 ________________。
a. 设置 (Setting) c. 短语 (Phrase)
b. Label
d. Text

+ 8. 下列哪项正确地创建了字体（Font）？
a. FontMyFont = new Font("Arial", 14F, FontStyle.Bold);
b. FontMyFont = new Font("Courier", 13.6);
c. myFont = Font Font new Font("TimesRoman", FontStyle.Italic);
d. Font MyFont = Font(20, "Helvetica", Underlined);

+ 9. 控件的默认事件是 ________________。
a. 当用户操作控件时自动发生或不发生
b. 在 IDE 中设计控件时双击该控件时生成的
c. 不需要参数
d. 当用户用鼠标点击控件时发生

10. 假设你创建了一个名为 myLabel 的 Label。下列哪项将 myLabel 的背景颜色设置为绿色？

+ a. myLabel = BackColor.System.Drawing.Color.Green;
b. myLabel.BackColor = System.Drawing.Color.Green;
c. myLabel.Green = System.DrawingColor;
d. myLabel.Background = new Color.Green;

11. 复选框（CheckBox）和单选按钮（RadioButton）对象之间的区别之一是？

+ a. 单选按钮继承自 ButtonBase；复选框不继承。
b. 一次只能选择一个单选按钮。
c. 一个表单上只能出现一个复选框。
d. 单选按钮不能放置在分组框中；复选框可以。

12. 单选按钮的 Checked 属性可以持有值

+ a. true 和 false                c. 0 和 1
b. Checked 和 Unchecked        d. Yes, No 和 Undetermined

13. 你可以显示位图或 JPEG 图像的控件是(n)

+ a. DisplayModule             c. BitmapControl
b. 图片框 (PictureBox)                   d. ImageHolder

14. ListBox, ComboBox 和 CheckedListBox 对象继承自哪个家族？

+ a. ListControl                 c. ButtonBase
b. List                                 d. ListBase

15. 下列哪些属性与 ListBox 相关但不与 Button 相关？

+ a. BackColor                  c. Location
b. SelectedItem                d. IsSelected

16. 通过 ListBox，你可以允许用户选择 ____________________。

+ a. 仅选择一个选项             c. 以上两者任其一
b. 多项选择         d. 以上均不是

17. 你可以使用 ________________  方法向 ListBox 添加项。

+ a. AddList()                    c. List()
b. Append()                     d. Add()

# 第 12 章 使用控件

18. 单选按钮（RadioButton）的 Checked 属性包含
a. 被选中项的位置
b. 被选中项的值
c. 一个指示项是否被选中的布尔值
d. 被选中项的数量

19. 当你创建一个 ListBox 时，它的 SelectionMode 是
a. Simple
b. Multi
c. Drop
d. false

20. 出现在表单（Form）或窗口标题栏下的通用选项水平列表是
a. 菜单条 (menu strip)
b. 标题栏 (title bar)

# 编程练习

+ 1. 创建名为 DaySelector 的项目。其 Form 包含两个 ListBox——一个包含至少四个名称，另一个包含至少四个尺寸。让每个列表的第一个项为默认值。

+ 2. 创建名为 BreezyApartments 的项目，包含一个用于租赁服务的 Form。允许用户选择卧室数量、浴室数量。在用户做出选择后，显示月租金，该租金是根据一间一室、二室或三室公寓每月每月 $450、$550 或 $700 的基础价格计算的。如果浴室大于一个，则在基础价格增加 $75。

+ 3. 创建名为 VacationPlanner 的项目，用于提供全包服务的的热带度假村。该项目包含一个 Form，允许用户在每个类别——出发城市、房型和餐食计划中至少选择一个选项。为每个选择分配不同的价格，并在用户点击按钮时显示总额。

+ 4. 创建名为 CarDealer 的项目，包含一个用于汽车经销商的 Form。包含至少三个车型的选项。用户做出选择后，跳转到一个包含所选机型信息的新 Form。

+ 5. 创建名为 AnnualBudget 的项目，包含一个带有 LinkLabel 的 Form。一个链接打开电子表格，其他链接访问你的网站。在 Form 上包含 Label 以解释每个链接。你可以创建一个包含几个年度预算数字的电子表格，也可以使用第 12 章中的 AnnualBudget.xls 文件。

+ 6. 创建名为 TinasCustomTees 的项目，包含一个生产 T 恤的公司 Form。允许用户从至少四种尺寸中选择（价格不同），并从至少三种颜色中选择。当用户选择尺寸时调整最终显示价格，并在选择不同尺寸时更改框架的背景颜色。此外，允许用户从日历（MonthCalendar）中选择订单日期并显示三天后的日期。

+ 7. 创建名为 MenuStripDemo2 的项目，基于第 12 章下载的学生文件中的 MenuStrip 项目。为当前已编程的菜单选项（字体菜单中的两个选项和颜色菜单中的三个选项）添加适当的功能。

