

## 第22章

在向 Customers 选项卡页面添加表格后，在从“数据源”窗口将下一个表格拖到其面板之前，先切换到下一个选项卡。当你在另外两个选项卡页面的面板上添加了适当的表格后，它们各自都包含一个 DataGridView 控件，但没有 BindingNavigator 控件——这没有被添加，因为你在添加 Customers 表格时已经有一个了。你可以从“工具箱”窗口向这些选项卡页面添加 BindingNavigator 控件，但有一个快捷方式可以使用。单击 Customers 选项卡页面上的 BindingNavigator 控件并按 Ctrl+C 将其复制到剪贴板。切换到其中一个其他选项卡页面，选择其面板，然后按 Ctrl+V 将控件从剪贴板复制到选项卡页面的面板上。切换到第三个选项卡页面，选择其面板，然后再次按 Ctrl+V 在该选项卡页面的面板上添加一个 BindingNavigator 控件。然后你可以将三个 BindingNavigator 控件的 Dock 属性值都设置为 Fill。

这两个被复制的 BindingNavigator 控件的 BindingSource 属性设置不正确，因此选择每个控件的该属性的值字段并从下拉列表中选择正确的 BindingSource 组件。你应该为 Employees 选项卡页面上的控件选择 EmployeesBindingSource，为 Products 选项卡页面上的控件选择 ProductsBindingSource。

如果你按 Ctrl+F5 构建并执行示例，你应该会看到图 22-26 所示的应用程序窗口。

![](img/2359b0c604600c58fba3539c738a356e_1169_0.png)

所有这些都无需任何编码即可实现。我认为你会同意，这对于生成访问数据源的应用程序来说是一个惊人的能力。

## 摘要

这是在 Windows Forms 应用程序中访问数据源的能力的简要介绍。你还可以做更多的事情，但你应该会发现你现在已经对如何使用设计功能在窗体上组装控件以及数据访问所涉及的控件如何协同工作有了一个很好的概念。你在独自进入其他领域时不会遇到太多问题。

本章中你学习到的关键点包括：

- 数据源可以是关系数据库、Web 服务或对象。
- 派生自 System::Data::DataSet 类的类用于封装数据源，而派生自 System::Data::DataTable 类的类封装数据源中的表。
- DataTable 对象中的数据行由 System::Data::DataRow 类型的对象表示，而列的架构由 System::Data::DataColumn 类型的对象描述。
- 对数据源的连接和访问数据的命令被封装在一个称为表适配器的组件中。
- 你在窗体上使用 DataGridView 控件以矩形网格的形式显示数据。
- 你可以将 DataGridView 控件绑定到数据源以显示表的內容。你也可以以非绑定模式使用 DataGridView 控件来显示源自你程序的数据。
- 你可以自定义 DataGridView 控件以修改行、列、标题和单个单元格的显示方式。
- BindingSource 组件在数据源和窗体上的控件之间提供接口。BindingSource 组件可以将表中的列链接到窗体上的单个控件，或将表的内容链接到 DataGridView 控件。
- BindingNavigator 控件提供用于导航通过 BindingSource 组件访问的数据的工具栏。

## 练习

你可以从 http://www.wrox.com 下载本书示例的源代码以及以下练习的解决方案。

- 1. 修改 Ex22_04 使列标题以 12 点斜体字体显示。
- 2. 修改 Ex22_05 使列宽足以容纳每个单元格中的文本。
- 3. 修改 Ex22_05 使每个选项卡页面上的交替数据行显示为阴影。
- 4. 创建一个 Windows Forms 应用程序，显示 Northwind 数据库中的 Suppliers 表。

![](img/2359b0c604600c58fba3539c738a356e_1172_0.png)

## C++ 关键字

关键字在 C++ 语言中具有特殊意义，因此你不得在程序中使用它们作为名称。Visual C++ 2005 编译器编译用 ISO/ANSI C++ 编写的程序以及符合 C++/CLI 规范的为 CLR 编写的程序，因此编译器识别 ISO/ANSI C++ 定义的关键字集以及 C++/CLI 定义的额外关键字集。虽然在原生 C++ 中编程，你只需关心 ISO/ANSI C++ 关键字。当为 CLR 编写程序时，你需要同时了解这两组关键字。

### ISO/ANSI C++ 关键字

ISO/ANSI C++ 语言规范定义了以下关键字：

| asm | false | sizeof |
| auto | float | static |
| bool | for | static_cast |
| break | friend | struct |
| case | goto | switch |
| catch | if | template |
| char | inline | this |
| class | int | throw |
| const | long | true |
| const_cast | mutable | try |
| continue | namespace | typedef |

表续于下一页

### 附录 A

| default | new | typedef |
| --- | --- | --- |
| delete | operator | typename |
| do | private | union |
| double | protected | unsigned |
| dynamic_cast | public | using |
| else | register | virtual |
| enum | reinterpret_cast | void |
| explicit | return | volatile |
| export | short | wchar_t |
| extern | signed | while |

## C++/CLI 关键字

C++/CLI 语言规范除了为 ISO/ANSI C++ 定义的关键字外，还定义了以下关键字：

| enum class | enum struct | for each | gcnew |
| --- | --- | --- | --- |
| interface class | interface struct | nullptr | ref class |
| ref struct | value class | value struct |

请注意，词对是关键字，而不一定是单个单词；例如，for each 是一个关键字，但 each 不是。

C++/CLI 语言还定义了一些在某些情况下具有上下文相关含义的标识符，但它们不是关键字。这些是：

| abstract | delegate | event | finally |
| generic | in | inotify | internal |
| literal | override | property | sealed |
| where |  |  |  |

## ASCII 代码

前 32 个 ASCII（美国信息交换标准代码）字符提供控制功能。在下面的表中，仅包含了前 128 个 ASCII 字符。其余 128 个字符包括更多特殊符号和国家字符集的字母，因此有许多变体可满足广泛的语言环境。

| Decimal | Hexadecimal | Character | Control |
|---|---|---|---|
| 000 | 00 | null | NUL |
| 001 | 01 | ☺ | SOH |
| 002 | 02 | ● | STX |
| 003 | 03 | ♥ | ETX |
| 004 | 04 | ♦ | EOT |
| 005 | 05 | ♣ | ENQ |
| 006 | 06 | ♠ | ACK |
| 007 | 07 | • | BEL (Audible bell) |
| 008 | 08 |  | Backspace |
| 009 | 09 |  | HT |
| 010 | 0A |  | LF (Line feed) |
| 011 | 0B |  | VT (Vertical tab) |
| 012 | 0C |  | FF (Form feed) |
| 013 | 0D |  | CR (Carriage return) |
| 014 | 0E |  | SO |
| 015 | 0F | ░ | SI |

表续于下一页

## 附录 B

| Decimal | Hexadecimal | Character | Control |
|---|---|---|---|
| 016 | 10 |  | DLE |
| 017 | 11 |  | DC1 |
| 018 | 12 |  | DC2 |
| 019 | 13 |  | DC3 |
| 020 | 14 |  | DC4 |
| 021 | 15 |  | NAK |
| 022 | 16 |  | SYN |
| 023 | 17 |  | ETB |
| 024 | 18 |  | CAN |
| 025 | 19 |  | EM |
| 026 | 1A | → | SUB |
| 027 | 1B | ← | ESC (Escape) |
| 028 | 1C | L | FS |
| 029 | 1D |  | GS |
| 030 | 1E |  | RS |
| 031 | 1F |  | US |
| 032 | 20 |  | space |
| 033 | 21 | ! |  |
| 034 | 22 | " |  |
| 035 | 23 | # |  |
| 036 | 24 | $ |  |
| 037 | 25 | % |  |
| 038 | 26 | & |  |
| 039 | 27 | ' |  |
| 040 | 28 | ( |  |
| 041 | 29 | ) |  |
| 042 | 2A | * |  |
| 043 | 2B | + |  |
| 044 | 2C | , |  |
| 045 | 2D | - |  |
| 046 | 2E | . |  |

