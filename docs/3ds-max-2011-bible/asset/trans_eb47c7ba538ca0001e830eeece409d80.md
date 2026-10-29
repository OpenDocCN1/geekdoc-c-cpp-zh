

## 使用表达式控制器进行动画制作和连接参数

Expressions（表达式）是你试图唤醒自己时在镜子里做出的表情；但在 Max 中，表达式是一系列用于定义对象行为的方程。Max 表达式可以简单到将两个数字相加，也可以复杂到包含多行 MAXScript。不过，表达式可以帮助你创建自定义的动画反应。

虽然 Max 表达式可以与任意 Max 微调器配合使用，但它们主要用于 MAXScript 脚本或 Expression controller（表达式控制器）中。Expression controller 是一种专用控制器，可让你使用脚本表达式控制对象的行为。

本章接下来将介绍一种基于对象参数驱动动画的独特方式。一个对象的参数可以连接到另一个对象的参数，这样当一个参数发生变化时，与之连接的参数也会随之变化。例如，你可以将灯光的 On/Off 参数连接到开关的移动。所有可以制作动画的参数都可以进行连接。

只要你处理的是参数，Max 就提供了多个用于查看和处理可用参数的实用工具，其中包括 Parameter Collector（参数收集器）。如果 Parameter Collector 没有收集到你确切需要的参数，你还可以创建自己的自定义参数。

## 本章内容

- 使用 Numerical Expression Evaluator（数值表达式求值器）
- 了解 Expression controller 界面
- 了解运算符、变量和函数
- 使用操纵器辅助对象连接参数
- 收集参数
- 创建自定义参数

## 使用微调器中的表达式

虽然本章主要介绍 Expression controller 的使用方法，但 Expression Controller Interface（表达式控制器界面）并不是唯一可以使用表达式的地方。你还可以使用 Numerical Expression Evaluator（数值表达式求值器）在微调器控件中输入表达式，如图 35.1 所示。选择一个微调器并按下 Ctrl+N，即可访问这个简单的对话框。

### 交叉引用

另一个经常使用表达式的地方是 Parameter Wiring（参数连接）对话框，本章后面会介绍该对话框。

## 图 35.1

Numerical Expression Evaluator 对话框允许你为微调器输入表达式。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_927_0.png)

要使用此求值器，只需在字段中输入表达式；结果会显示在结果字段中。结果字段会随着你输入表达式而更新。如果输入有误，Result 字段会被清空。Paste 按钮会将结果值放入微调器中，Cancel 按钮则会关闭对话框而不进行任何更改。

### 提示

你可以通过输入字母 R 和一个数值，在微调器中输入相对值。例如，如果球体对象的 Segments 值为 32，那么输入 R20 会将该值更改为 52，而输入 R-20 会将该值更改为 12。

## 了解 Expression controller 界面

Expression（表达式）是指一种数学表达式或简单公式，它根据其他值计算出一个值。这些表达式可以很简单，例如根据踏板的旋转来移动自行车；也可以很复杂，例如根据船下方的波浪计算船只在海面上的正弦平移。

你几乎可以将任何值用作表达式中的变量，包括对象坐标、修改器参数以及灯光和材质设置。表达式的结果会在每一帧中进行计算，并用于影响场景中的各种参数。你可以在表达式中加入帧数和时间变量，使动画结果在整个序列中重复。

### 注意

虽然 Expression controller 不如 Script controller（脚本控制器）强大，但它比 Script controller 快得多，因为不需要任何编译时间。

在所有可用的控制器中，Expression controller 的可能性几乎无穷无尽，足以写满一整本书。本节将介绍构建表达式的基础知识，并包含几个示例。

Expression controller 只是众多用于自动化动画的控制器之一。该控制器允许你通过数学公式或表达式定义对象的变换方式，并且可以将其应用于对象的任意轨迹。它在控制器列表中的名称取决于所分配轨迹的类型，可能显示为 Position Expression、Rotation Expression、Scale Expression、Float Expression 或 Point3 Expression controller。

## 第 35 章：使用 Expression controller 进行动画制作和连接参数

在轨迹上使用 Expression controller 之前，必须先将其分配给轨迹。你可以使用 Motion 面板或 Track View，将控制器分配给 Position、Rotation 和 Scale 轨迹；也可以在 Track View 中右键单击轨迹，然后选择 Assign Controller 选项来应用控制器。分配控制器后，Expression Controller 对话框会立即打开；你也可以随时右键单击轨迹，并从弹出菜单中选择 Properties 来访问该对话框。例如，在场景中选择一个对象，打开 Motion 面板，然后选择 Position 轨迹。接着单击 Assign Controller rollout 顶部的 Assign Controller 按钮，并从 Controllers 列表中选择 Position Expression。这会打开 Expression Controller 对话框。

你可以使用此对话框定义变量并编写表达式。如图 35.2 所示，该对话框包含四个独立窗格，用于显示 Scalar 和 Vector 变量列表、构建表达式，以及输入表达式说明。

## 图 35.2

你可以使用 Expression controller 构建表达式并定义其结果。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_928_0.png)

### 定义变量

*变量*是不同值的占位符。例如，为球体的半径创建一个名为“r”的变量，可以将用于将其尺寸加倍的表达式从“获取球体的半径并将其乘以二”简化为“r 乘以 2”。

要将变量添加到 Expression Controller 对话框的列表窗格中，请在 Name 字段中输入名称，选择 Scalar 或 Vector 选项类型，然后单击 Create 按钮；新变量会显示在 Scalars 或 Vectors 列表中。要删除变量，请从列表中选择该变量，然后单击 Delete 按钮。Tick Offset 值是添加到当前时间上的时间值，可用于延迟变量。

你可以将任何新变量分配给常量或控制器。将变量分配给常量，与直接在表达式中输入该常量的值作用相同。常量变量只是为了方便编写表达式。Assign to Controller 按钮会打开 Track View Pick 对话框，如图 35.3 所示，你可以在其中为变量选择特定的控制器轨迹，例如对象的位置轨迹。

## 图 35.3

Track View Pick 对话框显示场景中的所有轨迹。可以选择的轨迹以黑色显示。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_929_0.png)

将变量分配给控制器后，你就可以根据场景中的其他对象为所选对象制作动画。具体操作是：创建一个变量，并将其分配给另一个对象的动画轨迹。例如，如果创建一个名为 boxPos 的 Vector 变量，并将其分配给盒子对象的 Position 轨迹，那么在表达式中就可以使用该变量，根据盒子的位置来控制被分配对象的运动。

### 构建表达式

你可以直接在 Expression Controller 对话框的 Expression 窗格中输入表达式。要使用变量列表（Scalars 或 Vectors）中的命名变量，请在 Expression 窗格中输入其名称。诸如 F 和 NT 等预定义变量（将在本章后面介绍）不需要在变量窗格中定义。Function List 按钮会打开一个函数列表，如图 35.4 所示，你可以在其中查看能够包含在表达式中的函数。该列表仅供显示；你仍然需要在 Expression 窗格中输入函数。

### 提示

学习不同表达式语法的一种方法，是在 MAXScript Listener 窗口中启用 MacroRecorder，并在视口中执行操作时查看上方的窗格。

### 注意

Expression 窗格会忽略所有空白字符，因此你可以使用换行和空格，让表达式更容易查看和阅读。

