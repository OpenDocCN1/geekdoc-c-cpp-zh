
+ b. 使用 `index` 参数的值更新本地 `position` 成员。
+ c. 将 `index` 参数加 1。
+ d. 如果 `RightTree` 属性不为空，则调用 `RightTree` 属性的 `IndexTree` 方法，并将结果赋值给 `index` 参数。将 `index` 变量的当前值传递给 `IndexTree` 方法。
+ e. 在方法末尾，返回 `index` 参数的值。

+ 9. 在 `IndexTree` 方法之后，添加一个名为 `GetItemAtIndex` 的私有方法。该方法应接受一个名为 `index` 的整数参数，并返回一个 `Tree<T>` 对象。在方法中添加代码执行以下操作：
+ a. 如果 `position` 成员的值为 -1，则调用本地 `IndexTree` 方法。将 0 作为参数传递给 `IndexTree` 方法。
+ b. 如果 `position` 成员的值大于 `index` 变量的值，则调用 `LeftTree` 属性的 `GetItemAtIndex` 方法并返回生成的值。将 `index` 参数传递给 `GetItemAtIndex` 方法。
+ c. 如果 `position` 成员的值小于 `index` 变量的值，则调用 `RightTree` 属性的 `GetItemAtIndex` 方法并返回生成的值。将 `index` 参数传递给 `GetItemAtIndex` 方法。
+ d. 在方法末尾，返回当前对象的引用。

# 构建和枚举自定义集合类 13-43

10. 在 `GetItemAtIndex` 方法之后，添加一个名为 `GetCount` 的私有方法。该方法应接受一个名为 `accumulator` 的整数参数，并返回一个整数值。在方法中添加代码执行以下操作：
+ a. 如果 `LeftTree` 属性不为空，调用 `LeftTree` 属性的 `GetCount` 方法并将结果存储在 `accumulator` 变量中。将 `accumulator` 变量的当前值传递给 `GetCount` 方法。
+ b. 将 `accumulator` 变量的值加 1。
+ c. 如果 `RightTree` 属性不为空，调用 `RightTree` 属性的 `GetCount` 方法并将结果存储在 `accumulator` 变量中。
+ d. 在方法末尾，返回 `accumulator` 变量的值。

# 任务 4：实现 IList<T> 接口方法和属性

+ 1. 找到 `IndexOf` 方法。该方法接受一个名为 `item` 的 `TItem` 对象，并返回一个整数值。
该方法应该遍历树并返回一个指示 `TItem` 对象在树中索引的值。该方法目前抛出 `NotImplementedException`。

+ 2. 将 `IndexOf` 方法中的代码替换为执行以下操作的代码：
+ a. 如果 `item` 参数为空，返回值 -1。
+ b. 如果 `position` 成员的值为 -1，调用 `IndexTree` 方法并将值 0 作为参数传递给 `IndexTree` 方法。
+ c. 将 `item` 参数的值与本地 `NodeData` 属性的值进行比较：
+ i. 如果 `item` 参数的值小于 `NodeData` 属性的值，且 `LeftTree` 参数为空，则返回 -1。否则，返回递归调用 `LeftTree.IndexOf` 方法的结果，将 `item` 的值传递给 `IndexOf` 方法。
+ ii. 如果 `item` 参数的值大于 `NodeData` 属性的值，且 `RightTree` 参数为空，则返回 -1。否则，返回递归调用 `RightTree.IndexOf` 方法的结果，将 `item` 的值传递给 `IndexOf` 方法。
> 提示：使用 `CompareTo` 方法比较 `item` 参数的值和 `NodeData` 属性的值。
+ d. 在方法末尾，返回本地 `position` 成员的值。

+ 3. 找到 `this indexer`（此索引器）。
此索引器应该返回由 `index` 指定的索引处的 `TItem` 对象。目前，`get` 和 `set` 访问器都抛出 `NotImplementedException`。

+ 4. 将 `get` 访问器中的代码替换为执行以下操作的代码：
+ a. 如果 `index` 参数的值小于零，或大于 `Count` 属性的值，则抛出带有以下参数的 `ArgumentOutOfRangeException`：
+ i. 字符串值 "index"，
+ ii. `index` 参数的值。
+ iii. 字符串值 "Indexer out of range"：
+ b. 在 `get` 访问器的末尾，调用 `GetItemAtIndex` 方法。将 `index` 变量的值传递给 `GetItemAtIndex` 方法。返回调用 `GetItemAtIndex` 方法获取的对象的 `NodeData` 属性值。

+ 5. 找到 `Clear` 方法。该方法不接受参数，且不返回值。
该方法应该清空树的内容并将其还原为初始。目前，该方法抛出 `NotImplementedException`。

+ 6. 使用以下操作替换 `Clear` 方法：
+ a. 将 `LeftTree` 属性设置为 null。
+ b. 将 `RightTree` 属性设置为 null。
+ c. 将 `NodeData` 属性设置为默认值。

# 构建和枚举集合类 13-45

+ 7. 找到 `Contains` 方法。该方法接受一个 `Titem` 参数，并返回一个布尔值。
该方法应该遍历树并返回一个指示树中是否存在与 `item` 值匹配的节点的布尔值。目前，该方法抛出 `NotImplementedException`。

+ 8. 使用以下操作替换 `Contains` 方法中的代码：
+ a. 如果 `NodeData` 属性的值与 `item` 参数的值相同，则返回 true。
+ b. 如果 `NodeData` 属性的值大于 `item` 参数的值，且 `LeftTree` 属性不为空，则返回递归调用 `LeftTree.Contains` 方法的结果。
+ c. 如果 `NodeData` 属性的值小于 `item` 参数的值，且 `RightTree` 属性不为空，则返回递归调用 `RightTree.Contains` 方法的结果。
+ d. 在方法末尾，返回 false。

+ 9. 找到 `Count` 属性。
该属性是只读的，应该返回树中项的总数。目前，`get` 访问器抛出 `NotImplementedException`。

+ 10. 将 `get` 访问器中的代码替换为调用 `GetCount` 方法，并将 `accumulator` 传递该方法。返回 `GetCount` 计算的值。

+ 11. 找到 `IsReadOnly` 属性。
该属性应该返回一个指示树是否只读的布尔值。

+ 12. 将 `get` 访问器中的代码替换为返回布尔值的语句。

+ 13. 找到 `ICollection<Titem>.Remove` 方法。该方法接受一个 `Titem` 参数 `item`，并返回一个布尔值。
该方法应该检查树中是否存在与 `item` 值匹配的节点，如果是则从树中删除该项。如果删除了项，方法应返回 true；否则，方法应返回 false。
> 注意：此 `Remove` 方法使用了接口限定，以区分 `Tree` 类其他地方定义的本地 `Remove` 方法。

14. 在 `Collection<Item>.Remove` 方法中，将现有代码替换为执行以下操作：
+ a. 如果树包含匹配的项，调用本地 `Remove` 方法，然后返回 true。
+ b. 在方法末尾，返回 false。

15. 生成解决方案并修正任何错误。

# 任务 5：使用 BinaryTreeHarness 测试解决方案

1. 在 `BinaryTreeHarness` 项目中，打开 `Program.cs` 文件并检查 `Main` 方法。
`BinaryTreeHarness` 项目包含你用于测试完成的 `Tree` 类的代码。你将在后续练习中继续扩展 `Tree` 类，因此 `Tree` 类尚未完备。因此，此练习不使用测试执行程序中的方法。`Main` 方法包含了你要执行的每个测试方法的调用。

2. 检查 `TestIntegerTree` 方法。
`TestIntegerTree` 方法测试 `Tree` 类的 `Remove` 和 `Contains` 方法以及索引功能。首先，方法调用 `CreateTreeOfIntegers` 方法构建包含 10 个值的示例树。然后，方法调用 `WalkTree` 方法，该方法按数值顺序将每个值打印到控制台。
> 注意：`CreateTreeOfIntegers` 方法创建的 `Tree` 对象包含 10, 5, 11, 5, -12, 15, 0, 14, -8 和 10，顺序为方法添加这些值的顺序。
该方法调用 `Count` 方法并将结果打印到控制台。该方法将树转换为 `ICollection` 对象，然后调用 `Remove` 方法用于从树中删除值 11。该方法会再次向控制台打印 `Count` 方法的结果，以证明某个项已被删除。
注意：`BinaryTree` 方法包含两个 `Remove` 方法，在这种情况下，测试方法应该调用接口定义的 `ICollection.Remove` 方法。为了让测试方法能够执行此操作，它必须将 `Tree` 对象强制转换为 `ICollection` 对象。
然后，该方法通过调用 `Contains` 方法传入值 11（刚刚删除）和 -12（已知在列表中存在）来测试 `Contains` 方法。
最后，该方法通过以下步骤测试索引器：首先在树中检索值 5 的索引并将其打印到控制台，然后使用相同的索引从树的该位置检索值 5。

3. `TestDeleteRootNodeInteger` 测试了 `TestDeleteRootNodeInteger` 在尝试删除树根节点时的功能。当根值从树中删除时，下一个可用节点应该被复制到它的位置，以便树能够继续运行。
在本次测试中，根节点的值为 10。存在第二个值为 10 的节点，因此必须调用两次 `Remove` 方法来删除这两个值。
该方法首先调用 `CreateTreeIntegers` 构建示例树，然后通过调用 `WalkTree` 方法将树打印到控制台。接着，该方法将 `Tree` 对象转换为 `ICollection` 对象，然后调用两次 `Remove` 方法来删除两个 10 值。最后，该方法再次调用 `WalkTree` 方法验证树仍然正常运行。

4. 检查 `TestString` 方法。
此方法使用与 `TestTree` 类似的逻辑来测试 `Count`、`Remove`、`Contains` 和索引器方法的功能。该方法使用包含字符串值 "k203","h624","p936","h624","a279","z837","e762","r483","d776" 和 "k203" 的 `BinaryTree` 对象。在本次测试中，使用字符串值 "p936" 测试 `Remove` 方法，并使用字符串值 "h624" 测试索引器。

5. 检查 `TestDeleteRootNode` 方法。
此方法使用与 `TestDeleteRootNodeInteger` 方法类似的逻辑来测试 `Remove` 方法的功能，使用了与 `TestString` 方法相同的基于字符串的树。在本次测试中，删除两次 "k203" 字符串值以测试根节点的删除。

6. 检查 `TestResultTree` 方法。
此方法使用与 `TestIntegerTree` 和 `TestString` 方法类似的逻辑来测试 `Count`、`Remove`、`Contains` 和索引方法的功能，但它使用基于 `TestResult` 类型的 `BinaryTree` 对象。
> **注意：** `TestResult` 类实现了 `IComparable` 接口，并使用 `Deflection` 属性比较 `TestResult` 对象的实例。因此，树中的项按它们的 `Deflection` 值进行索引。
在这种情况下，使用 `Deflection` 值为 226 的 `TestResult` 对象测试 `Remove` 方法。使用 `Deflection` 值为 114 的 `TestResult` 对象测试索引器。

7. 检查 `TestDeleteRootNodeTestResult` 方法。
此方法使用与 `TestDeleteRootNodeInteger` 和 `TestDeleteRootNodeString` 方法类似的逻辑来测试 `Remove` 方法的功能，使用了与 `TestResultTree` 相同的基于 `TestResult` 的树。在本次测试中，删除两次 `Deflection` 值为 190 的 `TestResult` 对象以测试根节点的删除。

8. 运行 `BinaryTreeTestHarness` 应用程序。

9. 验证控制窗口中的输出类似于下面的代码示例。

```
TestIntegerTree()
WalkTree()
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
Count: 10
```

## Remove(11)

```
Count: 9
Contains(11): False
Contains(-12): True
IndexOf(5): 3
tree[3]: 5
```

注意：
- a. 控制台显示 `TestIntegerTree` 方法的输出。
- b. 树通过 `WalkTree` 方法按数字顺序显示。
- c. 初始列表包含 10 个项，调用 `Remove` 方法后，树包含 9 个项。
- d. `Remove` 方法删除了值 11，因此 `Contains` 方法的结果为 false。同样注意，`Contains` 方法验证了值 -12 的存在。
- e. `IndexOf` 方法报告值 5 位于列表的第 3 位置。这通过检索位置 3 的值（显示为 5）得到了确认。

10. 按下回车键，然后验证控制窗口中的输出类似于下面的代码示例。

```
TestDeleteRootNodeInteger()
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

注意第一个列表中树显示了两个值为 10 的实例。在删除这些值之后，列表将不再包含它们。还要注意，在删除根值后，树保留了剩余值并继续按预期运行。

11. 按下回车键，然后验证控制窗口中的输出符合代码示例。

```
TestStringTree()
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
Contains("a279"): True
IndexOf("h624"): 3
tree[3]: h624
```

这与步骤 9 中执行的测试相同，但使用的是字符串数据。列表中的项按字母顺序显示。

12. 按下回车键，然后验证控制窗口中的输出符合代码示例。

```
TestDeleteRootNodeString()
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

13. 按下回车键，然后验证控制窗口中的输出符合代码示例。

```
TestResultTree()
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

这与步骤 9 和 11 中执行的测试相同，但此测试基于 `TestResult` 对象。项按 `Deflection` 属性值的数字顺序显示。

14. 按下回车键，然后验证控制窗口中的输出符合代码示例。
