
你的代码应该类似于下面的代码示例。

```cs
// Step 4 - 在关闭反应堆前记录堆芯
// 温度

try {
    this.textBlock1.Text +=
        "\nStep 4: 关前的堆芯温度: " +
        sd.GetCoreTemperature();
}
catch (SwitchDevices.CoreTemperatureReadException ex) {
    this.textBlock1.Text +=
        "\n*** Step 4 异常: " + ex.Message;
}
```

## Step 5 - 将控制棒插入反应堆

将“Step 5 - 将控制棒插入反应堆”注释与“Step 6 - 在关闭反应堆后记录堆芯温度”注释之间的代码封装在一个 try/catch 块中，该块用于捕获 `SwitchDevices.RodClusterReleaseException` 异常。在异常处理程序中，在 textBlock 控件中换行打印一条消息（这是第 5 步）。
你的代码应该类似于下面的代码示例。

```cs
try {
    if (sd.InsertRodCluster() ==
        SwitchDevices.SuccessFailureResult.Success) {
        this.textBlock1.Text +=
            "\nStep 5: 控制棒插入成功";
    } else {
        this.textBlock1.Text +=
            "\nStep 5: 控制棒插入失败";
    }
}
catch (SwitchDevices.RodClusterReleaseException ex) {
    this.textBlock1.Text
    += "\n*** Step 5 异常: " + ex.Message;
}

// Step 6 - 在关闭反应堆后记录堆芯温度
```

- 9. 将“Step 6 - 在关闭反应堆后记录堆芯温度”注释与“Step 7 - 在关闭反应堆后记录堆芯辐射水平”注释之间的代码封装在一个 try/catch 块中，该块用于捕获 `SwitchDevices.CoreTemperatureReadException`。在异常处理程序中，在 textBlock1 控件中换行打印一条消息（这是第 6 步）。

你的代码应该类似于下面的代码示例。

```cs
// Step 6 - 在关闭反应堆后记录堆芯温度
try {
    this.textBlock1.Text +=
    "\nStep 6: 关后的堆芯温度: " +
    sd.GetCoreTemperature();
} catch (SwitchDevices.CoreTemperatureReadException ex)
{
    this.textBlock1.Text +=
    "\n*** Step 6 异常: " + ex.Message;
}
```

## Step 7 - 在关闭反应堆后记录堆芯辐射水平

- 10. 将“Step 7 - 在关闭反应堆后记录堆芯辐射水平”注释与“Step 8 - 广播‘关机完成’消息”注释之间的代码封装在一个 try/catch 块中，该块用于捕获 `SwitchDevices.CoreRadiationLevelReadException`。在异常处理程序中，在 textBlock1 控件中换行打印一条消息（这是第 7 步）。

你的代码应该类似于下面的代码示例。

```cs
// Step 7 - 在关闭反应堆后记录堆芯辐射水平
try {
    this.textBlock1.Text += 
        "\nStep 7: 关后的堆芯辐射水平: " +
        sd.GetRadiationLevel();
} catch (SwitchDevices.CoreRadiationLevelReadException ex) {
    this.textBlock1.Text += 
        "\n*** Step 7 异常: " + ex.Message;
}

// Step 8 - 广播“关机完成”消息
```

- 11. 将“Step 8 - 广播‘关机完成’消息”注释后的两个语句封装在一个 try/catch 块中，该块用于捕获 `SwitchDevices.SignallingException`。在每个异常处理程序中，在 textBlock1 控件中换行打印一条消息（这是第 8 步）。

你的代码应该类似于示例。

```cs
// Step 8 - 广播“关机完成”消息
try {
    sd.SignalComplete();
    this.textBlock1.Text +=
        "\nStep 8: 广播完成";
} catch (SwitchDevices.SignallingException) {
    this.textBlock1.Text +=
        "\n*** Step 8 异常: 信号错误";
}
```

```cs
this.textBlock1.Text +=
    "\nStep 8: 关机完成: " +
    DateTime.Now();
```

- 12. 生成解决方案并修复错误：

# 任务 4: 测试应用程序

- 目前应用程序随机生成异常，因此你第一次点击时可能看不到任何异常。
- a. 在调试菜单上开始调试。
- b. 在窗口中点击关机。
- c. 阅读消息，确认发生了异常。
- d. 关闭应用程序返回 Visual Studio。

## 练习 2: 检测异常情况

### 任务 1: 打开 Matrixplication 解决方案

- 1. 在 Visual Studio 中，点击文件菜单，选择打开项目/解决方案。
- a. 在打开项目对话框中，移动到 `\files\Lab4\Ex2\`，点击 `MatrixMultiplication.sln` 并打开。
- 2. 在资源管理器中打开 Matrixcs 文件：
- a. 在解决方案管理器中，在 MatrixMultiplication 项目中右键点击 `Matrix.cs`，然后查看代码。
- b. 检查 Multiply 方法。Multiply 方法对传入的矩阵进行乘法并返回结果。

## L4-10 处理异常

目前，方法接受任何大小的矩阵，并在计算结果之前不进行任何验证。你将添加检查以确保两个矩阵兼容（第一个矩阵的列数等于第二个矩阵的行数），并且任何矩阵中都没有负数。

如果矩阵不兼容，或者其中一个包含负值，方法必须抛出异常。

### 任务 2: 在 Multiply 方法中添加抛出异常

- 1. 在 Multiply 方法中，定位并删除注释 TODO Evaluate input matrices for compatibility。注释块下方，添加代码执行以下操作：
- a. 比较 matrix1 的列数与 matrix2 的行数。
- b. 如果值不等，则抛出 ArgumentException。异常消息应指定列数和行数应该匹配。

> 提示：你可以通过检查第一个维度的长度获取矩阵的列数。你可以通过检查第二个维度的长度获取矩阵的行数。

你的代码应该类似于下面的代码示例。

```cs
// 检查矩阵兼容性
if (matrix1.GetLength(0) != matrix2.GetLength(1)) {
    throw new ArgumentException(
        "第一个矩阵的列数必须与第二个矩阵的行数相同");
}
// 获取维度
```

- 2. 定位并删除注释 TODO Evaluate matrix data points for invalid data。此时，方法遍历每个矩阵中的数据点，将 matrix1 中每个单元格的值与 matrix2 中对应单元格的值相乘。在注释块下方添加代码执行以下操作：

a. 检查 matrix1 中当前列和行的值是否大于 0。`cell` 和 `row` 变量包含你应该检查的列索引和行索引。

b. 如果值不大于0，则抛出一个 `ArgumentException`。该异常应包含消息 "Matrix1 contains an invalid entry in cell[x,y]"，其中 x 和 y 是该单元格的列和行值。

**提示：** 使用 `String.Format` 方法来构造异常消息。

你的代码应类似于下面的代码示例。

```csharp
// 如果任一矩阵包含负值，则抛出异常
if (matrix1[cell, row] < 0)
    throw new ArgumentException(String.Format(
        "Matrix1 contains an invalid entry in cell[{0}, {1}]",
        cell, row));
accumulator += matrix1[cell, row] * matrix2[column, cell];
```

3. 添加另一块代码来检查 matrix2 中当前列和行的值是否大于 0。如果不是，则抛出一个 `ArgumentException` 异常，消息为 "Matrix2 contains an invalid entry in cell[x,y]."。`column` 和 `cell` 变量包含你应该检查的列和行索引。

你的代码应类似于下面的代码示例。

```csharp
...
"Matrix1 contains an invalid entry"
if (matrix2[column, cell] < 0)
    throw new ArgumentException(String.Format(
        "Matrix2 contains an invalid entry in cell[{0}, {1}]",
        column, cell));
accumulator += matrix1[cell, row] * matrix2[column, cell];
...
```

# 任务 3：处理 MatrixMultiply 方法抛出的异常

- 1. 在设计视图中打开 MainWindow Windows Presentation Foundation (WPF) 窗口并检查窗口。

此窗口提供了用户界面，允许用户输入两个待相乘矩阵的en。用户点击 Calculate（计算）按钮来计算并显示结果：

- 在解决方案资源管理器中，在 MatrixMultiplication 项目中，双击 `MainWindow.xaml`。

- 2. 打开 MainWindow WPF 窗口的代码。

- 在解决方案资源管理器中，在 MatrixMultiplication 项目中展开 `MainWindow.xaml`，右键点击 `MatrixMultiply.cs`，然后点击 View Code（查看代码）。

- 3. 在 MainWindow 类中，找到 `ButtonCalculate_Click` 方法。该方法在用户点击 Calculate 按钮时运行。

- 4. 在 `ButtonCalculate_Click` 方法中，找到调用 `Matrix.MatrixMultiply` 方法的代码行，并将该行封装在 `try/catch` 块中，捕获名为 `ex` 的 `ArgumentException`。

你的代码应类似于下面的代码示例：

```csharp
// 执行乘法 - 检查异常
try {
    result = Matrix.MatrixMultiply(matrix1, matrix2);
} catch (ArgumentException ex) {
}
// 显示结果
...
```

- 5. 在 catch 块中，添加一条语句显示消息框，其中包含异常对象的 `Message` 属性的内容。

> 提示：你可以使用 `MessageBox.Show` 方法来显示消息框。将要显示的消息作为字符串作为参数传递给此方法。

你的代码应类似于下面的代码示例。

```csharp
...
catch (ArgumentException ex)
{
    MessageBox.Show(ex.Message);
}
...
```

- 生成解决方案并纠正任何错误：
- 在 Build 菜单上，点击 Build Solution（生成解决方案）

- 不带调试启动应用程序：
- 在 Debug 菜单上，点击 Start Without Debugging（不带调试启动）

- 在 MainWindow 窗口中，在第一个下拉框中选择 Matrix 1: 2 Columns，在第二个下拉框中选择 Matrix 1: 2 Rows，在第三个下拉框中选择 Matrix 2: 2 Columns。
这将创建一个对初始化为零的 2 × 2 矩阵。

- 在两个矩阵的单元格中输入一些非负值，然后点击 Calculate。

验证结果是否已计算并显示，以及没有发生异常。

- 在任一矩阵的单元格中输入一个或多个负值，然后再次点击 Calculate。

验证是否显示了相应的异常消息，并且它是否识别了错误的矩阵和单元格。

- 关闭 MainWindow 窗口并返回 Visual Studio。

应用程序会抛出并捕获异常，因此你需要测试应用程序运行是否符合预期。虽然你可以通过应用程序界面测试负数数据点，但用户界面不允许创建不同维度的数组。因此，我们为你提供了单元测试，这些测试将调用 `MatrixMultiply` 方法并使用会导致异常的数据。这些测试已经创建；你只需运行它们来验证你的代码工作正常。

# 任务 4：实现测试用例并测试应用程序

- 1. 在 Matrix Unit Test 项目中，打开 `MatrixTest` 类，然后检查 `MatrixMultiplyTest1` 方法。

`MatrixMultiplyTest1` 方法创建了四个矩阵：`matrix1`、`matrix2`、`expected` 和 `actual`。`matrix1` 和 `matrix2` 矩阵是测试期间传递给 `MatrixMultiply` 方法的输入矩阵。`expected` 矩阵包含矩阵乘法的预期结果，而 `actual` 矩阵存储 `MatrixMultiply` 方法调用的结果。该方法在使用一系列 Assert 语句验证预期和实际矩阵相同之前调用了 `MatrixMultiply` 方法。

此测试已完成，不需要进一步工作：

- 在解决方案资源管理器中，展开 Solution Items 文件夹，展开 Unit Test Project，展开 Test References，然后双击 `MatrixTest.cs`。

- 2. 检查 `MatrixMultiplyTest2` 方法。
此方法创建了两个兼容的矩阵，但 `matrix2` 包含一个负值。这应该导致 `MatrixMultiply` 方法抛出异常。

`MatrixMultiplyTest2` 方法带有 `ExpectedException` 特性，如果没有抛出异常测试将会失败。

- 3. 检查 `MatrixMultiplyTest3` 方法。
此方法创建了两个不兼容的矩阵并将它们传递给 `MatrixMultiply` 方法，这应该抛出 `ArgumentException`。再次，该方法带有 `ExpectedException` 特性，如果没有抛出此异常测试将会失败。

- 4. 运行解决方案的所有测试，验证所有测试执行正确：

- 在 Build 菜单上，点击 Build Solution。
- 在 Test 菜单上，指向 Run，然后点击 All Tests（所有测试）。
- 等待测试运行，然后在 Test Results 窗口中验证所有测试已通过。

# 练习 3：检查数值溢出

## 任务 1：打开 IntegerOverflow 解决方案

- 在 E:\Labfiles\Lab4\Ex3\Starter 文件夹打开 IntegerOverflow 解决方案：
    在 Visual Studio 中，在 File 菜单上，指向 Open，然后点击 Project/Solution。
    在 Open 对话框中，转到 E:\Labfiles\Lab4\Ex3\Starter 文件夹，点击 `IntegerOverflow.sln`，然后 Open。

- 运行应用程序，然后点击 Multiply。观察显示的结果并注意它是错误的。

应用程序将 2147483647 乘以 2，并显示结果 -2，因为乘法导致了整数溢出。默认情况下，此类溢出错误不会导致异常。然而在许多情况下，捕获溢出错误比让应用程序使用错误数据继续运行更好：

- 在 Debug 菜单上，点击 Start Debugging
    在 MainWindow 窗口中，点击 Multiply。

- 在 Visual Studio 中，在 Debug 菜单上，点击 Stop Debugging。

## 任务 2：添加检查块

- 在解决方案资源管理器中，打开 `MainWindow.xaml.cs` 文件：
    在解决方案资源管理器中，在 IntegerMultiply 解决方案中，展开 `MainWindow.xaml`，右键点击 `MainWindow.xaml.cs`，然后点击 Code。

- 找到 `DoMultiply_Click` 方法。
    该方法在用户点击 Multiply 按钮时运行。

- 删除 TODO - 将乘放在检查块中。
    在执行乘法操作的代码行周围添加 `try/catch` 块，捕获 `OverflowException` 异常。
    你的代码应类似于下面的代码示例。

```cs
...
return;
}
try {
  labelAnswer.Content = (x * y).ToString();
} catch (OverflowException ex) {
```
