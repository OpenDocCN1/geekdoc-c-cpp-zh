
# 练习 2：使用静态成员共享数据

## 任务 1：打开 StressTesting 解决方案

- 在 `E:\Labfiles\Lab 7\Ex2\Starter` 文件夹中打开 StressTesting 解决方案。该解决方案包含 `StressTestCase` 类的副本，其公共属性已改为私有：
  - 在 Visual Studio 中，在“文件”菜单上，指向“打开”，然后点击“项目/解决方案”。
  - 在“打开项目”对话框中，移动到 `E:\Labfiles\Lab 7\Ex2\Starter` 文件夹，点击 `StressTesting.sln`，然后点击“打开”。

## 任务 2：创建一个结构体来存储成功和失败的数量

- 查看任务列表：
  - 如果任务列表不可见，在“视图”菜单上，点击“任务列表”。
  - 如果任务列表显示的是“用户任务”，在下拉列表框中点击“注释”。

## 任务 3：修改 StressTestCase 以包含一个 TestStatistics 对象

1. 在任务列表中，找到 `TODO - Add a TestStatistics field and method to StressTestCase class`，双击该任务。该任务位于 `StressTestCase` 类中。
2. 删除 `TODO - Add a TestStatistics field and method to StressTestCase class` 注释，然后声明一个新的名为 `statistics` 的私有静态 `TestStatistics` 成员。

你的代码应该类似于下面的代码示例：

```csharp
public class StressTest {
    ...
    private TestCaseResult? testResult;
    private static TestStatistics statistics;
    ...
}
```

3. 在成员声明下方，添加一个名为 `GetStatistics` 的公共静态方法。该方法不需要参数，但应该返回一个 `TestStatistics` 对象。在方法中添加代码返回 `statistics` 成员的值。

你的代码应该类似于下面的代码示例：

```csharp
public class StressTest {
    ...
    private static TestStatistics statistics;
    public static TestStatistics GetStatistics() {
        return statistics;
    }
    ...
}
```

4. 在 `GetStatistics` 方法下方，添加一个名为 `ResetStatistics` 的公共静态方法。该方法不需要参数且不返回值。在方法中添加代码调用 `statistics` 成员的 `ResetCounters` 方法。

你的代码应该类似于下面的代码示例：

```csharp
public class StressTest {
    ...
    public static TestStatistics GetStatistics() {
        return statistics;
    }
    public static void ResetStatistics() {
        statistics.ResetCounters();
    }
    ...
}
```

5. 在任务列表中，找到 `TODO - Update the PerformStressTest method to handle statistics` 任务，然后双击此任务。该方法位于 `StressTestCase` 类中。
6. 删除 `TODO - Update the PerformStressTest method to handle statistics` 注释，并在 `PerformStressTest` 方法中添加代码，在测试通过或失败时调用 `statistics` 成员的 `IncrementTests` 方法。如果测试通过，将值 `true` 作为 `IncrementTests` 方法的参数。如果测试失败，将值 `false` 作为 `IncrementTests` 方法的参数。

你的代码应该类似于下面的代码示例：

```csharp
public void PerformStressTest() {
    if (Utility.rand.Next(10) == 9) {
        ...
        tcr.reasonForFailure = failureReasons[Utility.rand.Next(5)];
        statistics.IncrementTests(false);
    } else {
        tcr.result = TestResult.Pass;
        statistics.IncrementTests(true);
        ...
    }
}
```

## 任务 4：在用户界面中显示统计数据

- 在任务列表中，找到 `TODO - Update the UI to display statistics` 任务，然后双击此任务。此任务位于 `MainWindow` 类中，位于 `doTests_Click` 方法的末尾。
- 在 `doTests_Click` 方法末尾，删除注释并添加代码执行以下任务：
  - 创建名为 `statistics` 的新 `Statistics` 对象。使用调用 `StressTestCase.GetStatistics` 方法返回的值初始化该对象。
  - 在 `statisticsLabel` 标签中，显示消息 "Number of tests: \<tests\>, Failures: \<failures\>"，其中 `tests` 是执行的测试次数，`failures` 是失败的测试次数。
    > **提示：** 设置 Label 控件的 `Content` 属性以在该控件中显示消息。
  - 调用 `statistics` 对象的 `IncrementTests` 方法，并传递 `true` 作为参数。
  - 调用 `StressTestCase` 对象的静态方法 `GetStatistics`，并将结果存储在 `statistics` 变量中。
  - 在 `statisticsLabel2` 标签中，显示消息 "Number of tests: \<tests\>, Failures: \<failures\>"，其中 `tests` 是执行的测试次数，`failures` 是失败的测试次数。

> 展示了按值传递或返回的原理。当代码第一次调用 `GetStatistics` 方法时，从 `StressTestCase` 对象返回一个值的副本。因此，当代码调用 `IncrementTests` 方法时，更新是在拷贝的值上进行的，而不是原始值。当第二次调用 `GetStatistics` 方法时，会获取原始值的另一个副本；因此，两个标签都将显示相同的值。

你的代码应该类似于下面的代码示例：

```csharp
private void doTests_Click(object sender, RoutedEventArgs e) {
    Statistics statistics = StressTestCase.GetStatistics();
    statisticsLabel1.Content = string.Format("Number of tests: {0}, Failures: {1}",
        statistics.GetNumberOfTestsPerformed(),
        statistics.GetNumberFailures());
    statistics.IncrementTests(true);
    statistics = StressTestCase.GetStatistics();
    statisticsLabel2.Content = string.Format("Number of tests: {0}, Failures: {1}",
        statistics.GetNumberOfTestsPerformed(),
        statistics.GetNumberFailures());
}
```

## 任务 5：测试解决方案

1. 生成解决方案并修正任何错误：
   - 在“生成”菜单上，点击“生成解决方案”。修正任何错误。
2. 运行应用程序：
   - 在“调试”菜单上，点击“开始执行(不调试)”。
3. 在 `MainWindow` 窗口中，点击“Run Stress Tests”，然后检查统计标签，它们都显示相同的值。
4. 关闭 `MainWindow` 窗口，返回 Visual Studio。

## 任务 6：检查并运行 TestStatistics 类的单元测试

1. 在测试列表中，找到 `TODO - Examine and run unit tests` 任务，然后双击此任务。此任务位于 `StressTestClass_TestStatisticsTest` 文件。
2. 检查 `GetNumberOfFailTest` 方法。
   该方法创建一个名为 `target` 的新 `Statistics` 对象，然后两次调用 `IncrementTests`，并将 `false` 作为参数。然后该方法从 `TestStatistics` 对象获取失败次数，并使用 `Assert` 语句验证该值是否正确。
3. 检查 `GetNumberOfTestsPerformed` 方法。
   该方法创建一个名为 `target` 的新 `Statistics` 对象，然后调用三次 `IncrementTests`。然后该方法从 `TestStatistics` 对象获取执行的测试次数，并使用 `Assert` 语句验证该值是否正确。
4. 检查 `IncrementTestsTest` 方法。
   该方法创建一个名为 `target` 的新 `Statistics` 对象，然后在此对象上调用四次 `IncrementTests` 方法。该方法从 `target` 对象获取执行的测试次数，并使用 `Assert` 语句验证该值是否正确。
5. 运行解决方案中的所有测试，然后验证所有测试是否成功执行。
   - 在“测试”菜单上，悬停在“运行”，然后点击“解决方案中的所有测试”。
   - 等待测试运行，并在“测试结果”窗口中验证所有测试均已通过。

# 练习 3：实现扩展方法

## 任务 1：打开 StressTesting 解决方案

- 打开 `E:\Labfiles\Lab 7\Ex3\Starter` 文件夹下的 StressTesting 解决方案。该解决方案包含解决方案的副本：
  - 在 Visual Studio 中，在“文件”菜单上，指向“打开”。
  - 移动到 `E:\Labfiles\Lab 7\Ex3\Starter` 文件夹，点击 `StressTesting.sln`。

## 任务 2：定义扩展方法

- 在解决方案资源管理器中，右键点击 StressTest 项目，指向“添加”。
- 在“添加新项”对话框中，在“名称”框中输入 `Extensions` 并点击“添加”。
- 修改 `Extensions` 类。该类应该是 `public static`。
- 在 `Extensions` 类中添加一个名为 `ToBinaryString` 的静态方法。
  > **提示：** 要指示该方法是扩展方法，请在参数前加上 `this` 关键字。
  > **提示：** 可以使用 `long` 作为 `System.Int64` 的别名。

你的代码应该是：

```csharp
public static class Extensions {
    public static string ToBinaryString(this long i) {
        long remainder = 0;
        StringBuilder binary = new StringBuilder("");
        while (i > 0) {
            remainder = i % 2;
            i = i / 2;
            binary.Insert(0, remainder);
        }
        return binary.ToString();
    }
}
```

## 任务 3：修改 TestCaseResult 结构体包含 long 字段

- 检查任务列表：
  - 如果任务列表可见，在“视图”菜单上点击“任务列表”。
  - 如果任务列表显示“用户任务”，点击“注释”。
- 在任务列表中，找到 `TODO - Modify the TestCaseResult struct to include a long field` 任务，然后双击此任务。该任务位于 `TestCaseResult` 结构体中。
- 在 `TestCaseResult` 结构体中，删除注释并添加一个类型为 `long` 的 public 字段。

你的代码应该是：

```csharp
public struct TestCaseResult {
    public string reasonForFailure;
    public long failureData;
}
```

## 任务 4：修改 PerformStressTest 方法

1. 在任务列表中，找到 `TODO - Update the PerformStressTest method` 任务，然后双击此任务。该任务位于 `StressTestCase` 的 `PerformStressTest` 方法中。
2. 在 `PerformStressTest` 方法中，删除 `TODO - Update the PerformStressTest` 注释，并添加代码更新 `TestCaseResult` 对象的 `failureData` 成员，模拟从压力测试设备获取的数据。
   > **提示：** 使用 `Utility` 静态类的 `Rand` 成员生成随机数。该方法包含一个名为 `Next` 的方法，返回指定范围内的随机数。将值 `int.MaxValue` 作为 `Next` 方法的参数以生成 0 到该值之间的随机数。`int.MaxValue` 字段指定整数类型支持的最大值。

你的代码应该类似于下面的代码示例：

```csharp
public void PerformStressTest() {
    tcr.reasonForFailure = failureReasons[Utility.rand.Next(5)];
    tcr.failureData = Utility.Rand.Next(int.MaxValue);
    statistics.IncrementTests(false);
}
```

## 任务 5：显示失败数据

1. 在任务列表中，找到 `TODO - Update the UI to display the binary string` 任务，然后双击此任务。该任务位于 `MainWindow` 类的 `doTests_Click` 方法中。
2. 修改 `doTests_Click` 方法，将 `failureData` 成员中的二进制数据附加到用户界面中显示的失败信息之后；在添加到 `resultList.Items` 集合的字符串末尾附加一个空格字符，然后是调用 `ToBinaryString` 方法的结果。

你的代码应该类似于下面的代码示例：

```csharp
private void doTests_Click(object sender, RoutedEventArgs e) {
    ...
    if (stc.GetStressTestResult().HasValue) {
        tcr = (TestCaseResult)stc.GetStressTestResult().Value;
        // 在练习 3 中修改以使用扩展方法。
        resultList.Add(tcr.ToString() + " " + tcr.reasonForFailure + " " + tcr.failureData.ToBinaryString());
    }
}
```
