

| 要 | 执行此操作 |
|---|---|
| 声明一个数组变量 | 写出元素类型的名称，后跟方括号，后跟变量的名称，后跟分号。例如：`bool[] flags;` |
| 创建一个数组的实例 | 写出关键字 *new*，后跟元素类型的名称，后跟方括号中括起来的数组大小。例如：`bool[] flags = new bool[10];` |
| 将数组的元素初始化为特定值 | 对于数组，将特定值写在花括号中用逗号分隔的列表中。例如：`bool[] flags = { true, false, true, false };` |
| 查找数组中的元素数量 | 使用 *Length* 属性。例如：`bool[] flags = ...;` `...` `int noOfElements = flags.Length;` |
| 访问单个数组元素 | 写出数组变量的名称，后跟方括号中括起来的元素的整数索引。请记住，数组索引从 0 开始，而不是 1。例如：`bool initialElement = flags[0];` |
| 遍历数组的元素 | 使用 *for* 语句或 *foreach* 语句。例如：`bool[] flags = { true, false, true, false };` `for (int i = 0; i < flags.Length; i++)` `{` `    Console.WriteLine(flags[i]);` `}` `foreach (bool flag in flags)` `{` `    Console.WriteLine(flag);` `}` |
| 声明一个多维数组变量 | 写出元素类型的名称，后跟一组用逗号分隔符表示维数数量的方括号，后跟变量的名称，后跟分号。例如，使用以下方法创建一个名为 *table* 的二维数组并将其初始化为容纳 4 行 6 列：`int[,] table;` `table = new int[4,6];` |
| 声明一个锯齿数组变量 | 将变量声明为子数组的数组。你可以初始化每个子数组使其长度不同。例如，使用以下方法创建一个名为 *items* 的锯齿数组并初始化每个子数组：`int[][] items;` `items = new int[4][];` `items[0] = new int[3];` `items[1] = new int[10];` `items[2] = new int[40];` `items[3] = new int[25];` |

## 第 11 章。理解参数数组

完成本章后，你将能够：

- 使用 *params* 关键字编写一个可以接受任意数量参数的方法。
- 使用 *params* 关键字结合 *object* 类型编写一个可以接受任意数量任意类型参数的方法。
- 解释接受参数数组的方法与接受可选参数的方法之间的区别。

如果您想要编写可以接受任意数量参数的方法，参数可能的类型也不同，参数数组就很有用。如果您熟悉面向对象概念，您可能会对上一句话感到沮丧。毕竟，面向对象的解决此问题的方法是定义重载方法。然而，重载并不总是最佳方法，特别是如果您需要创建一个方法，该方法可以接受真正可变数量的参数，并且每次调用方法时这些参数的类型都可能变化。本章将描述如何使用参数数组来解决此类情况。

### 重载——回顾

*Overloading* 是在同一作用域中声明两个或多个同名方法的技术术语。对方法进行重载对于您想要对不同类型的参数执行相同操作的情况非常有用。Microsoft Visual C# 中重载的经典示例是 *Console.WriteLine* 方法。该方法被重载多次，以便您可以传递任何原始类型参数。以下代码示例说明了 *Console* 类中 *WriteLine* 方法的某些定义方式：

Click here to view code image

```
class Console
{
    public static void WriteLine(Int32 value)
    public static void WriteLine(Double value)
    public static void WriteLine(Decimal value)
    public static void WriteLine(Boolean value)
    public static void WriteLine(String value)
    ...
}
```

### Note

*WriteLine* 方法的文档为其参数使用 *System* 命名空间中定义的构造类型，而不是这些类型的 C# 别名。例如，打印 *int* 值的重载实际上以 *Int32* 作为参数。请参阅 [第 9 章](Chapter 9)，“[使用枚举和结构创建值类型](Creating value types with enumerations and structures)”，以获取结构类型及其映射到 C# 别名的列表。

重载虽然很有用，但并不能涵盖所有情况。特别是，重载不易处理参数类型不变但参数数量变化的情况。例如，如果您想将多个值写入控制台，您是否必须提供可以接受各种组合的两个参数的 *Console.WriteLine* 版本，以及可以接受三个参数的其他版本，等等？这很快就会变得乏味。而且，这些重载方法的庞大重复会让您担心吗？应该会。幸运的是，有一种方法可以编写接受可变数量参数的方法（*variadic method*）：您可以使用参数数组，通过使用 *params* 关键字声明。

要了解 *params* 数组如何解决此问题，首先了解普通数组的使用和局限性会有所帮助。

### 使用数组参数

假设您想要编写一个方法来确定作为参数传递的值集中的最小值。一种方法是使用数组。例如，要找到几个 *int* 值中的最小值，您可以编写一个名为 *Min* 的静态方法，该方法有一个参数，表示 *int* 值数组：

[Click here to view code image](Click here to view code image)

```
class Util
{
    public static int Min(int[] paramList)
    {
        // Verify that the caller has provided at least one
parameter.
        // If not, throw an ArgumentException exception - it is not
possible
        // to find the smallest value in an empty list.
        if (paramList == null || paramList.Length == 0)
        {
            throw new ArgumentException("Util.Min: not enough
arguments");
        }

        // Set the current minimum value found in the list of
parameters to the first item
    int currentMin = paramList[0];

    // Iterate through the list of parameters, searching to see whether any of them
    // are smaller than the value held in currentMin
    foreach (int i in paramList)
    {
        // If the loop finds an item that is smaller than the value held in
        // currentMin, then set currentMin to this value
        if (i < currentMin)
        {
            currentMin = i;
        }
    }

    // At the end of the loop, currentMin holds the value of the smallest
    // item in the list of parameters, so return this value.
    return currentMin;
}
```

### Note

ArgumentException 类专门设计为在方法提供的参数不符合方法要求时抛出。

要使用 Min 方法查找名为 first 和 second 的两个 int 变量的最小值，您可以这样写：

```
int[] array = new int[2];
array[0] = first;
array[1] = second;
int min = Util.Min(array);
```

要使用 Min 方法查找三个 int 变量（名为 first、second 和 third）的最小值，您可以这样写：

```
int[] array = new int[3];
array[0] = first;
array[1] = second;
array[2] = third;
int min = Util.Min(array);
```

您可以看到此解决方案避免了大量重载的需求，但代价是：您必须编写额外的代码来填充传递的数组。当然，如果您愿意，也可以使用匿名数组，如下所示：

Click here to view code image

```
int min = Util.Min(new int[] {first, second, third});
```

然而，重点是您仍然需要创建和填充数组，而且语法可能会有点令人困惑。解决方案是使用 params 数组作为 Min 方法的参数，让编译器为您编写部分代码。

### 声明 params 数组

使用 params 数组，您可以向方法传递可变数量的参数。您通过在定义方法参数时使用 params 关键字作为数组参数修饰符来指示 params 数组。例如，这里是 Min 再次出现——这次其数组参数被声明为 params 数组：

Click here to view code image

```
class Util
{
    public static int Min(params int[] paramList)
    {
        // code exactly as before
    }
}
```

params 关键字对 Min 方法的影响是，它允许您使用任意数量的整数参数调用该方法，而无需担心创建数组。例如，要找到两个整数值的最小值，您只需这样写：

Click here to view code image

```
int min = Util.Min(first, second);
```

编译器将此调用转换为类似以下的代码：

```
int[] array = new int[2];
array[0] = first;
array[1] = second;
int min = Util.Min(array);
```

要找到三个整数值的最小值，您编写以下代码，编译器也将其转换为使用数组的相应代码：

Click here to view code image

```
int min = Util.Min(first, second, third);
```

对 Min 的两次调用（一次使用两个参数，另一次使用三个参数）都解析为同一个带有 params 关键字的 Min 方法。而且，正如您可能猜到的，您可以用任意数量的 int 参数调用此 Min 方法。编译器只需计算 int 参数的数量，创建 int

