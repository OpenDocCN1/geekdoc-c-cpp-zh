
回调方法（`handleWriteCompleted`）的参数是一个 `IAsyncResult` 对象，其中包含有关异步操作状态的信息以及任何其他状态信息。你可以将用户定义的信息传递给回调中的此参数；传递给 `BeginOperationName` 方法的最后一个参数被打包到此参数中。在此示例中，回调传递了对 `MemoryStream` 的引用。

尽管此序列有效，但它是一个混乱的范式，掩盖了你正在执行的操作。操作的代码被拆分为两个方法，如果你需要维护此代码，很容易在这些方法之间失去心理联系。如果你使用 `Task` 对象，可以通过调用 `TaskFactory` 类的静态 `FromAsync` 方法来简化此模型。此方法接受 `BeginOperationName` 和 `EndOperationName` 方法，并将它们包装成由 `Task` 执行的代码。无需创建 `AsyncCallback` 委托，因为 `FromAsync` 方法在幕后生成它。因此，你可以像这样执行与前一个示例中相同的操作：

```
Byte[] buffer = ...;

MemoryStream s = new MemoryStream();

Task t = Task<int>.Factory.FromAsync(s.BeginWrite, s.EndWrite,
                                    buffer, 0,
                                    buffer.Length, null);

t.Start();

await t;
```

如果需要访问在 `.NET Framework` 早期版本中开发的类型所公开的异步功能，此技术很有用。

## 使用 PLINQ 并行化声明式数据访问

数据访问是响应时间很重要的另一个领域，尤其是当你构建需要搜索冗长数据结构的应用程序时。在之前的章节中，你看到了 `LINQ` 从可枚举数据结构中检索数据的强大功能，但所展示的示例本质上是单线程的。`PLINQ` 提供了一组基于 `Tasks` 的 `LINQ` 扩展，可帮助你提高性能并并行化某些查询操作。

`PLINQ` 通过将数据集划分为分区，然后使用任务并行检索与查询为每个分区指定的条件匹配的数据来工作。当任务完成后，为每个分区检索的结果合并为单个可枚举结果集。`PLINQ` 非常适合涉及包含大量元素的 数据集的场景，或者如果为匹配数据指定的条件涉及复杂、计算成本高昂的操作。

`PLINQ` 的一个重要目标是尽可能不具侵入性。要将 `LINQ` 查询转换为 `PLINQ` 查询，可使用 `AsParallel` 扩展方法。`AsParallel` 方法返回一个 `ParallelQuery` 对象，其行为与原始可枚举对象类似，只是它为许多 `LINQ` 运算符（如 `join` 和 `where`）提供了并行实现。这些 `LINQ` 运算符的实现基于任务，并使用各种算法尝试在可能的情况下并行运行 `LINQ` 查询的各个部分。然而，正如并行计算世界中永远不变的规律一样，`AsParallel` 方法并非魔法。你无法保证代码会加速；一切都取决于你的 `LINQ` 查询的性质以及它们执行的任务是否适合并行化。

要了解 `PLINQ` 的工作原理以及它有用的情况，查看一些示例会有帮助。以下各节中的练习演示了一对简单场景。

## 使用 PLINQ 在迭代集合时提高性能

第一个场景很简单。考虑一个迭代集合并基于处理器密集型计算从集合中检索元素的 `LINQ` 查询。只要计算相互独立，此类查询就可以从并行执行中受益。集合中的元素可以划分为多个分区；确切数量取决于计算机当前负载和可用 `CPU` 数量。每个分区中的元素可以由单独的线程处理。当所有分区都处理完毕后，结果可以合并。任何通过索引访问元素的集合，例如数组或实现 `IList<T>` 接口的集合，都可以以这种方式管理。

### 并行化对简单集合的 LINQ 查询

1. 使用 `Visual Studio 2015`，打开 `PLINQ` 解决方案，该解决方案位于你的 `Documents` 文件夹中的 `\Microsoft Press\VCSBS\Chapter 24\PLINQ` 文件夹中。
2. 在 `Solution Explorer` 中，双击 `PLINQ` 项目中的 `Program.cs`，以在代码和文本编辑器窗口中显示该文件。

这是一个控制台应用程序。应用程序的骨架结构已为你创建。`Program` 类包含名为 `Test1` 和 `Test2` 的方法，说明了一对常见场景。`Main` 方法依次调用这两个测试方法。

这两个测试方法具有相同的总体结构：它们创建了一个 `LINQ` 查询

```
(you will add the code to do this later in this set of exercises), run it, and display the time taken. The code for each of these methods is almost completely separate from the statements that actually create and run the queries.
```

3. Examine the `Test1` method.

此方法创建一个大型整数数组并用一组介于 0 和 200 之间的随机数填充它。随机数生成器已设置种子，因此每次运行应用程序时你都应获得相同的结果。

4. Immediately after the first `TODO` comment in this method, add the `LINQ` query shown here in bold:

```
// TO DO: Create a LINQ query that retrieves all numbers that are greater than 100
var over100 = from n in numbers
    where TestIfTrue(n > 100)
    select n;
```

此 `LINQ` 查询检索 `numbers` 数组中所有值大于 100 的项。测试 `n > 100` 本身计算密集程度不足以显示并行化此查询的好处，因此代码调用名为 `TestIfTrue` 的方法，该方法通过执行 `SpinWait` 操作使其变慢一点。`SpinWait` 方法使处理器在短时间内不断执行特殊的“无操作”指令循环，保持处理器忙碌但实际上不做任何工作。 （这称为自旋。）`TestIfTrue` 方法如下所示：

```
public static bool TestIfTrue(bool expr)
{
    Thread.SpinWait(1000);
    return expr;
}
```

5. After the second `TODO` comment in the `Test1` method, add the following code shown in bold:

```
// TO DO: Run the LINQ query, and save the results in a List<int> object
List<int> numbersOver100 = new List<int>(over100);
```

记住 `LINQ` 查询使用延迟执行，因此它们在你检索结果之前不会运行。此语句创建一个 `List<int>` 对象并用运行 `over100` 查询的结果填充它。

6. After the third `TO DO` comment in the `Test1` method, add the following statement shown in bold:

```
// TO DO: Display the results
Console.WriteLine($"There are {numbersOver100.Count} numbers over 100");
```

7. On the `Debug` menu, click `Start Without Debugging`. Note the time that running `Test 1` takes and the number of items in the array that are greater than 100.

8. Run the application several times, and take an average for the time. Verify that the number of items greater than 100 is the same each time (the application uses the same random number seed each time it runs to ensure the repeatability of the tests). Return to `Visual Studio` when you have finished.

9. The logic that selects each item returned by the `LINQ` query is independent of the selection logic for all the other items, so this query is an ideal candidate for partitioning. Modify the statement that defines the `LINQ` query, and specify the `AsParallel` extension method to the `numbers` array, as shown here in bold:

```
var over100 = from n in numbers.AsParallel()
    where TestIfTrue(n > 100)
    select n;
```
