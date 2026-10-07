
C# 还允许将 `new` 关键字作为声明语句的一部分，因此它允许了如列表 3.10 所示的赋值和声明。

## 列表 3.10：声明期间使用 new 进行数组赋值

```csharp
string[] languages = new string[]{
  "C#", "COBOL", "Java",
  "C++", "Typescript", "Visual Basic",
  "Python", "Lisp", "JavaScript" };
```

使用 `new` 关键字允许运行时为该数据类型分配内存。它指示运行时实例化该数据类型——在本例中是一个数组。

每当你将 `new` 关键字作为数组赋值的一部分时，你也可以方括号内指定数组的大小。列表 3.11 展示了这种语法。

## 列表 3.11：使用 new 关键字进行声明和赋值

```csharp
string[] languages = new string[9]{
  "C#", "COBOL", "Java",
  "C++", "Typescript", "Visual Basic",
  "Python", "Lisp", "JavaScript" };
```

初始化语句中的数组大小与大括号内包含的元素数量必须匹配。此外，可以赋值数组但不指定数组的初始值，如列表 3.12 所示。

## 列表 3.12：不带字面值的赋值

```csharp
string[] languages = new string[9];
```

赋值数组但不初始化初始值仍然会初始化每个元素。运行时将数组元素初始化为它们的默认值，如下：

- 引用类型——无论为空（例如 `string` 和 `string?`）都初始化为 `null`。
- 可空值类型均初始化为 `null`。
- 不可空数值类型初始化为 `0`。
- `bool` 被初始化为 `false`。

## 第 3 章：数据类型的进阶

- `char` 被初始化为 `'\0'`。

非原始值类型通过将它们的每个字段初始化为相应的默认值来递归地进行初始化。因此，在使用数组之前，没有必要单独为每个元素赋值。

由于数组大小没有被包含在变量声明中，因此可以在运行时指定大小。例如，列表 3.13 根据 `Console.ReadLine()` 调用中指定的尺寸创建一个数组。

## 列表 3.13：在运行时定义数组大小

```csharp
string[] groceryList;
Console.Write("How many items on the list? ");
int size = int.Parse(Console.ReadLine());
groceryList = new string[size];
//...
```

C# 初始化多维数组的方式类似。用逗号分隔每一维的大小。列表 3.14 初始化了一个没有任何步棋的井棋盘。

## 列表 3.14：声明一个二维数组

```csharp
int[,] cells = new int[3,3];
```

如列表 3.15 所示，可以带特定位置初始化井棋盘。

## 列表 3.15：初始化一个整数二维数组

```csharp
int[,] cells = {
  {1, 0, 2},
  {1, 2, 0},
  {1, 2, 1}
};
```

初始化遵循这种模式：存在一个包含三个 `int[]` 类型元素的数组，且每个元素具有相同的大小；在本示例中，大小为 3。注意，每个 `int[]` 元素的大小必须完全相同。因此，列表 3.16 所示的声明是无效的。

## 列表 3.16：大小不一致导致错误的多维数组

```csharp
// ERROR: 每个维度的大小必须保持一致
//...
```

表示井棋并不需要在每个位置都使用整数。另一种方法是为每个玩家构建一个单独虚拟棋板，每个棋板包含一个 `bool`，用于指示玩家选择了哪些位置。列表 3.17

## 列表 3.17：初始化一个三维数组

```csharp
bool[,, ] cells;
cells = new bool[2, 3, 3];
{
  // 玩家1 移动
  // X | |
  //---++-
  // X | |
  //---++-
  // X | X
  {
    {true, false, false},
    {true, false, false},
    {true, false, true}
  },
  // 玩家2 移动
  // | 0 |
  // |--+-
  // | 0 |
  // |--+-
  // | 0 |
  {
    {false, false, true},
    {false, true, false},
    {false, true, true}
  }
};
```

在此示例中，棋板被初始化，且每一维的大小被显式识别。除了作为 `new` 表达式的一部分标识大小外，还提供了数组的字面值。`bool[,,]` 类型的字面值被拆分为两个大小为 3 × 3 的 `bool[]` 数组。每个二维数组由三个大小为 3 的 `bool` 数组组成。

如所述，多维数组中的每个维度的大小必须保持一致。然而，也可以定义交错数组（jagged array），即数组的数组。交错数组的语法与多维数组显著不同；此外，交错数组不需要大小一致。

## 列表 3.18：初始化交错数组

```csharp
int[][] cells = {
    new int[] {1, 2, 3},
    new int[] {4, 5, 6},
    new int[] {7, 8, 9}
};
```

由于数组大小没有包含在变量声明中，因此可以在运行时指定大小。例如，列表 3.13 根据 `Console.ReadLine()` 调用中指定的尺寸创建一个数组。C# 初始化多维数组的方式类似。用逗号分隔每一维的大小。列表 3.14 初始化了一个没有任何步棋的井棋盘。

## 列表 3.19：声明和访问数组

```csharp
string[] languages = new[]{
  "C#", "COBOL", "Java",
  "C++", "Typescript", "Visual Basic",
  "Python", "Lisp", "JavaScript"
};
// 获取 languages 中的第五个元素 (TypeScript)
string language = languages[4];
// 输出 "TypeScript"
Console.WriteLine(language);

// 获取从后数三个元素 (Python)
language = languages[^3];
// 输出 "Python"
Console.WriteLine(language);
```

从 C# 8.0 开始，你还可以使用**索引索引运算符**（index from end operator），也称为 `^`（帽子）运算符，相对于数组末尾访问项。例如，使用 `^1` 进行索引可以获取数组的最后一个项，而使用索引索引的第一个元素是 `^9`（其中 9 是数组中的项数）。在 3.19 中，`^3` 指定 `languages` 变量中从后数第三个项（"Python"）的值赋值给 `language`。

