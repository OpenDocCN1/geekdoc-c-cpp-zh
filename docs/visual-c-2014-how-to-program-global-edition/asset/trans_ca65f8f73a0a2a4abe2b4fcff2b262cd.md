

# 第 21 章 泛型集合：使用 LINQ/PLINQ 进行函数式编程

```csharp
Console.Write("\nValues: ");
// 使用 enumerator 遍历 int 数组
enumerator = intValues.GetEnumerator();
while (enumerator.MoveNext()) {
    Console.Write($"{enumerator.Current}");
}
Console.Write("\nValuesCopy: ");
// 使用 foreach 语句遍历第二个 int 数组
foreach (var element in intValuesCopy) {
    Console.Write($"{element}");
}
Console.WriteLine();
```

初始数组值：
doubleValues: 8.4 9.3 0.2 7.9 3.4
intValues: 1 2 3 4 5 6
intValuesCopy: 0 0 0 0 0 0

执行 Sort 和 Copy 后的数组值：
doubleValues: 0.2.2 3.4 7.9 8.4 9.3
intValues: 1 2 3 4 5 6
intValuesCopy: 1 2 3 4 5 6

在 intValues 的元素 4 处找到 5
在 intValues 中未找到 8763

> 图 21.3 | 用于常用数组操作的 Array 类静态方法。（3 部分中的 3 部分）

## 21.3.1 C# using static 指令

第 3 行和第 5 行的指令使用了命名空间 System（用于 Array 和 Console）和 System.Collections（用于接口 Enumerator，稍后我们将讨论）。第 4 行引入了 C# 6 的 `using static` 指令，用于无需完全限定名称即可访问类型的静态成员——在此情况下为 Array 类的静态成员。第 23 行

```csharp
Sort(doubleValues); // 对 Array 静态方法 Sort 的未限定调用
```

显示了对 Array 静态 Sort 的未限定调用，它等同于
```csharp
Array.Sort(doubleValues); // 调用 Array 静态方法 Sort
```

虽然我们也可以对 Array 的所有静态成员使用未限定调用（例如第 26 行的 Copy 以及第 33 和第 39 行的 BinarySearch），但使用完全限定的方法调用代码更具可读性，这清晰地表明了哪个类包含泛型方法。

## 21.3 Array 类和 Enumerator

## 21.3.2 Array 类的静态字段

我们的类声明了静态数组变量（10–12）。前两行分别将 intValues 和 doubleValues 初始化为 int 数组和 double 数组；`static int intValuesCopy` 用于演示 Array 的 Copy 方法——它初始为 `null`，因此它不引用任何数组。

第 17 行将 intValues 初始化为与 arrayValues 长度相同的数组。第 20 行调用 PrintArrays 方法（46–77）来输出所有三个数组的内容。我们稍后会讨论 PrintArrays 方法。图 21.3 的输出显示 intValuesCopy 的每个元素都被初始化为默认值 0。

## 21.3.3 Array 方法 Sort

第 23 行使用静态数组方法 Sort 对 doubleValues 进行升序排序。数组中的元素必须实现 `IComparable` 接口（所有简单类型都实现了），这使得 Sort 方法能够比较元素以确定它们的顺序。

## 21.3.4 Array 方法 Copy

第 26 行使用静态数组方法 Copy 将元素从 intValues 复制到数组 intValuesCopy。第一个参数是源数组（intValues），第二个参数是目标数组（intValuesCopy），第三个参数是表示要复制的元素数量（在本例中，`intValues.Length` 指定了所有元素）。Array 类还提供了复制数组部分内容的重载。

## 21.3.5 Array 方法 BinarySearch

第 39 行和第 30 行调用静态方法 BinarySearch 对数组 intValues 执行二分查找。BinarySearch 方法接收要搜索的排序数组以及要搜索的键。该方法返回键在数组中未找到（或返回负数）的索引。BinarySearch 假设它接收的是一个排序后的数组。它在未排序数组上的行为是未定义的。第 18 章将详细讨论搜索。

## 21.3.6 Array 方法 GetEnumerator 和接口 IEnumerator

PrintArrays 方法（46–77）使用 Array 类遍历数组的元素。Array 类实现了 `IEnumerator`（`IEnumerable<T>` 的非泛型版本）。所有数组都继承自 Array，因此 `int[]` 和数组类型都实现了 `IEnumerator` 方法 `GetEnumerator`，它返回一个可以迭代集合的 enumerator——此方法始终返回一个位于第一个元素之前的 enumerator。接口 `IEnumerator` 定义了 `MoveNext` 和属性 `Current`：

- `MoveNext` 将 enumerator 移动到集合中的下一个元素。第一次调用 `MoveNext` 将 enumerator 移动到集合的第一个元素——如果存在元素，`MoveNext` 返回 `true`；否则方法返回 `false`。
- `Reset` 方法将 enumerator 置于集合的第一个元素之前。
- 属性 Current 返回集合中当前位置的对象（由上一次调用 `MoveNext` 决定）。

Enumerator 不能修改集合的内容，只能获取内容。

![](img/57baed2319be0bb1b5f98674846f2711_890_0.png)

### 常见编程错误 21.1

> 在创建集合的 enumerator 后修改该集合，该 enumerator 将立即失效。

在创建集合的 enumerator 后修改该集合，该 enumerator 将立即失效。

