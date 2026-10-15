

# 事件

| 组件 | 操作 | 插入点 | 更改 | 文档 | 项目 | 列表选择 | 窗口 | 其他 |
|---|---|---|---|---|---|---|---|---|
| JButton | ✓ |  | ✓ |  | ✓ |  |  |  |
| JCheckBox | ✓ |  | ✓ |  | ✓ |  |  |  |
| JColorChooser |  |  | ✓ |  |  |  |  |  |
| JComboBox | ✓ |  |  |  | ✓ |  |  |  |
| JDialog |  |  |  |  |  |  | ✓ |  |
| JEditorPane |  | ✓ |  | ✓ |  |  |  | ✓ |
| JFileChooser | ✓ |  |  |  |  |  |  |  |
| JFrame |  |  |  |  |  |  | ✓ |  |
| JInternalFrame |  |  |  |  |  |  |  | ✓ |
| JList |  |  |  |  |  | ✓ |  | ✓ |
| JMenu |  |  |  |  |  |  |  | ✓ |
| JMenuItem | ✓ |  | ✓ |  | ✓ |  |  | ✓ |
| JOptionPane |  |  |  |  |  |  |  |  |
| JPasswordField | ✓ | ✓ |  | ✓ |  |  |  |  |
| JPopupMenu |  |  |  |  |  |  |  | ✓ |
| JProgressBar |  |  | ✓ |  | ✓ |  |  |  |
| JRadioButton | ✓ |  | ✓ |  |  |  |  |  |
| JSlider |  |  | ✓ |  |  |  |  |  |
| JTabbedPane |  |  | ✓ |  |  |  |  |  |
| JTable |  |  |  |  |  | ✓ |  | ✓ |
| JTextArea |  | ✓ |  | ✓ |  |  |  |  |
| JTextField | ✓ | ✓ |  | ✓ |  |  |  |  |
| JTextPane |  | ✓ |  | ✓ |  |  |  | ✓ |
| JToggleButton | ✓ |  | ✓ |  | ✓ |  |  |  |
| JTree |  |  |  |  |  |  |  | ✓ |

# 图 K.2 特定组件生成的特定事件

- 工具栏是一个将多个组件分组为一行或一列的容器。工具栏通常包含对应于也可以通过其他方式完成任务的按钮。工具栏可以从其最初存在的容器中拖离到自己的窗口中。
- 内部框架是一个容器，其操作方式类似于常规框架，但仅在另一个窗口内。内部框架可以在窗口内移动并与其他内部框架重叠。内部框架可用于创建类似 GUI 桌面的感觉，其中组件可以根据用户选择进行排列。

- 分层窗格是一个容器，它考虑到第三个维度，即深度，来组织其包含的组件。当组件添加到分层窗格时，其深度会被指定。如果组件重叠，则每个组件的深度值决定哪个在上。

- 进度条可用于指示特定活动的进度。用户通常不会与进度条交互，只是查看它以确定任务，例如图像加载，已进展到何种程度。

- 表格是 Java GUI 组件，以表格格式显示数据。Java 表格可以完全定制以提供精确的组织和呈现。它还可以允许用户编辑数据。Java 表格实际上不包含或存储数据；它只是以有组织的方式向用户呈现数据。

- 树是一个组件，以层次结构视图呈现数据。像表格一样，它实际上不存储数据；它提供一个有组织的视图，允许用户从高级根节点向下遍历各个分支。

- Java 对文本处理的支持是丰富的。我们已经使用了基本的文本组件，如文本字段和文本区域，但这只是开始。Java 标准类库（特别是 Swing API）有大量支持文本的显示、编辑和操作的类。

与本书中介绍的所有主题一样，我们鼓励您更详细地探索这些问题。特别是 Java GUI 的世界，为您提供了许多发现的机会。

此页 intentionally left blank

# Java 语法

本附录包含语法图， collectively 描述了 Java 语言元素可以构建的方式。矩形表示在另一个语法图中进一步定义的内容，而椭圆形表示字面单词或字符。

# 编译单元

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_746_0.png)

# 包声明

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_746_1.png)

# 导入声明

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_746_2.png)

# 类型声明

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_746_3.png)

# 类声明

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_747_0.png)

# 类关联

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_747_1.png)

# 类体

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_747_2.png)

# 类成员

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_747_3.png)

# 接口声明

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_747_4.png)

# 接口体

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_747_5.png)

# 接口成员

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_747_6.png)

# 字段声明

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_748_0.png)

# 变量声明符

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_748_1.png)

# 类型

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_748_2.png)

# 修饰符

# 原始类型

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_748_3.png)

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_748_4.png)

# 数组初始化器

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_748_5.png)

# 名称

# 名称列表

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_748_6.png)

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_748_7.png)

# 块

# 块语句

# 局部变量声明

# 语句

# If 语句

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_751_0.png)

# Switch 语句

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_751_1.png)

# Switch 情况

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_751_2.png)

# While 语句

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_751_3.png)

# Do 语句

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_751_4.png)

# For 语句

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_751_5.png)

# For 初始化

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_751_6.png)

# For 更新

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_751_7.png)

# 基本赋值

# Return 语句

# Throw 语句

# Try 语句

# Synchronized 语句

# 空语句

# Break 语句

# Continue 语句

# 带标签的语句

# 表达式

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_753_0.png)

# 主表达式

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_753_1.png)

# 主后缀

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_753_2.png)

# 参数

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_754_0.png)

# 分配

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_754_1.png)

# 数组维度

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_754_2.png)

# 语句表达式

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_754_3.png)

# 赋值

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_754_4.png)

# 一元表达式

# 前缀表达式

# 后缀表达式

# 字面量

# 整数字面量

# 十进制整数字面量

# 八进制整数字面量

# 十六进制数字

# 十六进制整数字面量

# 浮点字面量

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_757_0.png)

# 指数部分

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_757_1.png)

# 浮点后缀

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_757_2.png)

# 字符字面量

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_757_3.png)

# 布尔字面量

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_757_4.png)

# 字符串字面量

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_757_5.png)

# 转义序列

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_757_6.png)

# 标识符

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_758_0.png)

# Java 字母

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_758_1.png)

* “其他 Java 字母”类别包括除英语之外许多语言的字母。

# Java 数字

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_758_2.png)

* “其他 Java 数字”类别包括 Unicode 中定义的其他数字。

# Unicode 转义*

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_758_3.png)

* 在某些上下文中，Unicode 转义所表示的字符受到限制。

此页 intentionally left blank

# Java 类库

在本书的早期版本中，本附录包含 Java API 的简略参考资料。本附录仍可在 ftp://ftp.aw.com/cseng/authors/lewis/jss7/ 获取，任何希望下载并使用它的人都可以。

更好的解决方案是熟悉官方的完整在线 API 文档，如图 M.1 所示。它包含每个 Java 开发环境可用的每个类、接口和方法 的描述。我们鼓励您花一些时间熟悉该文档的组织和布局。它是在程序开发期间可以依赖的有价值的工具。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_760_0.png)

图 M.1 在线 Java API 文档

