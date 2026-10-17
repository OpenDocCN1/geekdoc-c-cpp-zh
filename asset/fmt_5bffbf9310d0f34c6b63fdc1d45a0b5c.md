
## L3-2 声明和调用方法

2. 使用任务列表（Task List）窗口导航到 TODO Exercise 1, Task 2 任务。该任务位于 `GCDAlgorithms.cs` 文件中：

   - a. 如果任务列表可见，在“视图”（View）菜单上点击“任务列表”。
   - b. 如果任务列表显示用户任务（User Tasks），在下拉列表中点击“注释”（Comments）。
   - c. 在任务列表窗口，双击 TODO Exercise 1, Task 2。

3. 在 `GCDAlgorithms` 类中，删除 TODO Exercise 1, Task 2 注释，并声明一个公共静态方法 `FindGCDEuclid`。该方法应接受两个整数参数 `a` 和 `b`，并返回一个整数值。

你的代码应该类似于下面的代码示例。

```cs
static class GCDAlgorithms {
    public static int FindGCDEuclid(int a, int b) {
    }
}
```

4. 在 `FindGCDEuclid` 方法中，添加代码使用欧几里得算法（Euclid's algorithm）计算并返回参数 `a` 和 `b` 指定值的最大公约数（GCD）。

欧几里得算法的工作原理如下：

   - a. 如果 `a` 为零，则 `a` 和 `b` 的 GCD 为 `b`。
   - b. 否则，反复从 `a` 中减去 `b`（当 `a > b` 时）或从 `b` 中减去 `a`（当 `b > a` 时），直到 `b` 为零。
   - c. 两个原始参数的 GCD 就是 `a` 的新值。

你的代码应该类似于下面的代码示例。

```cs
static class GCDAlgorithms {
    public static int FindGCDEuclid(int a, int b) {
        if (a == 0) return b;
        while (b != 0) {
            if (a > b) {
                a = a - b;
            }
            else {
                b = b - a;
            }
        }
        return a;
    }
}
```

## 任务 3：测试 FindGCDEuclid 方法

1. 使用任务列表窗口导航到 TODO Exercise 1, Task 3 任务。该任务位于 `MainWindow.xaml.cs` 文件中。这是 Windows® Presentation Foundation (WPF) 窗口的后台代码文件，你将用它测试 `FindGCDEuclid` 方法并显示结果：

   - 在任务列表窗口，双击 TODO Exercise 1, Task 3。

2. 删除 TODO Exercise 1, Task 3，添加代码调用 `GCDAlgorithms` 类的静态方法 `FindGCDEuclid`，并在 `resultEuclid` 标签控件中显示结果。在方法调用中，使用 `FirstNumber` 和 `secondNumber` 变量作为参数（这些变量包含用户在 WPF 窗口中输入的值）。最后，结果应按照下面的代码示例所示进行格式化。

> 提示：设置标签控件的 `Content` 属性以在标签中显示数据。使用 `String.Format` 方法创建格式化字符串。

你的代码应该类似于下面的代码示例。

```cs
... if (sender == null) // 两个整数的欧几里得算法
{
    // 调用 FindGCD 方法并显示结果
    this.resultEuclid.Content = String.Format("Euclid: {0}", GCDAlgorithms.FindGCDEuclid(FirstNumber, secondNumber));
}
```

生成解决方案并修正任何错误：

   - 在“生成”（Build）菜单上，点击“生成解决方案”。修正任何错误。

运行 GreatestCommonDivisor 应用程序：

   - 在“调试”（Debug）菜单上，点击“开始调试”

在 GreatestCommonDivisor 应用程序中，在 MainWindow 窗口的第一个框中输入 2806

在第二个文本框中输入 345，然后点击“Find GCD (2 Integers)”。应显示结果 23，如截图所示。

![](img/3ef84844c6ac82b838cfffa6448b2346_525_0.png)

7. 使用该窗口计算下表中指定值的 GCD，并验证显示的结果与表中相符。

| 第一个数字 | 第二个数字 | 结果 |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 10 | 10 |
| 25 | 10 | 5 |
| 25 | 100 | 25 |
| 26 | 100 | 2 |
| 27 | 100 | 1 |

8. 关闭 GreatestCommonDivisor 应用程序：

   - 在“调试”菜单上，点击“停止调试”

## 任务 4：为 FindGCDEuclid 方法创建单元测试

1. 打开 `GCDAlgorithms.cs` 文件：

   - 在“解决方案管理器”（Solution Explorer）中，双击 `GCDAlgorithms.cs`。

2. 在 `GCDAlgorithms` 类中，为 `FindGCDEuclid` 方法创建一个单元测试。创建一个项目来存放测试：

   - a. 在 `GCDAlgorithms` 类中，右键点击 `FindGCDEuclid` 方法，然后点击“单元测试”（Unit Tests）。
   - b. 在“单元测试”对话框中，确保选择了 `FindGCDEuclid(Int32, Int32)`，确保项目设置为创建新的 C# 测试项目，并点击“确定”。
   - c. 在“新建项目”对话框中，为你的新项目输入名称，输入 `GCD Test` 然后点击“创建”。
   - d. 如果显示“你已对测试进行了更改”对话框，点击“确定”。
   - e. 在 `InternalsVisibleTo` 对话框中，点击“是”。

3. 在 `GCD Test` 项目的 `GCDAlgorithmsTest.cs` 文件中，找到 `FindGCDEuclidTest` 方法：

4. 在 `FindGCDEuclidTest` 方法中，将变量 `a` 设置为 2806，将变量 `b` 设置为 345，将预期值变量 `expected` 设置为 23，然后添加 `Assert.AreEqual` 调用。你的代码应该类似于示例。

```cs
[TestMethod]
public void FindGCDEuclidTest()
{
    int a = 2806; // TODO: 初始化为适当的值
    int b = 345; // TODO: 初始化为适当的值
    int expected = 23; // TODO: 初始化为适当的值
    int actual;
    actual = GCDAlgorithms.FindGCDEuclid(a, b);
    Assert.AreEqual(expected, actual);
}
```

5. 打开测试窗口并验证测试结果：

   - a. 在测试中，点击“运行”。
   - b. 如果显示“你已对测试进行了更改”对话框，点击“确定”。
   - c. 在测试窗口中，点击“全部测试”。

6. 验证 `FindGCDEuclidTest` 是否成功运行：

   - a. 在测试结果中，找到 `FindGCDEuclidTest`。
   - b. 确保它已通过。

```cs
...
public static int FindGCDEuclid(int a, int b, int c, int d)
{
    int e = FindGCDEuclid(a, b, c);
    int f = FindGCDEuclid(e, d);
    return f;
}
...
```

8. 声明另一个 `FindGCDEuclid` 方法的重载版本。该方法应该接受五个名为 `a`、`b`、`c`、`d` 和 `e` 的整数参数，并返回一个整数值。使用其他的 `FindGCDEuclid` 重载方法来查找这些参数的最大公约数（GCD）并返回结果。

你的代码应该类似于下面的代码示例。

```cs
...
public static int FindGCDEuclid(int a, int b, int c, int d, int e)
{
    int f = FindGCDEuclid(a, b, c);
    int g = FindGCDEuclid(f, e);
    return g;
}
...
```

完成此任务后，`GCDAlgorithms` 类应该类似于下面的代码示例。

```cs
static class GCDAlgorithms
{
    // TODO Exercise 2, Task 2
    // 添加针对 3、4 和5 个整数的重载方法
    public static int FindGCDEuclid(int a, int b, int c)
    {
        int d = FindGCDEuclid(a, b);
        int e = FindGCDEuclid(d, c);
        return e;
    }
    public static int FindGCDEuclid(int a, int b, int c, int d)
    {
        int e = FindGCDEuclid(a, b, c);
        int f = FindGCDEuclid(e, d);
        return f;
    }
    public static int FindGCDEuclid(int a, int b, int c, int d, int e)
    {
        int f = FindGCDEuclid(a, b, c);
        int g = FindGCDEuclid(f, e);
        return g;
    }
}
```

# L3-10 声明和调用方法

```cs
int f = FindGCDEuclid(a, b, c, d);
int g = FindGCDEuclid(f, e);
return g;
}
...
```

# 任务 3：测试重载方法

- 使用“任务列表”（Task List）窗口导航到 `TODO Exercise 2, Task 3` 任务。此任务位于用于测试你代码的 WPF 窗口代码中：

  - 在任务列表窗口中，双击 `TODO Exercise 2, Task 3`。

- 删除 `TODO Exercise 2, Task 3` 注释，找到 `else if (sender == findGCD3)` 块，并修改将 `resultEuclid` 标签的 `Content` 属性设置为 "N/A" 的语句：

  - 调用接受三个参数的 `FindGCDEuclid` 重载，并将 `firstNumber`、`secondNumber` 和 `thirdNumber` 变量作为参数。
  - 在 `resultEuclid` 标签控件中显示结果。结果格式如下代码所示。

  Euclid: result

你的代码应该类似于下面的代码示例。

```cs
else if (sender == findGCD3) // 针对三个整数的欧几里德算法
{
    this.resultEuclid.Content =
        String.Format("Euclid: {0}",
            GCDAlgorithms.FindGCDEuclid(
                firstNumber,
                secondNumber,
                thirdNumber));
    this.resultStein.Content = "N/A";
}
```

- 找到 `else if (sender == findGCD3)` 块、`else if (sender == findGCD4)` 块和 `else if (sender == findGCD5)` 块，并修改将 `resultEuclid` 标签的 `Content` 属性设置为 "N/A" 的语句：
