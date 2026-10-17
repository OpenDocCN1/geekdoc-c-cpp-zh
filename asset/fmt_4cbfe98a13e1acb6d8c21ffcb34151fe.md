
# TestDeleteRootNodeTestResults()

```
Before
Deflection: 0, AppliedStress: 10, Temperature: 200, Date: 3/18/2010
Deflection: 38, AppliedStress: 20, Temperature: 200, Date: 3/18/2010
Deflection: 76, AppliedStress: 30, Temperature: 200, Date: 3/18/2010
Deflection: 114, AppliedStress: 40, Temperature: 200, Date: 3/18/2010
Deflection: 114, AppliedStress: 50, Temperature: 200, Date: 3/18/2010
Deflection: 190, AppliedStress: 60, Temperature: 200, Date: 3/18/2010
Deflection: 190, AppliedStress: 70, Temperature: 200, Date: 3/18/2010
Deflection: 266, AppliedStress: 80, Temperature: 200, Date: 3/18/2010
Deflection: 304, AppliedStress: 90, Temperature: 200, Date: 3/18/2010
Deflection: 342, AppliedStress: 100, Temperature: 200, Date: 3/18/2010
Removed Deflection 190
After
Deflection: 0, AppliedStress: 10, Temperature: 200, Date: 3/18/2010
Deflection: 38, AppliedStress: 20, Temperature: 200, Date: 3/18/2010
Deflection: 76, AppliedStress: 30, Temperature: 200, Date: 3/18/2010
Deflection: 114, AppliedStress: 40, Temperature: 200, Date: 3/18/2010
Deflection: 114, AppliedStress: 50, Temperature: 200, Date: 3/18/2010
Deflection: 266, AppliedStress: 80, Temperature: 200, Date: 3/18/2010
```

- 15. 按下两次回车键返回 Visual Studio。

# 练习 2：通过编写实现枚举器

`BinaryTree` 类必须支持 C# 的 `foreach` 语句以遍历 `BinaryTree` 对象的内容。你将在 `BinaryTree` 类中实现 `IEnumerable<T>` 接口的 `GetEnumerator` 方法，返回一个 `foreach` 语句可以使用的枚举器。

你将实现 `Dispose`、`MoveNext` 和 `Reset` 方法以及 `Current` 属性。然后，你将修改 `BinaryTree` 类中泛型的 `GetEnumerator` 方法以返回该枚举器的实例，并使用 `foreach` 循环测试该枚举器。

本次练习的主要任务如下：

- 1. 打开 CustomCollections 解决方案。
- 2. 创建 `TreeEnumerator` 类。
- 3. 添加类级变量和构造函数。
- 4. 添加一个填充队列的方法。
- 5. 实现 `IEnumerator<T>` 和 `IEnumerator` 方法。
- 6. 实现 `IDisposable` 接口。
- 7. 修改 `Tree` 类以返回一个 `TreeEnumerator` 对象。
- 8. 使用 `BinaryTreeTestHarness` 应用程序测试这些方法。

## 任务 1：打开 CustomCollections 解决方案

- 打开 `E:\Labfiles\Lab 13\Ex2\Starter` 文件夹下的 CustomCollections 解决方案。

> **注意**：Ex2 文件夹中的 CustomCollections 解决方案在功能上与你在练习 1 中完成的代码相同。但是，它包含更新后的任务列表和更新的测试辅助程序，以便你完成本次练习。

## 任务 2：创建 TreeEnumerator 类

- 在 BinaryTree 项目中，添加一个名为 `TreeEnumerator` 的新类。该类应实现 `IEnumerator` 接口，并接收一个类型参数 `TItem`，其中 `TItem` 类型实现了 `IComparable` 接口。

## 任务 3：添加类级变量和构造函数

- 1. 在 `TreeEnumerator` 类中，添加以下变量：
  - a. 一个名为 `currentData` 的 `Tree<TItem>` 对象，初始化为 `null`。
    此成员将存储构造时传递给类的初始 `Tree` 对象数据，并用于向内部队列填充数据。该数据也被存储以便重置内部队列。
  - b. 一个名为 `currentItem` 的 `TItem` 对象，初始化为默认 `TItem` 对象。
    此成员将存储从队列中移除的最后一个项。
  - c. 一个名为 `enumData` 的私有 `Queue<TItem>` 对象，初始化为 `null`。
    此成员持有枚举器将遍历的项的内部队列。你把 `Tree` 对象中的项填充到此队列。
- 2. 添加一个构造函数，它应该接受一个名为 `data` 的 `Tree<TItem>` 参数，并用该参数的值初始化 `currentData` 成员。

## 任务 4：添加一个填充队列的方法

- 在构造函数下方，添加一个名为 `Populate` 的新私有方法。该方法应接受一个名为 `enumQueue` 的 `Queue<TItem>` 参数和一个名为 `tree` 的 `Tree<TItem>` 参数。它不返回值。在方法中添加代码执行以下操作：
  - a. 如果参数 `tree` 的 `LeftTree` 属性不为 `null`，则递归调用 `Populate` 方法，并将 `enumQueue` 参数和 `tree.LeftTree` 属性作为参数传递给方法。
  - b. 将参数 `tree` 的 `NodeData` 属性值添加到 `enumQueue` 队列中。
  - c. 如果参数 `tree` 的 `RightTree` 属性不为 `null`，则递归调用 `Populate` 方法，并将 `enumQueue` 参数和 `tree.RightTree` 属性作为参数传递给方法。

此代码遍历树并按顺序将找到的每个项填充队列。

# 构建并枚举自定义集合类

## 任务 5：实现 IEnumerator<T> 和 IEnumerator 方法

- 1. 在类定义中，右键点击 `IEnumerator`，指向“实现接口”，然后点击“显式实现接口”。
  Visual Studio 将为 `IEnumerator<>`、`IEnumerator` 和 `IDisposable` 接口公开的方法和属性生成存根。
- 2. 找到 `Current` 属性。
  此属性应返回从队列移除的最后一个 `TItem` 对象。
- 3. 在 `Current` 属性的 `get` 访问器中，替换现有代码以执行以下操作：
  - a. 如果 `enumData` 为 `null`，则抛出一个新的 `InvalidOperationException` 异常，消息为“Use MoveNext before calling Current”。
  - b. 返回 `currentItem` 成员的值。
- 4. 找到 `MoveNext` 方法。该方法不接受参数并返回一个布尔值。
  `MoveNext` 方法应确保内部队列已初始化，从内部队列检索下一个项，然后将其存储在 `currentItem` 属性中。如果操作成功，方法返回 `true`，否则返回 `false`。
- 5. 在 `MoveNext` 方法中，替换现有代码执行以下操作：
  - a. 如果 `enumData` 为 `null`，创建一个新的队列对象并调用 `Populate` 方法，将新队列对象和 `currentData` 成员作为参数传递给方法调用。
  - b. 如果 `enumData` 对象包含任何值，检索队列中的第一个项，将其存储在 `currentItem` 成员中，然后返回布尔值 `true`。
  - c. 在方法结束处，返回布尔值 `false`。
- 6. 找到 `Reset` 方法。该方法不接受参数且不返回值。
  此方法应将枚举器重置为初始状态。你通过用 `Tree` 对象中的数据重新填充内部队列来实现这一点。
- 7. 在 `Reset` 方法中，替换现有代码调用 `Populate` 方法，将 `enumData` 和 `currentData` 成员作为参数传递。
- 8. 生成解决方案并修正任何错误。

## 任务 6：实现 IDisposable

- 1. 在 `TreeEnumerator` 类中，找到 `Dispose` 方法。该方法不接受参数且不返回值。
  此方法应释放任何可能无法回收的资源。
- 2. 在 `Dispose` 方法中，替换现有代码清除 `enumData`。
- 3. 生成解决方案并修正任何错误。

## 任务 7：修改 Tree 类以返回 TreeEnumerator 对象

- 1. 在 `Tree` 类中，找到 `GetEnumerator` 方法。
- 2. 在 `GetEnumerator` 方法中，替换现有代码创建并初始化 `TreeEnumerator` 对象。指定 `TItem` 类型为参数，并将 `currentData` 作为参数传递给 `TreeEnumerator` 构造函数。返回创建的 `TreeEnumerator` 对象。
- 3. 生成解决方案并修正任何错误。

## 任务 8：使用 BinaryTreeTestHarness 应用程序测试方法

- 1. 在 `BinaryTestHarness` 项目中，打开 `Program.cs` 文件。
  此版本的 `BinaryTestHarness` 项目包含与练习 1 相同的代码并执行相同的测试。但是，它已更新，以测试你添加的枚举器功能。
- 2. 检查 `TestIteratorsInteger` 方法。
  该方法通过使用与练习 1 相同的整数树来测试你实现的迭代器功能。该方法通过调用 `CreateIntegerField` 方法构建树，然后使用 `foreach` 语句遍历列表并将每个值打印到控制台。随后，该方法尝试反向遍历树，并将每个项打印到控制台。
  > **注意**：你将在下次练习中添加启用树反向遍历的功能。预计尝试反转树将抛出 `NotImplementedException`。`TestIteratorsIntegers` 方法会在异常发生时捕获它，并在控制台上打印一条消息。
- 3. 检查 `TestIteratorsStrings` 方法。
  该方法使用与 `TestIteratorsInteger` 方法类似的逻辑来测试 `BinaryTree` 对象的迭代器功能，但它使用了与你在练习 1 中使用的相同的字符串树。该方法使用 `CreateATreeOfStrings` 方法构建树，遍历树，并将所有项打印到控制台。该方法还尝试反向显示树中的数据并将遇到 `NotImplementedException`（你将在下次练习中实现此功能）。
- 4. 检查 `TestIteratorsTestResults` 方法。
  该方法使用与 `TestIteratorsInteger` 和 `TestIteratorsStrings` 方法类似的逻辑来测试 `BinaryTree` 对象的迭代器功能。它通过调用 `CreateATreeOfTestResults` 方法像练习 1 那样使用基于 `TestResult` 的树。
- 5. 运行 `BinaryTestHarness` 应用程序。
- 6. 验证控制台窗口中的输出是否与以下代码示例匹配。

### TestIntegerTree()

```
WalkTree()
-12
-8
0
5
5
10
11
14
15

Count: 10

Remove(11)

Count: 9

Contains(11): False

Contains(-12): True

IndexOf(5): 3
tree[3]: 5
```

此输出与练习 1 中的 `TestIntegerTree` 方法输出匹配，并证实了你在添加迭代器功能时没有破坏现有功能。

7. 按回车键，然后验证控制台窗口中的输出是否与以下代码示例匹配。

### TestDeleteRootNodeInteger()

```
Before
-12
-8
0
5
5
10
10
11
14
15
Remove 10 twice
After
-12
-8
0
5
5
11
14
15
```

此输出与练习 1 中的 `TestDeleteRootNodeInteger` 方法输出匹配，再次证实了现有功能按预期工作。

- 8. 按回车键，然后验证控制台窗口中的输出是否与以下代码示例匹配。

### TestIteratorsIntegers()

```
升序排列
-12
-8
0
5
10
10
11
14
15
降序排列
你将在练习 3 中实现此功能
```

> **注意**：列表中的项目按数字顺序显示，并且注意 `Reverse` 方法显示了一条消息，指示 `Reverse` 功能尚未实现。

- 9. 按回车键，然后验证控制台窗口中的输出是否与以下代码示例匹配。

### TestStringTree()

```
WalkTree()
a279
d776
e762
h624
h624
k203
k203
p936
r483
z837
Count: 10
Remove("p936")
Count: 9
Contains("p936"): False
Contains("a279"): True
IndexOf("h624"): 3
tree[3]: h624
```

此输出与练习 1 中的 `TestStringTree` 方法输出匹配。

10. 按回车键，并验证控制台窗口中的输出是否与以下代码示例匹配。

### TestDeleteRootNodeString()

```
Before
a279
d776
e762
h624
h624
k203
k203
p936
r483
z837
Remove k203 twice
After
a279
d776
e762
h624
h624
p936
r483
z837
```

此输出与练习 1 中的 `TestDeleteRootNodeString` 方法输出匹配。

11. 按回车键，然后验证控制台窗口中的输出是否与以下代码示例匹配。

### TestIteratorsStrings()

```
升序排列
a279
d776
e762
h624
h624
k203
k203
p936
r483
z837
降序排列
未实现。你将在练习 3 中实现此功能
```

注意这代表了你在步骤 8 中执行的相同测试。它使用字符串数据来验证迭代器功能，所有项目都按字母顺序显示。

12. 按回车键，并验证控制台窗口中的输出是否与以下代码示例匹配。

### TestResultTree()

```
WalkTree()
Deflection: 0, AppliedStress: 10, Temperature: 200, Date: 3/18/2010
Deflection: 38, AppliedStress: 20, Temperature: 200, Date: 3/18/2010
Deflection: 76, AppliedStress: 30, Temperature: 200, Date: 3/18/2010
Deflection: 114, AppliedStress: 40, Temperature: 200, Date: 3/18/2010
Deflection: 114, AppliedStress: 50, Temperature: 200, Date: 3/18/2010
Deflection: 190, AppliedStress: 60, Temperature: 200, Date: 3/18/2010
Deflection: 190, AppliedStress: 70, Temperature: 200, Date: 3/18/2010
Deflection: 266, AppliedStress: 80, Temperature: 200, Date: 3/18/2010
Deflection: 304, AppliedStress: 90, Temperature: 200, Date: 3/18/2010
Deflection: 342, AppliedStress: 100, Temperature: 200, Date: 3/18/2010
Count: 10
Remove(def266)
Count: 9
Contains(def266): False
Contains(def0): True
IndexOf(def114): 3
tree[3]: Deflection: 114, AppliedStress: 40, Temperature: 200, Date: 3/18/2010
```

此输出与练习 1 中的 `TestResultTree` 输出匹配。

13. 按回车键，并验证控制台窗口中的输出是否与以下代码示例匹配。

### TestDeleteRootTestMethod()

```
Before
```
