
这里，“Tuesday” 将存储在字符串类型变量 'today' 中。

### 示例

```csharp
// Illustration of array
using System;
namespace arrayconcept
{
    class Usingarray
    {
        static void Main()
        {
            int[] numbers; //declaration of array
            numbers = new int[6] { 100, 200, 300, 400, 500, 600 }; //creation and initialization of array
            Console.WriteLine("Numbers in the Array");
            for (int cnt = 0; cnt < 6; cnt++)
            {
                Console.WriteLine("\nNumber Element {0} of array = {1}", cnt + 1, numbers[cnt]);
                //accessing the array elements
            }
            Console.ReadLine();
        }
    }
}
```

输入 无

### 输出

数组中的数字
数组的第 1 个元素 = 100
数组的第 2 个元素 = 200
数组的第 3 个元素 = 300
数组的第 4 个元素 = 400
数组的第 5 个元素 = 500
数组的第 6 个元素 = 600

## 7.5 使用 foreach 循环访问数组元素

- foreach 循环语句可用于遍历数组。

### 示例

```csharp
//illustration of foreach loop for Array
using System;
namespace arrayconcept
{
    class ArrayUsingForEach
    {
        static void Main(string[] args)
        {
            int[] numbers = new int[5]; /*numbers is an array of 5 integers */
            /* initialization of array elements */
            for (int cnt = 0; cnt < 5; cnt++)
            {
                numbers[cnt] = cnt + 50;
            }

            int num;
            /* print each array element */
            Console.WriteLine("Array Elements ");
            foreach (num in numbers)
            {
                Console.WriteLine("{0}", num);
            }
            Console.WriteLine();
        }
    }
}
```

输入 无

### 输出

数组元素
50
51
52
53
54

## 6.1.2 数组类型

### 6.1.2.1 概念

在 C# 中有四种数组类型，如下所述。

| 数组类型 | 描述 |
|---|---|
| 一维数组 | 一个只包含一个维度的简单数组称为一维数组。 |
| 多维数组 | 包含一个以上维度的数组称为多维数组。多维数组最简单的形式是‘二维数组’。 |
| 锯齿数组 | Jagged array 是 "array of array"。 |
| 参数数组 | Param array 用于向方法传递未知数量的参数 |

### 6.1.2.2 一维数组

**概念**

仅包含一个维度（1 行）的数组称为一维数组。

**解释**

一维数组声明

```csharp
datatype[] arrayname
```

### 6.1.2.3 多维数组

**概念**

包含一个以上维度（多行多列）的数组称为多维数组。

**解释**

- 1. 在编程中，二维数组被广泛使用，它是多维数组最简单的形式。
- 2. 多维数组声明
- 3. 示例
- 4. 二维数组

```csharp
datatype[,] arrayname;//two-dimensional array
datatype[,,] arrayname;//three-dimensional array
```

```csharp
int[,] distances;// two dimensional array
string[,,] names;//three dimensional array
```

**概念**

二维数组是多维数组最简单的形式。具有两个维度（解释为 1 行和 1 列）的数组称为二维数组。

**解释**

- 3. 以下是大小为 (4*3) 的二维数组，表示 4 行 3 列的矩阵，其元素表示如下，

|  | 列0 | 列1 | 列2 | 列3 |  |
|---|---|---|---|---|---|
|  | Arr[0][0]=1 | Arr[0][1]=4 | Arr[0][2]=9 | Arr[0][3]=5 | 行0 |
|  | Arr[1][0]=4 | Arr[1][1]=4 | Arr[1][2]=1 | Arr[1][3]=2 | 行1 |
|  | Arr[2][0]=6 | Arr[2][1]=3 | Arr[2][2]=7 | Arr[2][3] | 行2 |

- 4. 二维数组中的每个元素表示为 arrayname[rowno][colno]。这里 rowno 和 colno 分别表示行和列的值。

- 5. 二维数组的初始化 :
  - 二维数组的初始化方式与一维数组相同，如下所示。

```csharp
int[,] matrix =
{
    {101, 102, 103, 104}, //row1 elements
    {105, 106, 107, 108}, //row2 elements
    {109, 110, 111, 112}  //row3 elements
};
//It is matrix of 3 rows and 4 columns
```

- 6. 访问二维数组的元素 :
  - 二维数组元素可以通过使用数组名称及其两个索引号、行索引和列索引来访问，如下所示。

位于第 2 行第 3 列位置存储的元素访问方式为 `matrix[1, 2]`

### 示例

```csharp
//illustration of 2-D array
using System;
namespace arrayconcept
{
    class Twodimensionalarray
    {
        static void Main()
        {
            int[,] squarematrix = new int[3, 3] { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
            //initialization of two dimensional array
            int row, col;
            for (row = 0; row < 3; row++)
            {
                for (col = 0; col < 3; col++)
                {
                    Console.WriteLine("\n squarematrix[{0},{1}] = {2}",
                        row, col, squarematrix[row, col]); //accessing 2-D array elements
                }

                Console.ReadLine();
            }
        }
    }
}
```

输入 无

### 输出

squarematrix[0,0] =1
squarematrix[0,1] =2
squarematrix[0,2] =3
squarematrix[1,0] =4
squarematrix[1,1] =5
squarematrix[1,2] =6
squarematrix[2,0] =7
squarematrix[2,1] =8
squarematrix[2,2] =9

### 6.1.2.4 锯齿数组

**概念**

- 1. 在 C# 中，Jagged array 是一种数组的数组，其中 jagged array 的每一行包含自己的数组，并且每个数组的长度可以不同。

**解释**

- 2. Jagged array 声明

```csharp
int[][] jaggedArray;
jaggedArray = new int[3][];
jaggedArray[0] = new int[4];
jaggedArray[1] = new int[2];
jaggedArray[2] = new int[5];
```

上述示例中 jaggedArray 包含 3 个数组，其中第一个数组有 4 个元素，第二个数组有 2 个元素，第三个数组有 5 个元素。

- 3. Jagged array 初始化

使用 jagged array 之前必须按如下方式初始化，

```csharp
int[][] JaggedArray = new int[3][]
{
    new int[] {2, 3, 5, 7},
    new int[] {4, 9},
    new int[] {1, 3, 5, 7, 9}
};
```

- 4. 访问 jagged array 的元素

jagged array 的元素使用数组名称及其索引按如下方式访问。

```csharp
JaggedArray[row][col];
```

### 示例

```csharp
//illustration of jagged array
using System;
namespace arrayconcept
{
    class jaggedarrays
    {
        static void Main()
        {
            // jagged array with 3 rows.
            int[][] jaggedNumbers = new int[3][];

            // Create a new array in the jagged array, and assign values to it.
            //set row 1
            jaggedNumbers[0] = new int[2];
            jaggedNumbers[0][0] = 1;
            jaggedNumbers[0][1] = 2;

            // set row 2, initialized to zero.
            jaggedNumbers[1] = new int[1];
            jaggedNumbers[1][0] = 3;

            // Set row 3, using array initializer.
            jaggedNumbers[2] = new int[] { 4, 5, 6 };

            // Access elements and Print all elements in the jagged array.
            for (int row = 0; row < jaggedNumbers.Length; row++)
            {
                int[] innerArray = jaggedNumbers[row]; //copying array reference
                Console.WriteLine("Inner Array {0} Elements ", row + 1);
                for (int index = 0; index < innerArray.Length; index++)
                {
                    Console.Write(innerArray[index] + " ");
                }
                Console.WriteLine();
            }
        }
    }
}
```

输入 无

### 输出

```csharp
Inner Array 1 Elements 1 2
Inner Array 2 Elements 3
Inner Array 3 Elements 4 5 6
```

### 6.1.2.5 参数数组

**概念**

在处理方法时，如果不确定方法的参数数量，则可以有效地使用 Param array。

**解释**

Param array 用于向方法传递未知数量的参数。

### 示例

```csharp
//illustration of param array
using System;
namespace arrayConcept
{
    class Paramarray
    {
        static int multiply(params int[] numbers)
        {
            int product = 1;
            foreach (int n in numbers)
            {
                product = product * n;
            }
            return product;
        }

        static void Main(string[] args)
        {
            int product;
            // passing 3 parameters
            product = Paramarray.multiply(2, 6, 8);
            Console.WriteLine("multiplication of 2,6,8 is {0}", product);

            // passing 5 parameters
            product = Paramarray.multiply(2, 4, 6, 8, 10);
            Console.WriteLine("Multiplication of 2,4,6,8,10 is {0}", product);
            Console.ReadLine();
        }
    }
}
```

输入 无

### 输出

2、6、8 的乘法结果是 96.
2、4、6、8、10 的乘法结果是 3840

## 6.1.3 将数组作为参数传递

**概念**

数组可以在 C# 中像其他参数一样传递给方法。

### 示例

```csharp
//illustration of array passed as parameter to a method
using System;
namespace arrayconcept
{
    class PassingarrayAsParameter
    {
        static void averagearrayelement(int[] avgarray)
        {
            int cnt, sum = 0;
            for (cnt = 0; cnt < 4; cnt++)
            {
                sum = sum + avgarray[cnt];
            }
            Console.WriteLine("Average of elements of array is {0}", sum / (avgarray.Length));
        }

        static void Main(string[] args)
        {
            int[] numbers = new int[4] { 11, 22, 33, 44 };
            //Passing array as parameter
            PassingarrayAsParameter.averagearrayelement(numbers);
            Console.ReadLine();
        }
    }
}
```

输入 无
