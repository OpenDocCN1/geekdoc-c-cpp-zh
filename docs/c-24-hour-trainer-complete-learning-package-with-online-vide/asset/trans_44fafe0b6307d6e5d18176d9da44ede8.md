
下面的代码展示了如何调用 Gcd 方法：

```
// Get the input values.
long a = long.Parse(aTextBox.Text);
long b = long.Parse(bTextBox.Text);

// Calculate the GCD.
long result = Gcd(a, b);

// Display the result.
resultTextBox.Text = result.ToString();
```

这段代码初始化两个整数，将它们传递给 Gcd 方法，并保存结果。然后显示这两个整数及其 GCD。

## 使用 ref 参数

参数列表还有一个特性，容易让人困惑，值得单独用一节来讲。参数可以按值或按引用传递给方法。

当按值传递参数时，C# 会复制该值并将副本传递给方法。然后方法可以随意修改其副本，而不会破坏调用代码使用的值。

相反，当按引用传递值时，C# 会将值的内存位置传入方法。如果方法修改了参数，调用代码中的值也会随之改变。

通常值是按值传递的。这样做不容易混淆，因为方法内部隐藏的更改不会破坏调用代码。

不过，有时你可能希望按引用传递参数。为此，请在参数声明前添加关键字 ref。

为了告诉 C# 你明白某个参数是按引用传递的，并且这不只是一个严重错误，你还必须在传入方法的值前添加关键字 ref。

例如，假设你想编写一个名为 GetMatchup 的方法，用于选择两名棋手进行对弈。如果该方法能找到匹配，则应返回 true；如果不可能再有匹配（因为所有对局都已进行过），则返回 false。该方法只能返回一个值（true 或 false），因此必须找到其他方式来返回两名匹配的棋手。

下面的代码展示了该方法可能的结构：

```
private bool GetMatchup(ref string player1, ref string player2)
{
    // Do complicated stuff to pick an even match.
    ...
    // Somewhere in here the code should set player1 and player2.
    ...

    // We found a match.
    return true;
}
```

该方法接受两个参数 player1 和 player2，它们是通过引用传递的字符串。该方法执行一些此处未展示的复杂计算，为变量 player1 和 player2 赋值。然后返回 true 表示找到匹配。

下面的代码展示了程序可能如何调用此方法：

```
string playerA = null, playerB = null;
if (GetMatchup(ref playerA, ref playerB))
{
    MessageBox.Show(playerA + " versus " + playerB);
}
else
{
    MessageBox.Show("No match is possible");
}
```

这段代码声明变量 playerA 和 playerB，用于保存所选棋手的姓名。它调用该方法，并在两个棋手姓名变量前加上 ref 关键字后传递。根据方法返回 true 还是 false，程序会宣布匹配结果或表示不可能匹配。

## 使用 out 参数

out 关键字的工作方式与 ref 关键字类似，只是它不要求输入变量必须初始化。例如，在前面的示例中，如果你没有将 playerA 和 playerB 初始化为某个值，Visual Studio 会警告你这些变量未初始化，并且不会允许你运行程序。其理念是，方法可能需要使用这些变量的输入值来完成工作。

相反，如果使用 out 关键字而不是 ref，则这些值被视为方法的仅输出参数，你不需要初始化它们。

如果对参数使用 out 关键字，请确保方法不要尝试使用传入该参数的值，因为它可能未初始化。事实上，如果方法确实尝试使用参数的传入值，Visual Studio 会警告你它可能未初始化。

> 注意 一般来说，避免通过按引用传递的参数返回结果被认为是良好的实践，因为这可能会造成混淆。如果可能，最好使用输出参数。
>
> 更好的方法是通过参数传入方法输入，并让方法使用 return 语句返回其所有返回值。例如，国际象棋匹配示例可以返回一个结构或类实例，其中包含两名棋手的姓名。

这意味着 minimum、maximum 和 average 参数应使用 out 关键字，而不是 ref 关键字。

- 2. 将 minimum 和 maximum 变量初始化为数组中的第一个元素。
- 3. 将 total 变量初始化为数组中的第一个元素。
- 4. 循环遍历数组的其余部分（跳过第一个元素，因为它已经被考虑过），根据需要更新 minimum 和 maximum 变量，并将数组中的值累加到 total 中。
- 5. 完成循环后，将 total 除以值的数量以得到平均值。

下面的代码展示了如何构建此方法：

```csharp
// Calculate the minimum, maximum, and average values for the array.
private void FindMinimumMaximumAverage(double[] values,
    out double minimum, out double maximum, out double average)
{
    // Initialize the minimum, maximum, and total values.
    minimum = values[0];
    maximum = values[0];
    double total = values[0];

    // Loop through the rest of the array.
    for (int i = 1; i < values.Length; i++)
    {
        if (values[i] < minimum) minimum = values[i];
        if (values[i] > maximum) maximum = values[i];
        total += values[i];
    }

    // Calculate the average.
    average = total / values.Length;
}
```

编写代码测试该方法。

- 1. 当用户单击按钮时，获取 TextBox 的文本，并使用其 Split 方法将用户的值拆分为字符串数组。
- 2. 创建一个 double 数组，并使用 for 循环将文本值解析到其中。
- 3. 调用该方法计算所需结果。
- 4. 显示结果。

下面的代码展示了如何构建按钮的事件处理程序：

```csharp
// Find and display the minimum, maximum, and average of the values.
private void calculateButton_Click(object sender, EventArgs e)
{
    // Get the values.
    string[] textValues = valuesTextBox.Text.Split();
    double[] values = new double[textValues.Length];
    for (int i = 0; i < textValues.Length; i++)
    {
        values[i] = double.Parse(textValues[i]);
    }

    // Calculate.
    double smallest, largest, average;
    FindMinimumMaximumAverage(values,
        out smallest, out largest, out average);

    // Display the results.
    minimumTextBox.Text = smallest.ToString();
    maximumTextBox.Text = largest.ToString();
    averageTextBox.Text = average.ToString("0.00");
}
```

> 注意 本课提到，通过按引用传递的参数返回值并不是一种好做法。那么，如何修改此示例以避免这样做呢？
>
> 你可以将 FindMinimumMaximumAverage 方法拆分为三个独立的方法：FindMinimum、FindMaximum 和 FindAverage。然后每个方法都可以通过 return 语句返回其结果。除了避免按引用传递参数外，这还使每个例程执行一个专注的单一任务，从而更易于理解和使用。它也使这些方法更容易单独使用，以防你只想查找数组的最小值，而不需要最大值或平均值。
>
> （另请注意，数组提供了可为你查找这些值的方法，因此你其实根本不需要编写这些函数。它们在这里纯粹是为了演示按引用传递的参数。）

## 练习

- 1. 编写一个计算两个整数的最小公倍数（LCM）的程序。（两个整数的最小公倍数是这两个数都能整除的最小整数。）提示：LCM(a, b) = a * b / GCD(a, b)。另外，不要从头编写 LCM 方法。相反，让它调用本课前面描述的 GCD 方法。
- 2. 递归方法是一种调用自身的方法。使用以下定义编写递归阶乘方法：
   - 0! = 1
   - N! = N * (N-1)!
   - 提示：务必检查停止条件 N = 0，这样方法就不会永远调用自身。（另请注意，递归方法可能非常难以理解和调试，因此通常如果可能的话，最好编写不使用递归的方法。有些问题具有自然的递归定义，但通常非递归方法更好。）
