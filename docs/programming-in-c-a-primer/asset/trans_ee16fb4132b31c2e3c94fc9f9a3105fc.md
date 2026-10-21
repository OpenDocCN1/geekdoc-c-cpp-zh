

考虑下面所示的另一个示例：

```csharp
for (int x = 0; x < 10; x++)
    average[x] = (float)x;
```

此循环将数组 average 初始化为 0.0 到 9.0 的值。程序 9.1 说明了使用数组对数字列表进行排序。

## 程序 9.1 | 对数字列表进行排序

```csharp
using System;
class NumberSorting
{
	public static void Main( )
	{
		int[] number = { 55, 40, 80, 65, 71 };
		int n = number.Length;
		Console.Write("Given list : ");
		for (int i = 0; i < n; i++)
		{
			Console.Write(" " + number[i]);
		}
		Console.WriteLine("\n");
		// Sorting begins
		for (int i = 0; i < n; i++)
		{
			for (int j = i+1; j < n; j++)
			{
				if(number[i] < number[j])
				{
					// Interchange values
					int temp = number[i];
					number[i] = number[j];
					number[j] = temp;
				}
			}
		}
		Console.Write("Sorted list : ");
		for (int i = 0; i < n; i++)
		{
			Console.Write(" " + number[i]);
		}
		Console.WriteLine(" ");
	}
}
```

程序 9.1 显示以下输出：

```text
Given list : 55 40 80 65 71

Sorted list : 80 71 65 55 40
```

## 9.4 二维数组

到目前为止，我们讨论了可以存储值列表的数组变量。在某些情况下，需要存储值表。考虑以下数据表，显示了四名销售员销售三种商品的销售额：

|            | Item1 | Item2 | Item3 |
|------------|-------|-------|-------|
| Salesgirl #1 | 310 | 275 | 365 |
| Salesgirl #2 | 210 | 190 | 325 |
| Salesgirl #3 | 405 | 235 | 240 |
| Salesgirl #4 | 260 | 300 | 380 |

该表包含总共十二个值，每行三个。我们可以将此表视为由四行三列组成的矩阵。每行代表特定销售员的销售额，每列代表特定商品的销售额。

在数学中，我们使用两个下标来表示矩阵中的特定值，例如 v_ij。这里 v 表示整个矩阵，v_ij 指第 i 行第 j 列的值。例如，在上表中 v_23 指值 325。C# 允许我们使用二维数组定义此类项目表。上面讨论的表可以在 C# 中表示为 v[4,3]

二维数组在内存中存储如图所示 9.2 所示。与一维数组一样，数组的每个维度从零索引到其最大大小减一；第一个索引选择行，第二个索引在该行内选择列。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_167_0.png)

图 9.2 内存中二维数组的表示

创建二维数组时，我们必须遵循与简单数组相同的步骤。我们可以像这样创建一个二维数组：

```csharp
int[,] myArray;
myArray = new int[3,4];
```

或

```csharp
int[,] myArray = new int[3,4];
```

这创建了一个可以存储十二个整数值的表，四列三行。

与一维数组一样，二维数组也可以通过在其声明后跟随用大括号括起的初始值列表来初始化。例如，

```csharp
int[,] table ={{0,0,0},{1,1,1}};
```

将第一行的元素初始化为零，第二行的元素初始化为一。初始化按行进行。我们也可以以矩阵的形式初始化二维数组，如下所示：

```csharp
int[,] table = {
    {0,0,0},
    {1,1,1}
};
```

注意上面语句的语法。除了最后一行外，每个关闭行的括号后都需要逗号。

我们可以通过使用对应元素的列和行的下标来引用二维数组中存储的值。例如：

```csharp
int value = table[1,2];
```

这检索表矩阵中第二行第三列存储的值。

初始化二维数组的快速方法是使用嵌套 for 循环，如下所示：

```csharp
for (i = 0; i < 5; i++)
{
    for (j = 0; j < 5; j++)
    {
        if (i == j)
            table[i,j] = 1;
        else
            table[i,j] = 0;
    }
}
```

这将所有对角线元素设置为 1，其余设置为零，如下所示：

|   |   |   |   |   |
|---|---|---|---|---|
| 1 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 | 0 |
| 0 | 0 | 0 | 1 | 0 |
| 0 | 0 | 0 | 0 | 1 |

程序 9.2 说明了在现实生活情况下使用二维数组。

## 程序 9.2 二维数组的应用

```csharp
using System;
class MulTable
{
    static int ROWS = 20;
    static int COLUMNS = 20;

    public static void Main()
    {
        int[,] product = new int[ROWS,COLUMNS];

        Console.WriteLine("MULTIPLICATION TABLE");
        Console.WriteLine(" ");
        int i,j;
        for (i = 10; i < ROWS; i++)
        {
            for (j = 10; j < COLUMNS; j++)
            {
                product[i,j] = i*j;
                Console.Write("  "+product[i,j]);
            }
            Console.WriteLine(" ");
        }
    }
}
```

程序 9.2 产生以下输出：

MULTIPLICATION TABLE

|    |    |    |    |    |    |    |    |    |    |
|---|---|---|---|---|---|---|---|---|---|
| 100 | 110 | 120 | 130 | 140 | 150 | 160 | 170 | 180 | 190 |
| 110 | 121 | 132 | 143 | 154 | 165 | 176 | 187 | 198 | 209 |
| 120 | 132 | 144 | 156 | 168 | 180 | 192 | 204 | 216 | 228 |
| 130 | 143 | 156 | 169 | 182 | 195 | 208 | 221 | 234 | 247 |
| 140 | 154 | 168 | 182 | 196 | 210 | 224 | 238 | 252 | 266 |
| 150 | 165 | 180 | 195 | 210 | 225 | 240 | 255 | 270 | 285 |
| 160 | 176 | 192 | 208 | 224 | 240 | 256 | 272 | 288 | 304 |
| 170 | 187 | 204 | 221 | 238 | 255 | 272 | 289 | 306 | 323 |
| 180 | 198 | 216 | 234 | 252 | 270 | 288 | 306 | 324 | 342 |
| 190 | 209 | 228 | 247 | 266 | 285 | 304 | 323 | 342 | 361 |

## 9.5 变长数组

C# 将多维数组视为“数组的数组”。可以按如下方式声明二维数组：

```csharp
int[] [] x = new int[3][];    //three rows array
x[0] = new int[2];            //first row has two elements
x[1] = new int[4];            //second row has four elements
x[2] = new int[3];            //third row has three elements
```

这些语句创建了一个二维数组，每个行的长度不同，如图 9.3 所示。变长数组称为锯齿数组。

元素可以按如下方式访问：

```csharp
x[1][1] = 10;
int y = x[2][2];
```

注意我们访问这两种数组的方式的差异。对于矩形数组，所有索引都在一组方括号内，而对于锯齿数组，每个元素都在自己的方括号内。

![](img/bae4ee2c7c29c052feb3b9a9c5659998_169_0.png)

## 9.6 SYSTEM.ARRAY 类

在 C# 中，我们创建的每个数组都自动派生自 System.Array 类。该类定义了许多方法和属性，可用于更有效地操作数组。表 9.1 列出了一些常用的方法和其用途。

### 表 9.1 System.Array 类的一些常用方法

| METHOD/PROPERTY | PURPOSE |
|---|---|
| Clear () | Sets a range of elements to empty values |
| CopyTo () | Copies elements from the source array into the destination array |
| GetLength () | Gives the number of elements in a given dimension of the array |
| GetValue () | Gets the value for a given index in the array |
| Length | Gives the length of an array |
| SetValue () | Sets the value for a given index in the array |
| Reverse () | Reverses the contents of a one-dimensional array |
| Sort () | Sorts the elements in a one-dimensional array |

程序 9.3 说明了 Sort () 和 Reverse () 方法的实现。

## 程序 9.3 对数组进行排序和反转

```csharp
using System;
class SortReverse
{
    public static void Main()
    {
        //creating an array
        int [] x = { 30, 10, 80, 90, 20 };
        Console.WriteLine ("Array before sorting");
        foreach (int i in x)
            Console.Write(" " + i );
        Console.WriteLine ();
        //Sorting and reversing the array elements
        Array.Sort(x); Array.Reverse (x);
        Console.WriteLine("Array after Sorting and Reversing");
        foreach ( int i in x )
            Console.Write(" " + i);
        Console.WriteLine ();
    }
}
```

程序 9.3 的输出：

```text
Array before sorting
30 10 80 90 20
Array after Sorting and Reversing
90 80 30 20 10
```
