
在方法作用域内被更改后，作为参数传入的原始变量的值也会随之更改。

ref 关键字用于声明引用参数。

**示例：**

```csharp
class Program
{
    void IncreaseNo(ref int no)
    {
        no++;
    }

    public static void Main()
    {
        Program p = new Program();
        int number = 2;
        p.IncreaseNo(ref number);
        Console.WriteLine(number);
    }
}
```

代码编译后，结果将为：

```text
3
```

### 输出参数

return 语句用于从方法返回值。使用 return 语句只能返回单个变量。输出参数正是为此目的而提供。

它们与引用参数类似，区别在于它们将数据传出方法。

**示例：**

```csharp
class Program
{
    void Demo(out int no)
    {
        no = 10;
    }

    public static void Main()
    {
        Program p = new Program();
        int number;
        p.Demo(out number);
        Console.WriteLine(number);
    }
}
```

代码编译后，结果将为：

```text
10
```

## 第 9 章 C# 中的数组

### 9.1 数组简介

数组是相同数据类型值的集合。数组中的变量称为数组元素。数组元素通过单个名称和表示元素在数组中位置的索引号来访问。

数组具有秩，它决定与每个数组元素关联的索引数量。数组的秩也称为数组的维度。下图展示了系统中的数组结构。

![](img/c133ae999967b1fbceab3bccc1cb1d4f_82_0.png)

### 9.2 数组声明

在任何程序中使用数组之前，必须先声明数组。以下语法用于声明数组。

```text
datatype[] ArrayName;
```

数组语法涉及以下组成部分：

- **datatype：** 用于指定元素的数据类型。该类型的数据将存储在数组中。
- **[]：** 指定数组的大小，并称为秩。
- **ArrayName：** 表示数组的名称。

### 9.3 初始化并添加值

**new** 关键字用于创建数组的实例。数组的大小在初始化时指定。以下代码片段用于初始化数组。

```text
int[] x;
x = new int[15];
```

可以通过合并这两条语句来初始化数组，写法如下：

```text
int[] x = new int[15];
```

**为数组赋值**

可以使用**索引号**为数组的每个元素赋值。索引号也称为元素的下标。以下代码片段用于为数组赋值。

```text
int[] amount = new int[5];
amount[0] = 50;
```

可以使用以下代码创建并初始化数组：

```text
int[] amount = { 40, 60, 70, 80 };
```

可以省略数组的大小。

```text
int[] age = new int[] { 21, 31, 40 };
```

当用户将数据从一个数组复制到另一个数组时，源数组和目标数组引用同一位置。以下代码片段展示了将一个数组复制到另一个数组。

```text
int[] age = new int[] { 12, 14, 15, 16 };
int[] amount = age;
```

创建了 **age** 和 **amount** 两个数组。它们指向同一内存位置。

### 9.4 访问数组元素

要访问数组中的元素，需要使用索引。索引是表示元素在数组中位置的数字。索引始终从零开始，因此要访问数组中的第一个元素，应采用以下格式：

`array_name[index]`

在这种情况下，索引的值为零。

**示例：**

**示例 28：**

```csharp
using System;
namespace arraydeclare
{
    class Arraydemo
    {
        static void Main(string[] args)
        {
            int[] a = new int[5];
            int x, y;

            for (x = 0; x < 5; x++)
            {
                a[x] = x + 10;
            }
            for (y = 0; y < 5; y++)
            {
                Console.WriteLine("Element [{0}] = {1}", y, a[y]);
            }
            Console.ReadLine();
        }
    }
}
```

**编译并执行代码后，输出为：**

- 元素 [0] = 10
- 元素 [1] = 11
- 元素 [2] = 12
- 元素 [3] = 13
- 元素 [4] = 14

### 9.5 foreach 循环

此循环专门设计用于遍历数组的所有元素。它非常适合高效地检索数组元素。

**语法：**

```text
foreach(type identifier in expression)
    statement – block
```

**示例：**

```csharp
using System;
namespace arraydeclare
{
    class Arraydemo
    {
        static void Main(string[] args)
        {
            int[] a = new int[5];

            for (int x = 0; x < 5; x++)
            {
                a[x] = x + 10;
            }
            foreach (int y in a)
            {
                int x = y - 10;
                Console.WriteLine("Element[{0}]={1}", x, y);
                x++;
            }
            Console.ReadLine();
        }
    }
}
```

代码编译并执行后，输出为：

```text
Element [0] = 10
Element [1] = 11
Element [2] = 12
Element [3] = 13
Element [4] = 14
```

### 9.6 不同类型的 C# 数组

以下是用于开发代码的各种类型的 C# 数组。

**多维数组**

多维数组将数据存储在**多个行维度**中。它也称为矩形数组。用户可以如下声明整数的二维数组：

```text
int[,] no;
```

二维数组可以视为表格。它有 x 行和 y 列。一个二维数组包含 2 行和 4 列。

|  | 列 0 | 列 1 | 列 2 | 列 3 |
|---|---|---|---|---|
| 行 0 | x[0][0] | x[0][1] | x[0][2] | x[0][3] |
| 行 1 | x[1][0] | x[1][1] | x[1][2] | x[1][3] |

**初始化二维数组**

以下数组有 3 行和 3 列。

```csharp
int[,] x = new int[3, 3] {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

**访问多维数组的元素**

可以使用下标访问多维数组中的元素。下标即数组的行索引和列索引。

**示例：**

```csharp
int output = a[1, 2];
```

在上述语句中，访问的是第二行第三列的元素。

**示例：**

```csharp
using System;
namespace twodimension
{
    class multiarray
    {
        static void Main(string[] args)
        {
            int[,] x = new int[3,2] {{1,1},{2,2},{3,3}};
            int a, b;

            for (a = 0; a < 3; a++)
            {
                for (b = 0; b < 2; b++)
                {
                    Console.WriteLine("x[{0},{1}]={2}", a, b, x[a,b]);
                }
            }
            Console.ReadLine();
        }
    }
}
```

代码编译并执行后，输出为：

- x[0,0] = 1
- x[0,1] = 1
- x[1,0] = 2
- x[1,1] = 2
- x[2,0] = 3
- x[2,1] = 3

**交错数组**

交错数组是数组的数组。int 类型的交错数组声明如下：

```csharp
int[][] marks;
```

数组可以按如下方式初始化：

```csharp
int[][] marks = new int[2][] { new int[] { 45, 57, 78 }, new int[] { 60, 75, 86, 45, 35 } };
```

marks 数组由两个整数数组组成：marks[0] 包含 3 个整数，marks[1] 包含 5 个整数。

**示例：**

**示例 3.1：**

```csharp
using System;
namespace Jaggedarray
{
    class jagged
    {
        static void Main(string[] args)
        {
            int[][] x = new int[][] {
                new int[] {0,0},
                new int[] {2,2},
                new int[] {3,4},
                new int[] {4,2},
                new int[] {1,3}};

            int a, b;

            for (a = 0; a < 5; a++)
            {
                for (b = 0; b < 2; b++)
                {
                    Console.WriteLine("x[{0},{1}]={2}", a, b, x[a][b]);
                }
            }
            Console.ReadLine();
        }
    }
}
```

代码编译并执行后，输出为：

```text
x[0,0] = 0
```

