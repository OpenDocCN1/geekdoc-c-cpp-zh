
```csharp
// output each array element's value
for (int counter = 0; counter < array.Length; ++counter)
{
    Console.WriteLine($"{counter,5}{array[counter],8}");
}
```

| 索引 | 值 |
|---:|---:|
| 0 | 2 |
| 1 | 4 |
| 2 | 6 |
| 3 | 8 |
| 4 | 10 |

**图 8.4** | 计算要放入数组元素中的值。（第 2 部分之 2。）

### 使用 `const` 声明命名常量

第 9 行使用修饰符 const 声明常量 ArrayLength，其初始化为 5。常量必须在其声明中初始化，之后不能再修改。常量使用与类、方法和属性相同的 Pascal 大小写命名约定。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_237_0.png)

> **良好的编程实践 8.1**
> 
> 常量也称为命名常量。使用常量的应用程序通常比使用字面值（例如，5）的应用程序更易于阅读——例如，命名常量 ArrayLength 清楚地表明了其用途，而字面值 5 根据其使用的上下文可能具有不同的含义。使用命名常量的另一个优点是，如果必须更改常量的值，则只需在声明中进行更改，从而降低代码维护成本。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_237_1.png)

> **良好的编程实践 8.2**
> 
> 将数组的大小定义为命名常量而不是字面值可以使代码更清晰。这种技术称为符号命名，常用。例如，在处理包含五个元素的数组的数组处理代码中反复提及大小 5 会使数字 5 具有人为的重要性，并且当程序包含与数组大小无关的其他 5 时会令人困惑。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_237_2.png)

> **常见的编程错误 8.2**
> 
> 在命名常量初始化后为其赋值是编译错误。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_237_3.png)

> **常见的编程错误 8.3**
> 
> 尝试在未初始化的情况下声明命名常量是编译错误。

### 8.4.4 对数组元素求和

通常，数组的元素代表一系列用于计算的值。例如，如果数组的元素代表考试成绩，教师可能希望对元素求和，然后使用该和来计算班级平均分。本章后面的 GradeBook 示例（第 8.8 节和第 8.10 节）使用了这种技术。图 8.5 对包含在 10 个元素的 int 数组中的值求和，该数组在第 9 行声明并初始化。for 语句通过将每个元素的值加到总计中来执行计算（第 15 行）。³

```csharp
// Fig. 8.5: SumArray.cs
// Computing the sum of the elements of an array.
using System;

class SumArray
{
   static void Main()
   {
      int[] array = { 87, 68, 94, 100, 83, 78, 85, 91, 76, 87 };
      int total = 0;

      // add each element's value to total
      for (int counter = 0; counter < array.Length; ++counter)
      {
         total += array[counter]; // add element value to total
      }

      Console.WriteLine($"Total of array elements: {total}");
   }
}
```

```
Total of array elements: 849
```

**图 8.5** | 计算数组元素的总和。

### 8.4.5 使用 foreach 遍历数组

到目前为止，我们使用计数控制的 for 语句遍历数组元素。在本节中，我们介绍 foreach 语句，它遍历整个数组的元素（或集合的元素，如第 9.4 节中所述）。foreach 语句的语法是

```
foreach (type identifier in arrayName)
{
   statement
}
```

其中 *类型* 和 *标识符* 是迭代变量的类型和名称（例如 int number），而 *arrayName* 是要遍历的数组。迭代变量的类型必须与数组的元素类型一致。迭代变量在 foreach 语句的连续迭代中代表数组中的连续值。

图 8.6 使用 foreach 语句（第 13–16 行）计算数组元素的总和。迭代变量 number 的类型在第 13 行声明为 int，因为 array 包含 int 值。foreach 语句一次迭代一个地遍历 array 中的连续 int 值，从第一个元素开始。foreach 头可以简洁地读作“每次迭代，将数组的下一个元素赋给 int 变量 number，然后执行以下语句。”第 13–16 行等价于图 8.5 中第 13–16 行使用的计数控制迭代。

> **常见的编程错误 8.4**
> 
> 在 foreach 语句的主体中尝试更改迭代变量的值会导致编译错误。

```csharp
1 // Fig. 8.6: ForEachTest.cs
2 // Using the foreach statement to total integers in an array.
3 using System;
4
5 class ForEachTest
6 {
7     static void Main()
8     {
9         int[] array = {87, 68, 94, 100, 83, 78, 85, 91, 76, 87};
10         int total = 0;
11
12         // add each element's value to total
13         foreach (int number in array)
14         {
15             total += number;
16         }
17
18         Console.WriteLine($"Total of array elements: {total}");
19     }
20 }
```

```
Total of array elements: 849
```

图 8.6 | 使用 foreach 语句对数组中的整数求和。

### foreach 与 for

只要遍历数组的代码不需要访问当前数组元素的索引，就可以使用 foreach 语句代替 for 语句。例如，对数组中的整数求和只需要访问元素值——每个元素的索引无关紧要。如果应用程序出于除简单遍历数组之外的其他原因必须使用计数器（例如，根据计数器的值计算元素的值，如图 8.4 所示），则应使用 for 语句。

> **常见的编程错误 8.5**
> 
> 尝试使用 foreach 语句的迭代变量修改数组元素的值是逻辑错误——迭代变量只能用于访问每个数组元素的值，而不能修改它。

### 8.4.6 使用条形图以图形方式显示数组数据；介绍使用 var 进行类型推断

许多应用程序以图形方式向用户呈现数据。例如，数值通常以条形图中的条形显示。在这样的图表中，更长的条形代表成比例更大的数值。以图形方式显示数值数据的一种简单方法是使用条形图，其中每个数值显示为星号 (*) 的条形。

教师可能会绘制每个类别中的成绩数量，以可视化考试的成绩分布。假设一次考试的成绩为 87、68、94、100、83、78、85、91、76 和 87。其中有一个 100 分，两分在 90 分段，四分在 80 分段，两分在 70 分段，一分在 60 分段，没有低于 60 分的成绩。我们的下一个应用程序（图 8.7）将此成绩分布数据存储在包含 11 个元素的数组中，每个元素对应一个成绩类别。例如，array[0] 表示 0-9 范围内的成绩数量，array[7] 表示 70-79 范围内的成绩数量，array[10] 表示 100 分的成绩数量。第 8.8 节和第 8.10 节中类 GradeBook 的两个版本包含基于一组成绩计算这些成绩频率的代码。目前，我们手动创建数组并用每个范围内的成绩数量对其进行初始化（图 8.7，第 9 行）。我们在介绍应用程序的逻辑后讨论关键字 var（第 14 行和第 27 行）。

```csharp
1  // Fig. 8.7: BarChart.cs
2  // Bar chart displaying app.
3  using System;
4  
5  class BarChart
6  {
7      static void Main()
8      {
9          int[] array = {0, 0, 0, 0, 0, 0, 1, 2, 4, 2, 1}; // distribution
10 
11         Console.WriteLine("Grade distribution:");
12 
13         // for each array element, output a bar of the chart
14         for (var counter = 0; counter < array.Length; ++counter)
15         {
16             // output bar labels ("00-09: ", ..., "90-99: ", "100: ")
17             if (counter == 10)
18             {
19                 Console.Write("  100: ");
20             }
21             else
22             {
23                 Console.Write($"{counter * 10:D2}-{counter * 10 + 9:D2}: ");
24             }
25 
26             // display bar of asterisks
27             for (var stars = 0; stars < array[counter]; ++stars)
28             {
29                 Console.Write("*");
30             }
        }
```
