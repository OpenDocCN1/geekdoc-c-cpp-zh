

# 第 10 章 继承简介

特殊处理，40美元的订单收取10美元费用，更高价格的订单收取8美元费用。
创建一个名为 CookieDemo2 的应用程序，演示多个 SpecialCookieOrder 对象。

- 5. a. 创建一个名为 AutomobileDemo 的应用程序，提示用户输入八个 `Automobile` 对象的数据。`Automobile` 类包含 ID 编号、品牌、年份和价格的自动实现属性。重写 `ToString()` 方法以返回 `Automobile` 的所有信息。在数据输入期间，如果任何 ID 编号重复，重新提示用户。按 ID 编号对对象进行排序，并显示所有数据以及价格总和。
- b. 以 `Automobile` 类为基类，派生出一个 `FinancedAutomobile` 类，它包含 `Automobile` 的所有数据，以及用于存储融资金额和利率的字段。重写父类的 `ToString()` 方法以包含子类的额外数据。创建一个名为 AutomobileDemo2 的程序，包含一个有四个 `Automobile` 对象的数组。提示用户输入所有必要数据，确保 ID 编号不重复且不允许融资金额大于汽车价格。按 ID 编号对所有记录进行排序，并显示所有汽车的总价格和总融资金额。
- c. 编写一个名为 AutomobileDemo3 的应用程序，它为 `FinancedAutomobile` 类使用扩展方法。该方法计算并返回 `FinancedAutomobile` 的每月还款额（融资金额的1/24）。应用程序应允许用户输入四个对象的数据，然后显示每个对象的所有数据。

- 6. 创建一个名为 ShapesDemo 的应用程序，创建多个继承自抽象类 `GeometricFigure` 的对象。每个 `GeometricFigure` 包含高度、宽度和面积。为每个字段提供 `get` 和 `set` 访问器，面积除外；面积是计算的且只读的。包含一个名为 `ComputeArea()` 的抽象方法，用于计算 `GeometricFigure` 的面积。创建三个类：
- `Rectangle`（矩形）是一个 `GeometricFigure`，其面积通过宽度乘以高度来决定。
- `Square`（正方形）是一个 `Rectangle`，其宽度和高度相同。提供一个构造可以同时接受高度和宽度的构造函数，如果它们不等，则强制它们相等。提供第二个仅接受一个维度的构造函数，并将其同时用于高度和宽度。`Square` 类使用 `Rectangle` 的 `ComputeArea()` 方法。
- `Triangle`（三角形）是一个 `GeometricFigure`，其面积通过宽度乘以高度来决定。

在 `ShapesDemo` 类中，在每个对象创建后，将其传递给一个接受 `GeometricFigure` 参数的方法，并在其中显示数据。更改某些图形的维度，并再次将每个传递给显示方法。

# 练习

- 7. 创建一个名为 RecoveringDemo 的应用程序，声明三种类型之一：`Patient`（病人）、`Upholster`（装饰家具师）和 `FootballPlayer`（足球运动员）。创建一个名为 `IRecoverable` 的接口，包含一个方法 `Recover()`。创建名为 `Patient`、`Upholster` 和 `FootballPlayer` 的类，使每个实现 `IRecoverable`。为每个类的 `Recover()` 方法显示适当的消息。例如，`Patient` 的 `Recover()` 方法可能会显示“我正在好起来”。

- 8. 创建一个名为 TurningDemo 的应用程序，创建四个类的实例：`Page`（页）、`Corner`（角）和 `Leaf`（叶）。创建一个名为 `ITurnable` 的接口，包含一个方法 `Turn()`。`Page`、`Corner` 和 `Leaf` 类实现 `ITurnable`。为每个类的 `Turn()` 方法显示适当的消息。例如，`Page` 的 `Turn()` 方法可能会显示“你在书中翻了一页”。

- 9. 编写一个名为 SalespersonDemo 的程序，使用 `RealEstateSalesperson`（房地产销售员）和 `Girl1Scout`（一级童军）类实例化对象。演示每个对象都可以适当使用 `Sale()` 方法。此外，对每个对象使用两次或三次 `MakeSale()`，并显示每个对象数据字段的最终内容。首先，创建一个抽象类 `Salesperson`。包含字段的属性。包含一个返回字符串的方法，用于持有销售员的全名——姓和名用空格隔开。然后执行以下任务：

- 创建 `Salesperson` 的两个子类：`RealEstateSalesperson` 和 `Girl1Scout`。`RealEstateSalesperson` 类包含美元总价值和总赚取佣金的字段（两者均初始化为 0），以及类构造函数所需的佣金率字段。`Girl1Scout` 类包含一个用于存储销售饼干盒数的字段，初始化为 0。为每个字段包含属性。
- 创建一个名为 `ISellable` 的接口，包含两个方法：`SalesSpeech()` 和 `MakeSale()`。在 `RealEstateSalesperson` 和 `Girl1Scout` 中，实现 `SalesSpeech()` 以显示对象类可以使用的适当单句或双句。

在 `RealEstateSalesperson` 类中，实现 `MakeSale()` 方法以接受房屋的整数值，将该值加上 `RealEstateSalesperson` 的总销售额中，并计算赚取的佣金。在 `Girl1Scout` 类中，实现 `MakeSale()` 方法以接受代表销售饼干盒数的整数，并将其加上总字段中。

# 调试练习

- 1. 可下载学生文件 `Chapter.10` 文件夹中的以下每个文件都有语法或逻辑错误。在每种情况下，确定问题并修复程序。修正错误后，使用相同的文件名并在其前面加上 `Fixed` 保存每个文件。例如，`DebugTen01.cs` 将变为 `FixedDebugTen01.cs`。
- a. DebugTen01.cs
- b. DebugTen02.cs
- c. DebugTen03.cs
- d. DebugTen04.cs

# 案例分析

- 1. 在第99题中，你为 Greenville Idol 比赛创建了一个 `Contestant`（参赛者）类。该类包含参赛者的姓名、天赋代码和天赋描述。比赛变得非常受欢迎，因此为儿童、青少年和成人建立了不同参赛费的独立比赛。修改 `Contestant` 类包含一个持有分类费用的字段，并添加 get set 访问器。扩展 `Contestant` 类创建三个子类：`ChildContestant`（儿童参赛者）、`TeenContestant`（青少年参赛者）和 `AdultContestant`（成人参赛者）。儿童参赛者12岁及以下，参赛费为15美元。青少年参赛者13至17岁（含），参赛费为20美元。在每个子类中，设置参赛费字段为正确值，并重写 `ToString` 方法以返回包含所有参赛者数据（包括分类和参赛费）的字符串。修改 GreenvilleRevenue 程序执行以下任务：

- 程序提示用户输入今年比赛的参赛人数，必须在0到30之间。程序继续提示用户，直到输入有效值。
- 程序提示用户输入参赛者的姓名、年龄和天赋代码。在提示天赋代码的同时，显示有效分类列表。根据每个参赛者输入的年龄，创建正确类型的对象（成人、青少年或儿童），并将其存储在 `Contestant` 对象数组中。
- 数据输入完成后，显示预期总收入，即所有参赛者参赛费的总和。
- 数据输入完成后，显示有效的天赋分类，然后持续提示用户输入代码，并显示分类中所有参赛者的数据。如果输入的代码不是字符或有效代码，则显示适当的消息。

- 2. 在第9章中，你为 Marshall Murals 创建了一个 `Mural`（壁画）类。该类持有客户的姓名、壁画代码和描述。现在，为 `Mural` 类添加一个持有价格的字段。通过扩展 `Mural` 类来创建 `InteriorMural`（室内壁画）和 `ExteriorMural`（室外壁画），并在这些类中放置定义壁画价格的语句。（壁画价格取决于月份，如第9章案例分析中所示。）还为这些子类创建 `toString()` 方法，以返回包含壁画所有相关数据的字符串。

修改 `MarshallsRevenue` 程序执行以下任务：

- 程序提示用户输入月份、计划的室内壁画数量和计划的室外壁画数量。在每情况下，程序继续提示用户直到输入有效值。
- 程序提示用户输入室内室外壁画的客户姓名和壁画代码。在提示壁画代码的同时，显示有效分类列表。
- 数据输入完成后，程序显示室内、室外所有壁画的总收入。
- 数据输入完成后，程序显示有效的壁画分类，然后持续提示用户输入代码，并使用 `toString()` 方法显示分类中所有壁画的详情。如果输入的代码不是字符或有效代码，则显示适当的消息。
