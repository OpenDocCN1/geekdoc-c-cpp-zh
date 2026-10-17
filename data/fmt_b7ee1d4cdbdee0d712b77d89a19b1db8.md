
你的代码应该类似于下面的代码示例。

```java
public void PerformStressTest()
{
    if (Utility.rand.Next(10) == 9) {
        currentTestCase.Result = TestResult.Fail;
        currentTestCase.ReasonForFailure = failureReasons[Utility.rand.Next(5)];
        TestCaseResult = currentTestCase;
    }
}
```

### 任务 3：修改 `else` 块

修改 `else` 块以执行以下任务：
a. 修改 `currentTestCase` 对象，而不是 `TestCaseResult` 成员。
b. 在 `if` 块的末尾，将 `currentTestCase` 对象存储在 `TestCaseResult` 成员中。

你的代码应该类似于下面的代码示例。

```java
public void PerformStressTest()
{
    else {
        currentTestCase.Result = TestResult.Pass;
        TestCaseResult = currentTestCase;
    }
}
```

## 任务 5：修改 GetStressTestResult 方法

在 `GetStressTestResult` 方法中，修改方法定义以返回一个可空的 `TestCase` 值。

你的代码应该类似于下面的代码示例。

```csharp
public TestCase? GetStressTestResult()
{
    ...
}
...
```

## 任务 6：修改 GetStressTestResult 方法调用

在任务列表中，找到处理空值的任务 `TODO - Modify call to GetStressTestResult method`，然后双击此任务。

删除注释，然后修改代码以创建一个名为 `currentTestResult` 的可空 `TestCaseObject`。

你的代码应该类似于下面的代码示例。

```csharp
StressTestCase currentTestResult;
TestCase? currentTestResult;
for (int i = 0; i < stressTestCases.Length; i++)
...
```

在 `for` 块中，从 `currentTestResult.GetStressTestResult` 方法获取 `currentTestResult` 对象的值后，添加代码来检查 `currentTestResult` 对象是否包含值。如果存在值，则向 `resultList` 框添加一个包含 `StressTestResult` 的 `Result` 和 `ReasonForFailure` 属性的字符串。

你的代码应该类似于下面的代码示例。

```csharp
for (int i = 0; i < stressTestCases.Length; i++)
{
    currentStressTest = stressTestCases[i];
    currentStressTest.PerformStressTest();
    testList.Items.Add(currentStressTest.ToString());
    currentTestResult = currentStressTest.GetStressTestResult();
}
if (currentTestResult.HasValue)
{
```

```csharp
resultList.Items.Add(
    currentTestResult.Value.Result.ToString() + " " + 
    currentTestResult.Value.ReasonForFailure);
```

## 任务 7：测试解决方案

1. 生成解决方案并修正错误：
   - 在“生成”（Build）菜单中，点击“生成解决方案”（Build Solution）。修正任何错误。
2. 运行应用程序：
   - 在“调试”（Debug）菜单中，点击“转到调试”（Start Without Debugging）。
3. 在“主窗口”（MainWindow）窗口中，点击“运行压力测试”（Run Stress Tests）。
   验证应用程序的功能与之前相同。
4. 关闭应用程序并返回 Visual Studio。

## 任务 8：更新单元测试

1. 在任务列表中，找到处理可空类型更新的任务 `TODO - Examine and run unit tests updated to deal with nullable type`，然后双击此任务。此任务位于 `StressTestCase` 类中。

> 注意：大多数案例与练习 3 中的案例相同。仅在 `GetStressTestResult` 和 `PerformStressTest` 方法中发生了变化。

2. 检查 `GetStressTestResult` 方法。
   此方法创建一个新的 `StressTestCase` 对象。然后它评估结果上的 `HasValue` 属性。在 `GetStressTestResult` 调用后评估 `HasValue` 属性以验证是否存在值。

3. 检查 `PerformStressTest` 方法的更改。
   此方法创建一个 `StressTestCase` 对象，然后在该对象上调用 `PerformStressTest` 方法。在 `StressTestCase` 对象上生成一个 `TestCaseResult` 值。测试再次评估 `HasValue` 属性以验证是否存在。

4. 运行解决方案中的所有测试：
   a. 在“生成”（Build）菜单中，点击“生成解决方案”。
   b. 在“测试”（Test）菜单中指向“运行”（Run），然后点击“解决方案中的测试”。
   c. 等待测试运行，在测试窗口中验证所有测试已通过。

5. 关闭 Visual Studio：
   - 在“文件”（File）菜单中，点击“退出”（Exit）。

## 数据与方法

## 实验 7：数据与方法

## 练习 1：隐藏成员

### 任务 1：打开 StressTesting 解决方案

1. 以学生身份登录虚拟机。
2. 打开 Visual Studio 2010：
   - 点击“开始”（Start），指向“所有程序”（All Programs），点击 Visual Studio 2010。
3. 在 `E:\Labfiles\7\Ex1\` 文件夹中打开 `StressTesting.sln` 并点击“打开”。
   a. 在 Visual Studio 中，在“文件”（File）菜单中指向“打开”（Open），并点击“项目/解决方案”（Project/Solution）。
   b. 在“打开项目”对话框中，移动到 `E:\Labfiles\7\Ex1\` 文件夹，点击 `StressTesting.sln`。

### 任务 2：将 StressTestCase 类中的字段声明为私有

1. 查看任务列表：
   a. 如果任务列表可见，在“视图”（View）菜单中点击“任务列表”（Task List）。
   b. 如果任务列表显示的是“任务”（Tasks），点击“注释”（Comments）。
2. 在任务列表中，找到 `TODO - Modify StressTestCase class to make members private`，双击此任务。此任务位于 `StressTestCase` 类中。
3. 在 `StressTestCase` 类中删除 `TODO - Modify StressTestCase class to make members private`，然后修改每个字段将所有字段声明为私有。

你的代码应该类似于下面的代码示例。

```csharp
/// <summary>
/// 梁材料类型（枚举类型）
/// </summary>
private Material girderMaterial;
```

```csharp
/// <summary>
/// 梁截面（枚举类型）
/// </summary>
private CrossSection crossSection;
```

```csharp
/// <summary>
/// 梁长度（毫米）
/// </summary>
private int lengthInMm;
```

```csharp
/// <summary>
/// 测试结果详情（结构体类型）
/// 已设为空
/// </summary>
private TestCaseResult? testCaseResult;
```

...

### 任务 3：生成项目并修正错误

1. 生成项目，然后查看错误列表。
   项目应该将无法生成，因为测试框架项目中 `doTests_Click` 方法中的代码尝试访问 `StressTest` 类中已变为私有的字段：
   a. 在“生成”（Build）菜单中，点击“生成解决方案”。
   b. 如果错误列表没有自动显示，在“视图”（View）菜单中点击“错误列表”（Error List）。
   c. 如果错误列表没有显示错误，在错误列表面板中，点击“错误”（Errors）。

注释掉导致错误列表中显示的错误的代码。
这些错误是由 `doTests_Click` 方法中的六条语句引起的：
   - 在错误列表中，双击第一个错误。该错误位于 StressTest Harness 解决方案的 `MainWindow.xml` 文件中。
   - 在 `MainWindow` 类中，在 `doTests_Click` 方法中注释掉引发错误的六行代码。

你的代码应该类似于下面的代码示例。

```csharp
private void doTests_Click(object sender, RoutedEventArgs e)
{
    // Material m = stc.girderMaterial;
    // CrossSection c = stc.crossSection;
    // int l = stc.lengthInMm;
    // int h = stc.heightInMm;
    // int w = stc.widthInMm;
    // tcr = stc.testCaseResult.Value;
    stc.PerformStressTest();
}
```

### 任务 4：更新单元测试以解决错误

- 在“生成”（Build）菜单中，点击“生成解决方案”。仍然有一些错误。
  剩余的错误位于单元测试项目。
- 在任务列表中，找到 `TODO - Update unit tests to resolve errors` 任务，然后双击此任务。此任务位于 `StressTestCaseTest` 单元类中。
- 在 `StressTestCaseConstructorTest` 中，注释掉导致错误的五个 `Assert` 语句。

你的代码应该类似于下面的代码示例。

```csharp
public void StressTestCaseConstructorTest()
{
    // Assert.AreEqual(Material.Composite, target.girderMaterial);
    // Assert.AreEqual(CrossSection.CShaped, target.crossSection);
    // Assert.AreEqual(5000, target.lengthInMm);
    // Assert.AreEqual(32, target.heightInMm);
    // Assert.AreEqual(18, target.widthInMm);
    ...
}
```

2. 更新该方法，通过执行以下任务来验证构造的对象是否包含正确的成员值：

> 提示：你无法直接访问成员数据，因为你刚刚声明了私有成员。`ToString` 方法返回对象的字符串表示，包含成员数据。

a. 在实例化目标对象之前，声明一个名为 `expected` 的新字符串，并使用以下代表测试预期结果的数据来填充该字符串：

`Material: Composite, CrossSection: CShape, Length: 5000mm, Height: 32mm, Width: 18mm, No Stress Test Performed`

你的代码应该类似于下面的代码示例。

```csharp
public void StressTestCaseConstructorTest()
...
string expected = "Material: Composite, CrossSection: CShape, Length: 5000mm, Height: 32mm, Width: 18mm, No Stress Test Performed";
StressTestCase target = new StressTestCase(
    girderMaterial,
    crossSection,
    lengthInMm,
    heightInMm,
    widthInMm);
...
```

b. 在方法末尾，添加一个 `Assert` 语句，检查预期字符串是否与 `target.ToString` 方法的输出匹配。

你的代码应该类似于下面的代码示例。

```csharp
public void StressTestCaseConstructorTest()
{
    ...
    StressTestCase target = new StressTestCase(
        girderMaterial,
        crossSection,
        lengthInMm,
        heightInMm,
        widthInMm);
    Assert.AreEqual(expected, target.ToString());
}
```

5. 更新 `StressTestCaseConstructorTest1` 方法并通过执行以下任务解决错误：

a. 注释掉现有的 `Assert` 语句。
b. 在方法创建目标对象之前，创建一个包含默认 `StressTestCase` 类预期结果的新字符串。此字符串与之前的测试所预期的字符串相同。
c. 在方法末尾，添加一个 `Assert` 语句，检查预期字符串是否与 `target.ToString` 的输出匹配。

你的代码应该类似于下面的代码示例。

```csharp
public void StressTestCaseConstructorTest1()
{
    string expected = "Material: StainlessSteel, CrossSection: IBeam, Length: 4000mm, Height: 20mm, Width: 15mm, No Stress Test Performed";
    StressTestCase target = new StressTestCase();
    // Assert.AreEqual(Material.StainlessSteel, target.girderMaterial);
    // Assert.AreEqual(CrossSection.IBeam, target.crossSection);
    // Assert.AreEqual(4000, target.lengthInMm);
    // Assert.AreEqual(20, target.heightInMm);
    // Assert.AreEqual(15, target.widthInMm);
    Assert.AreEqual(expected, target.ToString());
}
```
