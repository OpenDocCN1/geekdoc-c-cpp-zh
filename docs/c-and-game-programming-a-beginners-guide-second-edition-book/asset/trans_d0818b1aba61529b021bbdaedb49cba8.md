
就像标准数组可以初始化、传递并作为整个数组包含在函数内部一样，多维数组也可以。虽然外观略有不同，但它们遵循相同的规则并具有相同的基本限制。接下来的几个示例展示了这种类型的编码是如何实现的（参见示例 4.14）。

程序在示例 4.14 中接受一个包含六个名字且每个名字为五个字母的列表。这些值存储在多维数组（6x5）中。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_251_0.png)

### 示例 4.14. 二维数组。

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            string[,] names = new string[6, 5];

            for (int i = 0; i < 6; i++) {
                Console.WriteLine("Enter student's name "
                    + "(all names must include 5 letters): ");
                for (int j = 0; j < 5; j++) {
                    names[i, j] = Console.ReadLine();
                }
            }

            file(names);
        }

        static void file(string[,] tester) {
            for (int i = 0; i < 6; i++) {
                for (int j = 0; j < 5; j++)
                    Console.WriteLine(tester[i, j]);
            }
        }
    }
}
```

## 三维数组

代数使用笛卡尔坐标来绘制维度，例如 *x*、*y* 和 *z*。物理学使用字母 *i*、*j* 和 *k*，其含义完全相同（参见示例 4.15 和 4.16）。

### 示例 4.15. 绘制坐标 *x*、*y*、*z*。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_252_0.png)

### 示例 4.16. 绘制坐标 *i*、*j* 和 *k*。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_252_1.png)

大多数程序员使用 *i*、*j* 和 *k* 来引用数组的内存位置，以及表示嵌套循环、三维空间等。三维数组的值在编码术语上基本上相同，但数据的参考点却大不相同，如示例 4.17 所示。

### 示例 4.17. 三维数组值。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_252_2.png)

这个立方体向我们展示了值是如何从 0, 0, 0 布局到 3, 3, 2。我们可以分配参考点，使得 i 等于数组列表，j 是每个数组的第一个值，k 是为每个列表存储的最后一个值。

### 示例 4.18. 声明、初始化和传递三维数组。

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            char[,,] names = new char[4, 5, 6] {
                {
                    {'T', 'h', 'i', 's', ' ', 'i'},
                    {'s', ' ', 'a', ' ', 't', 'e'},
                    {'s', 't', ' ', ' ', 't', 'h'},
                    {'i', 's', ' ', 'i', 's', ' '},
                    {'o', 'n', 'l', 'y', ' ', 'a'},
                },
                {
                    {' ', 't', 'e', 's', 't', ' '},
                    {'\n', 'f', 'o', 'r', ' ', 't'},
                    {'h', 'e', ' ', '\n', 'e', 'x'},
                    {'t', ' ', 'm', 'i', 'n', 'u'},
                    {'t', 'e', ' ', 'y', 'o', 'u'},
                },
                {
                    {'r', ' ', 'c', 'o', 'm', 'p'},
                    {'u', 't', 'e', 'r', ' ', 'w'},
                    {'i', 'l', 'l', ' ', 'b', 'e'},
                    {' ', 'c', 'o', 'n', 'd', 'u'},
                    {'c', 't', 'i', 'n', 'g', '\n'},
                },
                {
                    {'a', ' ', 't', 'e', 's', 't'},
                    {' ', 'o', 'f', ' ', 't', 'h'},
                    {'e', ' ', 'm', 'u', 'l', 't'},
                    {'i', 'd', 'i', 'm', 'e', 'n'},
                    {'s', 'i', 'o', 'n', 'a', 'l'},
                },
            };
        }
    }
}

{
    {
        { ' ', 'a', 'b', 'c', 'd', 'e' },
        { 'f', 'g', 'h', 'i', 'j', 'k' },
        { 'l', 'm', 'n', 'o', 'p', 'q' },
        { 'r', 's', 't', 'u', 'v', 'w' },
        { 'x', 'y', 'z', ' ', ' ', ' ' }
    },
    {
        { 'A', ' ', 'T', 'E', 'S', 'T' },
        { '!', '\n', 'A', 'B', 'C', 'D' },
        { 'E', 'F', 'G', 'H', 'I', 'J' },
        { 'K', 'L', 'M', 'N', 'O', 'P' },
        { 'Q', 'R', 'S', 'T', 'U', 'V' }
    },
    {
        { 'W', 'X', 'Y', 'Z', 'a', 'b' },
        { 'c', 'd', 'e', 'f', 'g', 'h' },
        { 'i', 'j', 'k', 'l', 'm', 'n' },
        { 'o', 'p', 'q', 'r', 's', 't' },
        { 'u', 'v', 'w', 'x', 'y', 'z' }
    }
};

Display(names);
}

static void Display(char[,,] print) {
    const short sets = 3, rows = 5, columns = 6;
    for (int i = 0; i < sets; i++)
        for (int j = 0; j < rows; j++)
            for (int k = 0; k < columns; k++)
                Console.Write("{0}\\", print[i, j, k]);

    Console.WriteLine();
}
```

多维数组也认为是有锯齿的（没有恒定形状）或矩形/正方形（具有两个或更多边长相同的）。

## 排序数组

*排序*，与数组相关，是重新排列或重新组织元素的顺序以使特定任务更容易遵循的动作。这通常涉及某种逻辑参考点，例如字母按字母顺序排列，数字按数字顺序列出。用于置换这些值的主要方法涉及对该数据的比较和重新分配。用于排序这些值的技术范围从非常简单到复杂，但它们都做得差不多；因此，对替代技术的需求更多地与过程的速度有关，而非结果。其中最简单的一种被称为 *冒泡排序*（也称为 *下沉排序*）；值列在一个数组中，相互比较并根据需要交换，直到所有值都按正确顺序排列。单词 bubble 用于帮助可视化较小的（较轻的）值上升到顶部，而单词 sinking 用于可视化较大的（较重）值下沉到底部。该排序也非常直接——参见示例 4.19。

### 示例 4.19. 冒泡排序。

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            const short array_size = 12;
            int[] simple_array = new int[array_size] {
                31, 31, 54, 0, 60, 35, 34, 29, 18, 17, 13, 10};

            BubbleSort (simple_array, array_size);
        }

        static void BubbleSort (int[] my_array, short size) {
            int temp = 0;
            Console.WriteLine("\nRandom numbers inputted in this order");

            for (int i = 0; i < size; i++)
                Console.WriteLine("{0}  ", my_array[i]);
            for (int i = 0; i < size; i++)
                for (int j = 0; j < size-1; j++)
                    if (my_array[j] > my_array[j+1]) {
                        temp = my_array[j];
                        my_array[j] = my_array[j+1];
                        my_array[j+1] = temp;
                    }

            Console.WriteLine("\nsorting...\n" +
                "\nIn ascending order");
            for (int i = 0; i < size; i++)
                Console.WriteLine("  {0}", my_array[i]);

            Console.WriteLine("\nand in descending order");
            for (int i = size-1; i > -1; i--)
                Console.WriteLine("  {0}", my_array[i]);
        }
    }
}
```

## 搜索数组

有两种基本类型的搜索是有用的并且直接与存储在数组中的数据相关。第一种是 *线性搜索*，顾名思义，它是对每个元素进行连续比较，直到找到正确的信息为止。这是一种非常常见且特别有用的搜索算法，尤其是在处理随机或不相关的、无法排序的数据时。第二种，也被认为更高效的搜索，是 *二分搜索*。这种搜索将两个标准进行划分和比较，其中总值被分为两组，不相关的组被丢弃。该过程在回退到基本的线性搜索之前会重复尽可能多次。两种搜索都被认为有效，但在处理需要重复搜索的较长、可排序的数据流时，二分搜索更受青睐（参见示例 4.20 和 4.21）。二分搜索还要求数据预先排序；预先排序的数据也可以存储为二级文件，从而消除了持续重新排序的需求。

### 示例 4.20. 线性搜索（在数组中查找一个数字）。

```csharp
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            string input;
            const int array_size = 100;
