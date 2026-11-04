
例如，下面的程序初始化一个名为 sqrs 的数组，其中包含数字 1 到 10 及其平方。

```csharp
// Initialize a two-dimensional array.
using System;

class Squares {
    static void Main() {
        int[,] sqrs = {
            { 1, 1 },
            { 2, 4 },
            { 3, 9 },
            { 4, 16 },
            { 5, 25 },
            { 6, 36 },
            { 7, 49 },
            { 8, 64 },
            { 9, 81 },
            { 10, 100 }
        };
        int i, j;

        for(i=0; i < 10; i++) {
            for(j=0; j < 2; j++) {
                Console.Write(sqrs[i,j] + " ");
            }
            Console.WriteLine();
        }
    }
}
```

以下是该程序的输出：

```
1 1
2 4
3 9
4 16
5 25
6 36
7 49
8 64
9 81
10 100
```

## 交错数组

在前面的示例中，创建二维数组时，你创建的是 C# 所称的矩形数组。如果把二维数组看作表格，那么矩形数组就是一种每一行的长度在整个数组中均相同的二维数组。然而，C# 还允许创建一种特殊类型的二维数组，称为交错数组。交错数组是数组的数组，其中每个数组的长度可以不同。因此，交错数组可用于创建各行长度不相同的表格。

交错数组通过使用多组方括号来声明，以表示每个维度。例如，要声明一个二维交错数组，可以使用以下一般形式：

```
type[][] array-name = new type[size][];
```

这里，size 表示数组中的行数。行本身尚未分配。相反，各行是单独分配的。这使得每一行的长度可以不同。例如，下面的代码在声明 jagged 时为其第一维分配内存。然后手动分配第二维。

```
int[][] jagged = new int[3][];
jagged[0] = new int[4];
jagged[1] = new int[3];
jagged[2] = new int[5];
```

执行这段代码后，jagged 看起来像这样：

![](img/7022d9b97326a713562c15aa43977d15_171_0.png)

很容易看出交错数组为什么叫这个名字！

创建交错数组后，访问元素时需要在各自的一组方括号中指定每个索引。例如，要将值 10 赋给 jagged 的元素 2, 1，可以使用以下语句：

```
jagged[2][1] = 10;
```

注意，这与访问矩形数组元素所用的语法不同。下面的程序演示了创建二维交错数组：

```csharp
// Demonstrate jagged arrays.
using System;
class Jagged {
  static void Main() {
    int[][] jagged = new int[3][];
    jagged[0] = new int[4];
    jagged[1] = new int[3];
    jagged[2] = new int[5];
    int i;
    // Store values in first array.
    for(i=0; i < 4; i++)
      jagged[0][i] = i;
    // Store values in second array.
    for(i=0; i < 3; i++)
      jagged[1][i] = i;
    // Store values in third array.
    for(i=0; i < 5; i++)
        jagged[2][i] = i;

    // Display values in first array.
    for(i=0; i < 4; i++)
        Console.Write(jagged[0][i] + " ");

    Console.WriteLine();

    // Display values in second array.
    for(i=0; i < 3; i++)
        Console.Write(jagged[1][i] + " ");

    Console.WriteLine();

    // Display values in third array.
    for(i=0; i < 5; i++)
        Console.Write(jagged[2][i] + " ");

    Console.WriteLine();
  }
}
```

输出如下：

0 1 2 3
0 1 2
0 1 2 3 4

并非所有应用程序都会使用交错数组，但在某些情况下它们可能很有效。例如，如果你需要一个非常大的、稀疏填充的二维数组（即并非所有元素都会被使用），那么交错数组可能是一个完美的解决方案。

最后一点：由于交错数组是数组的数组，因此并不要求这些数组必须是一维的。例如，下面的代码创建一个由二维数组组成的数组：

```
int[][,] jagged = new int[3][,];
```

下一条语句将一个 4x2 数组的引用赋给 jagged[0]：

```
jagged[0] = new int[4, 2];
```

下面的语句将值赋给 jagged[0][1,0]：

```
jagged[0][1,0] = i;
```

## 赋值数组引用

与其他对象一样，当你将一个数组引用变量赋给另一个变量时，只是让两个变量都引用同一个数组。你既不会导致创建数组的副本，也不会导致将一个数组的内容复制到另一个数组。例如，考虑下面的程序：

```csharp
// Assigning array reference variables.
using System;

class AssignRef {
    static void Main() {
        int i;

        int[] nums1 = new int[10];
        int[] nums2 = new int[10];

        for(i=0; i < 10; i++) nums1[i] = i;

        for(i=0; i < 10; i++) nums2[i] = -i;

        Console.Write("Here is nums1: ");
        for(i=0; i < 10; i++)
            Console.Write(nums1[i] + " ");
        Console.WriteLine();

        Console.Write("Here is nums2: ");
        for(i=0; i < 10; i++)
            Console.Write(nums2[i] + " ");
        Console.WriteLine();

        nums2 = nums1; // now nums2 refers to nums1

        Console.Write("Here is nums2 after assignment: ");
        for(i=0; i < 10; i++)
            Console.Write(nums2[i] + " ");
        Console.WriteLine();

        // Next, operate on nums1 array through nums2.
        nums2[3] = 99;

        Console.Write("Here is nums1 after change through nums2: ");
        for(i=0; i < 10; i++)
            Console.Write(nums1[i] + " ");
        Console.WriteLine();
    }
}
```

该程序的输出如下：

```
Here is nums1: 0 1 2 3 4 5 6 7 8 9
Here is nums2: 0 -1 -2 -3 -4 -5 -6 -7 -8 -9
Here is nums2 after assignment: 0 1 2 3 4 5 6 7 8 9
Here is nums1 after change through nums2: 0 1 2 99 4 5 6 7 8 9
```

如输出所示，在将 nums1 赋给 nums2 后，两个数组引用变量都引用同一个对象。

## 使用 Length 属性

C# 将数组实现为对象，这带来了许多好处。其中之一是每个数组都关联一个 Length 属性，该属性包含数组可以容纳的元素数。因此，每个数组都提供了一种确定其长度的方式。下面是一个演示该属性的程序：

```csharp
// Use the Length array property.
using System;

class LengthDemo {
    static void Main() {
        int[] nums = new int[10];
        Console.WriteLine("Length of nums is " + nums.Length);
        // Use Length to initialize nums.
        for(int i=0; i < nums.Length; i++)
            nums[i] = i * i;
        // Now use Length to display nums.
        Console.Write("Here is nums: ");
        for(int i=0; i < nums.Length; i++)
            Console.Write(nums[i] + " ");
        Console.WriteLine();
    }
}
```

该程序显示以下输出：

Length of nums is 10
Here is nums: 0 1 4 9 16 25 36 49 64 81

在 LengthDemo 中，注意 for 循环如何使用 nums.Length 来控制执行的迭代次数。由于每个数组都带有自己的长度，你可以使用这一信息，而不必手动跟踪数组的大小。请记住，Length 的值与实际使用的元素数无关。Length 包含数组能够容纳的元素数。获取多维数组的长度时，返回的是该数组能够容纳的元素总数。例如：

```csharp
// Use the Length array property on a 3D array.
using System;

class LengthDemo3D {
    static void Main() {
        int[,] nums = new int[10, 5, 6];
        Console.WriteLine("Length of nums is " + nums.Length);
    }
}
```

输出如下：

```
Length of nums is 300
```

如输出所验证，Length 获取的是 nums 可以容纳的元素数，在本例中为 300（10×5×6）。无法使用 Length 获取某个特定维度的长度。

包含 Length 属性简化了许多算法，使某些类型的数组操作更易于执行，也更安全。例如，下面的程序使用 Length 将一个数组的内容从后向前复制到另一个数组中，从而反转其内容：

```csharp
// Reverse an array.

using System;

class RevCopy {
  static void Main() {
    int i, j;
    int[] nums1 = new int[10];
    int[] nums2 = new int[10];

    for(i=0; i < nums1.Length; i++) nums1[i] = i;

    Console.Write("Original contents: ");
    for(i=0; i < nums2.Length; i++)
      Console.Write(nums1[i] + " ");

    Console.WriteLine();

    // Reverse copy nums1 to nums2.
    if(nums2.Length >= nums1.Length) // make sure nums2 is long enough
      for(i=0, j=nums1.Length-1; i < nums1.Length; i++, j--)
        nums2[j] = nums1[i];

    Console.Write("Reversed contents: ");
    for(i=0; i < nums2.Length; i++)
      Console.Write(nums2[i] + " ");

    Console.WriteLine();
  }
}
```

输出如下：

```
Original contents: 0 1 2 3 4 5 6 7 8 9
Reversed contents: 9 8 7 6 5 4 3 2 1 0
```

在这里，Length 有助于执行两个重要功能。首先，它用于确认目标数组足够大，能够容纳源数组的内容。其次，它提供执行反向复制的 for 循环的终止条件。当然，在这个简单示例中，数组的大小很容易知道，但同样的方法可以应用于各种更具挑战性的情况。
