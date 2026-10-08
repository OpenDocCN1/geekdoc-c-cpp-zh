
在这种情况下，我们在声明时创建并初始化了数组元素。在下图，我们看到当数组的值在声明瞬间初始化时，数组在内存中是如何分配的：

| 栈 (Stack) | 堆 (Heap) |
|---|---|
| `myArray` -> | 0 1 2 3 4 5 |
| | 1 2 3 4 5 6 |

使用这种语法，我们用大括号代替 `new` 运算符。在括号之间列出数组的初始值，用逗号分隔。它们的数量定义了数组的长度。

## 数组的声明与初始化 – 示例

这是一个如何声明和初始化数组的示例：

```
string[] daysOfWeek =
{ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday",
"Saturday", "Sunday" };
```

在这种情况下，我们分配了一个包含七个 `string` 类型元素的数组。下图显示了当数组的值在声明时初始化时，数组在内存中是如何分配的：

![](img/251ffe19d2b15f8a8f566ab01924bb12_237_0.png)

## 数组边界

数组是基于索引的，这意味着枚举从 0 开始。第一个元素是 0，最后一个元素是 N-1。

## 访问元素

我们使用索引直接访问数组。这里有一个设置值的示例：

```
myArray[index] = 100;
```

在上面的示例中，我们分配了一个包含六个整数的数组。这里有一个修改某些值的示例：

```
int[] myArray = new int[6];
myArray[5] = 5;
```

修改后，数组如下所示：

![](img/251ffe19d2b15f8a8f566ab01924bb12_238_0.png)

我们可以使用循环遍历数组。常见的迭代形式是 `for` 循环：

```
int[] arr = new int[5];
for (int i = 0; i < arr.Length; i++)
{
  arr[i] = i;
}
```

## 数组越界

.NET Framework 对每次元素访问进行自动检查，确定索引是否有效。当我们尝试访问数组中的无效（不存在）元素时，会抛出 `IndexRangeException`。自动检查有助于开发者在处理数组时发现错误。当然，检查是有代价的。但与避免“越界”、“访问未分配内存”等错误相比，这不算什么。

这里有一个尝试访问范围外的示例：

```c
# IndexOutOfRangeExample.cs
class IndexOfRangeExample
{}
static void Main()
{
    int[] myArray = { 1, 2, 3, 4, 5, 6 };
    Console.WriteLine(myArray[6]);
}
```

在上面的示例中，我们分配了一个包含六个整数的数组。第一个索引是 0，最后一个索引是 5。我们尝试向控制台打印元素 6，但不存在该元素导致了异常：

![](img/251ffe19d2b15f8a8f566ab01924bb12_239_0.png)

## 反转数组 – 示例

在下一个示例中，我们将使用索引访问并修改元素。任务是倒序打印元素。我们将使用辅助数组来反转数组，其中保留第一个数组的元素，但顺序倒置。

```csharp
// ArrayReverseExample.cs
class ArrayReverseExample
{
    int[] array = { 1, 2, 3, 4, 5 };
    // 获取数组大小
    int length = array.Length;
    // 声明并创建反转数组
    int[] reversed = new int[length];
    // 初始化反转数组
    for (int index = 0; index < length; index++)
    {
        reversed[length - index - 1] = array[index];
    }
}
```

```
// 打印反转数组
for (int index = 0; index < length; index++)
{
    Console.Write(reversed[index] + " ");
}
// 输出: 5 4 3 2 1
```

该示例的工作原理如下：最初，我们分配一个 `int` 类型的一维数组，并用 1 到 5 的数字对其进行初始化。之后，我们将数组的长度存储在变量 `length` 中。注意，我们使用了 `Length` 属性，它返回数组元素的总数。在 C# 中，每个数组都有一个 `length` 属性。

随后，我们声明了一个相同长度的数组 `reversed`，用于存储原始数组的元素，但按反序排列。

为了反转元素，我们使用 `for` 循环。在每次迭代中，我们将 `index` 变量加 1，并确保访问了数组的所有连续元素。循环条件确保了数组将从头到尾进行迭代。

让我们看看遍历数组时发生了什么。在第一次迭代中，`index` 的值为 0。通过 `array[index]` 我们访问数组的第一个元素，相应地，通过 `reversed[length - index - 1]` 我们访问新数组 `reversed` 的最后一个元素并进行赋值。因此，我们将数组第一个元素的赋值赋给反转数组的最后一个元素。每次迭代中，`index` 都会加 1。这样，我们按照 `array` 的顺序访问下一个元素，按 `reversed` 的顺序访问上一个元素。

结果是我们反转了数组并打印了它。在示例中，我们展示了数组的连续迭代，也可以使用不同类型的循环结构（例如 `while` 和 `foreach`）。

# 从控制台读取数组

让我们看看如何从控制台读取数组的值。使用 `for` 循环和 .NET Framework 工具从控制台读取。

最初，我们使用 `Console.ReadLine()` 从控制台读取一行，然后使用 `int.Parse()` 将该行解析为整数并赋值给变量 `n`。然后我们将数字 `n` 作为数组的长度。

```csharp
int n = int.Parse(Console.ReadLine());
int[] array = new int[n];
```

242 C# 计算机编程基础

我们再次使用循环来遍历数组。在每次迭代中，我们将当前元素设置为从控制台读取的内容。循环将执行 `n` 次，这意味着它将遍历数组，因此我们将数组的每个元素读取一个值：

```csharp
for (int i = 0; i < n; i++)
{
  array[i] = int.Parse(Console.ReadLine());
}
```

# 检查对称数组 – 示例

如果数组的第一个元素和最后一个元素相等，同时第二个元素和倒数第二个元素也相等，依此类推，则数组是对称的。在图中显示了对称数组的示例：

![](img/251ffe19d2b15f8a8f566ab01924bb12_241_0.png)

在下一个示例中，我们将检查一个数组是否对称：

```csharp
Console.Write("Enter a positive integer: ");
int n = int.Parse(Console.ReadLine());
int[] array = new int[n];
Console.WriteLine("Enter the values of the array:");
for (int i = 0; i < n; i++) {
  array[i] = int.Parse(Console.ReadLine());
}
bool symmetric = true;
for (int i = 0; i < array.Length / 2; i++) {
  if (array[i] != array[n - i - 1]) {
    symmetric = false;
    break;
  }
}
Console.WriteLine("Is symmetric? {0}", symmetric);
```

# 第 7 章 数组 243

我们初始化一个数组并从控制台读取其元素。我们需要遍历数组的一半来检查它是否是对称的。数组中间元素的索引为 `array.Length / 2`。如果长度是奇数，则索引是中间位置；如果是偶数，则索引位于中间的右侧（中间位于两个元素之间）。循环从 0 运行到 `array.Length / 2`（不包含边界）。

为了检查数组是否对称，我们使用一个 `bool` 变量，并最初假设数组是对称的。在遍历数组期间，比较第一个和最后一个元素、第二个和倒数第二个元素，依此类推。如果在某一点点比较的元素不相等，我们将 `bool` 变量设置为 `false`，这意味着该数组不是对称的。

最后，我们将 `bool` 变量的值打印到控制台。

# 向控制台打印数组

在完成对数组的操作后，我们通常需要将给定数组元素打印到控制台。

向控制台打印数组元素的方法与初始化元素类似，即通过循环遍历数组。打印没有严格的规则，但通常会使用某种适当的格式。

常见的错误是尝试像打印数字一样打印数组：

```csharp
string[] array = {"one", "two", "three"};
Console.WriteLine(array);
```

遗憾的是，这段代码并没有打印数组的元素。我们得到的是：

![](img/251ffe19d2b15f8a8f566ab01924bb12_241_0.png)

我们手动打印数组元素：

```csharp
string[] array = {"one", "two", "three"};
for (int i = 0; i < array.Length; i++) {
    Console.WriteLine(array[i]);
}
```

243 C# 计算机编程基础

使用循环迭代

遍历数组最常用的结构之一是 `for` 循环。我们可以根据需要遍历数组。这里是一个示例：

```csharp
int[] array = {1, 2, 3, 4};
for (int i = 0; i < array.Length; i++) {
    Console.WriteLine(array[i]);
}
```

## 遍历数组

使用 `for` 循环我们将遍历数组，这将打印当前元素。结果如下：

```csharp
int[] array = {1, 2, 3, 4};
for (int i = 0; i < array.Length; i++) {
    Console.WriteLine(array[i]);
}
```

# "foreach" 循环迭代

遍历数组元素最常用的结构之一是 `foreach`。C# 中的 `foreach` 循环结构如下：

```csharp
foreach (var item in collection)
{
    // 在此处处理值
}
```

通常情况下，`foreach` 循环结构与 `for` 循环具有相同的属性。主要区别在于迭代总是通过所有元素——从开始到结束。我们无法访问当前索引，只是以某种方式遍历集合，这种方式是由集合本身定义的。对于数组，迭代的顺序是从第一个元素到连续

最后一种。`foreach` 循环中的循环变量是只读的，因此我们无法在循环体中修改当前的循环项。

当我们不需要更改元素只需要读取它们时，会使用 `foreach` 语句。

## 使用 "foreach" 进行迭代——示例

在下一个数组中，我们将学习如何使用 `foreach` 循环遍历数组：

```csharp
string[] capitals =
{ "Sofia", "Washington", "London", "Paris" };
foreach (string capital in capitals)
{
    Console.WriteLine(capital);
}
```

声明数组 `capitals` 后，我们使用 `foreach` 循环遍历数组并将元素打印到控制台。每个元素存储在变量 `capital` 中。执行代码得到的结果：

Sofia
Washington
London
Paris

## 多维数组

一维数组在数学中也称为向量。我们经常需要超过一个维度的数组。例如，我们可以很容易地将棋盘表示为 8x8 的二维数组（水平方向8个单元格，垂直方向8个单元格）。

## 什么是多维数组？什么是矩阵？

C# 中的每个有效类型都可以用于数组。因此，我们可以拥有数组的数组，稍后我们将讨论。

我们使用 `int[]` 声明一维整数数组，使用 `int[,]` 声明二维数组。这个示例显示了：

```csharp
int[,] twoDimensionalArray;
```

这些数组被称为二维，因为它们有两个维度。通常情况下，超过一个维度的数组被称为多维。我们可以通过增加一个维度声明三维数组：

```csharp
int[,,] threeDimensionalArray;
```

理论上数组维度没有限制，但在实践中我们不使用超过两个维度的数组，因此专注于二维数组。

## 多维数组的声明与分配

我们以类似于一维数组的方式声明多维数组。除了第一个维度外的每个维度都用逗号标记：

```csharp
int[,] intMatrix;
float[,] floatMatrix;
string[,,] strCube;
```

在示例中我们创建了二维和三维数组。每个维度由方括号 `[]` 表示。我们通过使用 `new` 关键字为多维数组分配内存，并在括号中设置每个维度的长度：

```csharp
int[,] intMatrix = new int[3,4];
float[,] floatMatrix = new float[8,2];
string[,,] strCube = new string[5,5,5];
```

在这个示例中，`intMatrix` 是一个具有 3 个 `int` 类型元素的二维数组，这 3 个元素中的每个长度为 4。二维数组很容易理解，因此我们可以将其想象为具有行和列的二维矩阵：

| 0 | 1 | 2 | 3 |
|---|---|---|---|
| 0 | 1 | 3 | 6 |
| 1 | 8 | 5 | 9 |
| 2 | 4 | 7 | 3 |

矩阵的行和列用从 0 到 n-1 的索引编号。如果一个二维数组的大小为 m x n，则恰好有 $m*n$ 个元素。

## 二维数组初始化

我们以与一维数组相同的方式初始化二维数组。我们可以在声明后直接列出元素值：

```csharp
int[,] matrix =
{
  {1, 2, 3, 4}, // 第 0 行值
  {5, 6, 7, 8}, // 第 1 行值
}
// 矩阵大小为 2 x 4 (2行，4列)
```

在上面的示例中，我们初始化了一个大小为 2 行 4 列的整数二维数组。在外部括号中，我们放置第一个维度的元素，即数组的行。每行包含一个一维数组，我们知道如何初始化它。

## 访问多维数组元素

矩阵有两个维度，我们分别使用两个索引访问每个元素：一个用于行，一个用于列。多维数组每个维度都有不同的索引。

> 多维数组中的每个维度都从索引 0 开始。

让我们查看下一个示例：

```csharp
int[,] matrix =
{
  {1, 2, 3, 4},
  {5, 6, 7, 8},
}
```

数组 `matrix` 有 8 个元素，存储在 2 行 4 列中。可以通过以下方式访问每个元素：

| matrix[0, 0] | matrix[0, 1] | matrix[0, 2] | matrix[0, 3] |
| matrix[1, 0] | matrix[1, 1] | matrix[1, 2] | matrix[1, 3] |

在这个示例中，我们可以使用索引访问每个元素。如果将行的索引赋值给 `row`，将列的索引赋值给 `col`，那么就可以所示访问任何元素：

```csharp
matrix[row, col]
```

当我们使用多维数组时，每个元素都是唯一的，并且可以通过索引标识：

## 多维数组的长度

多维数组的每个维度都有自己的长度，我们可以通过 `GetLength` 方法获取。因此，在这种情况下，`GetLength(0)` 返回行数，`GetLength(1)` 返回列数。

## 打印矩阵——示例

在下一个示例中，我们展示如何通过 `foreach` 循环遍历数组并打印到控制台。我们先声明并初始化数组：

```csharp
int[,] matrix = {
    {1, 2, 3, 4},
    {5, 6, 7, 8}
};
foreach (int capital in matrix)
{
    Console.WriteLine(capital);
}
```

## 从控制台读取矩阵

在这个示例中，我们学习如何从控制台读取二维数组。首先，我们使用嵌套循环赋值每个维度的值：

```csharp
Console.Write("行数: ");
int rows = int.Parse(Console.ReadLine());
Console.Write("列数: ");
int cols = int.Parse(Console.ReadLine());
int[,] matrix = new int[rows, cols];
Console.WriteLine("矩阵单元:");
for (int row = 0; row < rows; row++) {
    for (int col = 0; col < cols; col++) {
        Console.Write("matrix[{0},{1}] = ", row, col);
        matrix[row, col] = int.Parse(Console.ReadLine());
    }
}
```
