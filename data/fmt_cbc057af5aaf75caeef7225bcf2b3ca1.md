
- c. 输出控件（用于项目金额、小计、销售税和总计）是 `ReadOnly` 属性为 `True` 的 `TextBox`。

- d. 将表单的 `AcceptButton` 属性设置为计算（Calculate）按钮。

- 为程序需要管理的控件命名。包括所有 `NumericUpDown` 控件、所有的 `TextBox` 以及按钮（Button）。

当用户点击按钮时，让程序执行：

- 将每个项目的数量值乘以其单价值，并将结果显示在对应的项目金额 `TextBox` 中。

- 将所有项目金额值相加，并将结果显示在小计 `TextBox` 中。

- 将小计值乘以输入的税率，并将结果显示在销售税 `TextBox` 中。

- 将小计、销售税和运费值相加，并将结果显示在总计 `TextBox` 中。

通过三个步骤很容易完成：

- 从用户处获取输入值并存储在变量中。因为它们已经是数值，代码不需要从 `NumericUpDown` 控件的 `Value` 属性中解析值。程序确实需要解析 `TextBox` 中的值以将其转换为 `decimal` 值：

```csharp
// 获取输入值；
decimal quantity1 = qty1NumericUpDown.Value;
decimal quantity2 = qty2NumericUpDown.Value;
decimal quantity3 = qty3NumericUpDown.Value;
decimal quantity4 = qty4NumericUpDown.Value;
```

# 182 | 第11节 使用变量和执行计算

```csharp
decimal priceEach1 = decimal.Parse(priceEach1TextBox.Text);
decimal priceEach2 = decimal.Parse(priceEach2TextBox.Text);
decimal priceEach3 = decimal.Parse(priceEach3TextBox.Text);
decimal priceEach4 = decimal.Parse(priceEach4TextBox.Text);
decimal taxRate = decimal.Parse(taxRateTextBox.Text);
decimal shipping = decimal.Parse(shippingTextBox.Text);
```

2. 执行计算。在本次练习中，计算非常简单，为了程序为每个结果使用单独的变量而不是一次性相加：

```csharp
// 计算结果。
decimal total1 = quantity1 * priceEach1;
decimal total2 = quantity2 * priceEach2;
decimal total3 = quantity3 * priceEach3;
decimal total4 = quantity4 * priceEach4;
decimal subtotal = total1 + total2 + total3 + total4;
decimal salesTax = subtotal * taxRate;
decimal grandTotal = subtotal + salesTax + shipping;
```

3. 显示结果。程序使用 `ToString("C")` 以货币格式显示值：

```csharp
// 显示结果。
total1TextBox.Text = total1.ToString("C");
total2TextBox.Text = total2.ToString("C");
total3TextBox.Text = total3.ToString("C");
total4TextBox.Text = total4.ToString("C");
subtotalTextBox.Text = subtotal.ToString("C");
salesTaxTextBox.Text = salesTax.ToString("C");
grandTotalTextBox.Text = grandTotal.ToString("C");
```

## 练习

1. [WPF] 使用 WPF 程序重复此“尝试一下”。

2. 当用户更改计算中使用的值时，如果程序显示旧的计算值，会让人产生困惑。复制你为练习编写的程序并进行以下修改：

- 禁用计算（Calculate）按钮。

- 当用户修改任何值时，清空已计算的 `TextBox` 并启用计算按钮。

- 在显示计算值后，再次禁用按钮。

3. [WPF] 使用你为练习1编写的程序重复练习2。提示：当程序启动时，所有的 `TextBox` 都会触发 `Changed` 事件，导致程序无法清空。为了避免崩溃，请使用事件处理程序检查窗口是否已加载：

```csharp
if (!IsLoaded) return;
```

4. 复制你为练习2编写的程序。目前，如果缺少任何输入值，程序将会崩溃。修改程序，仅在所有需要的值时启用计算按钮：

- 在事件处理程序禁用禁用按钮。

- 在重新启用按钮之前，使用如下代码：

```csharp
if (priceEach1TextBox.Length == 0) return;
```

如果用户输入“ten”等非数值值，程序将崩溃。现在不要担心，你将在第二节学习如何修复。

5. [WPF] 使用你为练习3编写的程序重复练习4。

6. 你为练习4编写的程序不理解货币值。例如，如果在 Price `TextBox` 中输入 $6.00 并点击计算，程序将崩溃。修复它。提示：

- 使用如下代码允许货币值、千位分隔符、前缀和后缀：

```csharp
decimal priceEach = decimal.Parse(priceEach1TextBox.Text, System.Globalization.NumberStyles.Currency);
```

- 不要更改数量值或税率值，因为它们不是货币值![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_222_0.png)。

7. [WPF] 使用你为练习5编写的程序重复练习6。

8. 创建一个如图所示的程序。当用户勾选 A 或 B `TextBox` 时，程序应该勾选或取消勾选结果 `TextBox`。例如，如果 A 和 B 都勾选，则 B 应该被勾选。提示：

- 将结果 `TextBox` 的属性设置为布尔表达式。例如：

```csharp
andBCheckBox.Checked = aCheckBox.Checked && bCheckBox.Checked;
```

- 为了制作 `CheckBox` 的标题，在其 `Text` 属性中放置 "A & B"。

- 当最后一个 `CheckBox` 与其他一个同时被勾选时会触发。哪种方式更合理？

9. 程序可以通过多种方式获取操作系统信息。有用的值包括：

- `Environment.UserName`——当前用户名。

- `DateTime.Now.ToShortTimeString()`——短格式当前时间。

- `DateTime.Now.ToShortDateString()`——短格式当前日期。

# 第11节 使用变量和执行计算

创建一个程序，在启动时通过显示如图11-3所示的消息框来问候用户。（提示：你需要拼接字符串。）

10. 复制你为练习9编写的程序，让其在 `Label` 中显示问候信息。

11. 创建一个程序判断 `12345 * 54321` 是否等于 `22222 * 33333`。在三个 `Label` 中显示 `12345 * 54321` 的结果、`22222 * 33333` 的结果以及 `12345 * 54321 = 22222 * 33333` 的结果。最终值应该是 true 或 false。（提示：使用 `ToString` 将布尔转换为字符串。）

12. 创建一个将摄氏度转换为华氏度的程序。它应该有两个带有按钮的 `TextBox`。当用户在 Celsius `TextBox` 中输入值并点击其按钮时，程序将该值转换为华氏并将结果显示在另一个 `TextBox` 中。另一个按钮将华氏度转换为摄氏度：

- °F = °C * 9 / 5 + 32 以及 °C = (°F - 32) * 5 / 9。

- -40°C 有什么特别之处？

13. 创建一个在美元、英镑、欧元、日元、卢比和法之间之间的转换器。为转换因子创建常量（或在线查找当前汇率）：

```csharp
// 以美元计算的汇率。
const decimal eurPerUs = 0.68M;
const decimal GBPPerUs = 0.63M;
const decimal jpyPerUs = 89.16M;
const decimal inPerUs = 47.24M;
const decimal chfPerUs = 1.03M;
```

为了让程序中的每个事件处理程序都能使用常量，将它们放置在任何事件处理程序的外部（放在 Form 方法之后即可）。为每种货币创建一个 `TextBox` 和按钮。当用户点击按钮时，程序应该：

- 获取对应 `TextBox` 中的值。

- 将该值转换为美元。

- 使用美元值计算其他货币值。

- 显示结果。

14. 创建一个与你为练习13制作的类似的程序，但让它在英寸、英尺、码、米、厘米和公里之间转换。

15. [游戏] 创建一个包含 `Picture`（包含一张会飞行的图片）和 `Timer`（间隔 `Interval = 50`）的程序。

在每个事件处理程序的外部代码中，声明两个名为 `Theta` 和 `Dtheta` 的 `double` 类型变量，分别初始化为 0 和 `Math.PI / 30`。（`System` 包含许多常用的数学值和方法，包括 `Sin` 和 `Cos`，你稍后会用到）

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_223_0.png)

当用户点击 `PictureBox` 时，启用或禁用 `Timer`。

在 `Timer` 的 `Tick` 事件处理程序中，将 `PictureBox` 移动到点：`(100 + 100 * Math.Cos(Theta), 100 + 75 * Math.Sin(Theta))`。然后给 `Theta` 加上 `Delta`。（如有必要请转换数据类型。）

- 16. [游戏] 复制你为练习 15 构建的程序，并添加一个 `Minimum = 1`、`Maximum = 10` 且 `LargeChange = 1` 的 `HScrollBar`。在它的 `Scroll` 事件处理程序中，在只读 `TextBox` 中显示新值，并将 `Timer` 的 `Interval` 属性设置为：`110 - 10 * speedScrollBar.Value`。

- 17. [高级] 处理抛体运动的方法是使用 `Vx` 和 `Vy` 分别表示对象在 X 方向和 Y 方向上的速度。在 `Timer` 的每次 tick 中，将 `Vx` 和 `Vy` 加到对象的当前 X 和 Y 坐标上。对于抛体运动，给 `Vy` 加上一个向下的重力加速度。

对于这个练习，构建一个与图 14-4 所示类似的程序来模拟抛体运动。为了保持程序简单，角度使用度数，速度使用每秒英尺，比例为 1 像素 = 1 英尺。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_224_0.png)

图 14-4

提示：

- 按照图 14-4 所示构建表单。坦克是一个显示在 `PictureBox` 中的图像。还添加一个名为 `moveTimer` 的 `Timer`，并将其 `Interval` 属性设置为 50。

- 在任何事件处理程序之外，创建六个 `float` 变量 `TicksPerSecond`, `X`, `Vx`, `Vy` 和 `Ay`。

- 当用户点击 Fire Button：

    - 使用表单的 `ClientSize` 和 `PictureBox` 的 `Size` 将 `PictureBox` 移动到表单的左下角。

    - 解析用户输入的角度和速度。

    - 使用公式 `radians = -degrees * Math.PI / 180` 将角度从度转换为弧度。

使用以下公式计算每秒 `Timer` tick 的次数：

`TicksPerSecond = 1000 / moveTimer.Interval`

使用以下等式（必要时转换数据类型）计算球每 tick 的初始速度 `Vx` 和 `Vy`（单位为英尺）：

`Vx = speed * Math.Cos(radians) / TicksPerSecond`

`Vy = speed * Math.Sin(radians) / TicksPerSecond`

使用以下计算计算球每 tick 的重力加速度（单位为英尺）：

`Ay = 32 / TicksPerSecond / TicksPerSecond`

- 启用 `Timer`。

  禁用 Fire Button。

  启用 Stop Button。

- 当用户点击 Stop Button 时：

    禁用 `Timer`。

  启用 Fire Button。

  禁用 Stop Button。

- 当 `Timer` 的 `Tick` 事件发生时：

    通过在 `PictureBox` 的 `Left` 属性上加上 `Vx` 并在 `PictureBox` 的 `Top` 属性上减去 `Vy` 来移动坦克弹。（你之所以减去 `Vy`，是因为在表单上 Y 坐标在向上时是减小的。）

    通过减去 `Ay` 来给 `Vy` 加上向下的重力力加速度。

- 如果一切顺利，那么对于 60° 的角度和 120 英尺/秒的速度，坦克弹大约需要 8.5 秒从表单底部掉落（这似乎很长时间，但在此期间球水平方向移动了超过 400 英尺）。

> 注意 请访问 www.wrox.com/go/csharp24hourtrainer2evideos 选择第 11 课在线视频。

## 12

## 调试代码 (Debugging Code)

`Bug` 是导致程序无法产生正确结果的编程错误。程序可能会崩溃、显示错误的数据或执行完全出乎意料的操作，例如删除错误的文件。

在本节中，你将学习如何使用 Visual Studio IDE 提供的优秀调试工具来查找 C# 中的 bug。你将学习不同类型的 bug，并可以在从书籍网站下载的一些带 bug 的示例上练习调试技术。

## 延迟技术 (DEFERRED TECHNIQUES)

遗憾的是，在书的这一阶段，你对编写代码的了解不足以理解和修复某些类型的 bug。例如，如果程序尝试访问数组之外的项，程序就会崩溃，但你直到第 16 节才会学习数组。

那么，既然你还不掌握所有引起和修复某些类型 bug 所需的技术，为什么这一节还要涵盖调试呢？这有两个原因。

首先，上一节是书中第一个部分，你很可能在那里遇到 bug。每当我教编程时，一旦你在第 11 节写了执行计算的代码，学生就开始看到 bug 了。如果你了解一点调试知识，这类 bug 是很容易修复的，但如果你不，它们可能会让你感到非常沮丧。

其次，事实证明你并不需要了解更多高级技术来学习简单的调试。一旦你学会了如何追踪简单的 bug，你就可以使用相同的技术来发现更高级的 bug。如果你学会了在 3 英尺深的水中游泳，以后你可以使用相同的技术在 10 英尺或 100 英尺深的水游泳。

以后，当你对 C# 编程有更多了解并能够创建更高级的 bug 时，同样的知识将帮助你修复这些 bug。当你对数组索引足够熟悉时，你也会知道如何修复它们。

# 过去与现在的调试 (DEBUGGING THEN AND NOW)

在过去，程序员通常通过盯着代码、进行一些更改然后重新运行程序来修复 bug。这种试错方法很慢，因为程序员不知道发生了什么。今天，Visual Studio 提供了优秀的工具。特别是，它可以让你在程序运行时停止并查看正在发生的情况。

## 设置断点 (SETTING BREAKPOINTS)

断点会在特定的语句停止执行。要设置断点，点击你想停止的行左侧的灰色区域。或者点击该行并按 F9。

IDE 通过显示红圈指示断点。图 12-1 显示在以下行有一个断点：

```csharp
decimal grandTotal = subtotal + salesTax;
```

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_227_0.png)

图 12-1

当你运行程序时，执行会在该处停止。调试器提供了编辑并继续的功能。要移除断点，点击红圈。

## 随机停止 (SPONTANEOUS STOP)

如果你需要在程序运行时停止但没有设置断点，可以选择调试菜单中的“全部停止”命令或按 Ctrl+Alt+Break。调试器将在程序执行中间时停止它。如果调试菜单中没有 Break 命令（某些版本可能），你仍然可以使用快捷键 Ctrl+Alt+Break。

## 读取变量 (READING VARIABLES)

当执行停止时，读取变量的值非常简单。只需将鼠标悬停在变量上，其值就会出现在弹出窗口中。

例如，考虑图 12-2 所示的订单摘要。程序应该将小计、9% 的销售税和运费相以得到总额。你必须足够敏锐才能发现图 12-2 中的问题。如果你为 19.95 元支付了 204.50 元，你需要找到一个新的停止位置。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_228_0.png)

图 12-2

现在你已经知道 bug 隐藏在变量 `salesTax` 中，你可以将鼠标悬停在其他变量上查看该值是如何计算的。如果你将鼠标悬停在上行代码的变量上，你会发现 `subTotal` 为 19.95（仍然正确），而 `taxRate` 为 9。

你可能需要思考一下才能意识到问题出在哪里。应用像 9% 这样的税率时，应该将其除以 100 然后相乘。在这种情况下，`taxRate` 应该是 0.09，而不是 9。

找到问题后，可以通过打开调试（Debug）菜单并选择“停止调试”（Stop Debugging）命令、点击工具栏上的“停止调试”按钮，或按下 Shift+F5 来停止程序。

现在你可以修复代码并再次运行程序，看看它是否可以工作。接下来的行显示了错误的代码行（我在图 12-3 中将其移出了视图范围，以防完全泄露答案）：
