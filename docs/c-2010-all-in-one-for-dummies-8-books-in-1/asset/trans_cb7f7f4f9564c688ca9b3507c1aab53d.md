

# 遍历数组的循环 115

名为 `Length` 的属性包含数组的长度。`doublesArray.Length` 的值与 `numElements` 相同。

以下 `for` 循环更为佳：

```csharp
// 将值累加到数组中。
for (int i = 0; i < doublesArray.Length; i++) ...
```

# 初始化数组

以下几行显示了一个带有初始化器的数组，以及另一个分配了空间但未初始化元素值的数组：

```csharp
double[] fixedLengthArray = {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
double[] array = new double[10];
```

你可以使用以下代码来实现它：

```csharp
double[] fixedLengthArray = new double[10] {5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3};
```

在这里，你专门分配了新内存 `new`，并为数组成员声明了初始值。我想我可以预测出你偏好哪种形式。（提示：第1行？）

# 遍历数组的循环

给定一个字符串数组，以下循环计算其长度的平均值：

```csharp
public class Student // 在书二中阅读类的章节。
{
    public string name; // 学分点平均
    public double gpa;
}
public class Program
{
    public static void Main(string[] args)
    {
        // . 以某种方式创建数组 . .
        // 现在计算你所拥有的学生的平均值。
        double sum = 0.0;
        for (int i = 0; i < students.Length; i++)
        {
            sum += students[i].gpa;
            double avg = sum / students.Length;
            // . 对平均值进行某些操作 . .
        }
    }
}
```

`for` 循环遍历数组的成员。（是的，你可以拥有任何类型对象的数组，而不像 `double` 和 `string` 这样的简单类型。你可能还没有被正式介绍过类，所以请再多等我一下。我会在下一书中介绍它们。）

# 116 数据数组排序

`students.Length` 包含数组中元素的数量。

C# 提供了另一种循环，名为 `foreach`，专门为遍历像数组这样的集合而设计。它的工作方式如下：

```csharp
// 现在计算你所拥有的学生的平均值。
double sum = 0.0;
foreach (Student student in students)
{
    sum += student.gpa; // 这提取当前学生的 GPA。
    double avg = sum / students.Length;
}
```

循环第一次通过时，`foreach` 从数组中获取第一个 `Student` 对象并将其存储在变量 `student` 中。在随后的每次迭代中，`foreach` 获取下一个元素。当数组中的元素处理完毕后，控制权将传出。

注意，`foreach` 语句中没有出现索引。索引的缺失大大减少了错误的概率，并且比 `for` 语句更简单，尽管有时索引很方便，你可能更倾向于使用 `for` 循环。

`foreach` 循环比看起来要强大得多。该语句适用于数组之外的其他集合类型。此外，`foreach` 还处理多维数组（实际上是数组的数组），这是一个我在书中没有描述的话题。要了解关于多维数组，请在 C# 帮助系统中查找多维数组。

# 数据数组排序

一个常见的编程挑战是需要对数组内的元素进行排序。因为数组不能增长或缩小，但这并不意味着内部的元素不能被移动、删除或添加。例如，以下代码段交换了数组中两个字符串元素的位置：

```csharp
string temp = strings[i]; // 保存第 i 个字符串。
strings[i] = strings[k]; // 用第 k 个替换它。
strings[k] = temp; // 用 temp 替换第 k 个。
```

在这个示例中，`strings` 数组中第 `i` 位置的对象引用被保存下来，这样当第二个语句用另一个元素替换它时，它就不会丢失。最后，`temp` 变量被保存回第 `k` 位置。从图上看，这个过程就像图 6-1。

本章其余部分讨论的数据集合在添加和删除元素方面比数组更灵活。

之前：

第一本书
第6章

| planets[i] | "Mercury" |
| planets[j] | "Earth" |

排队的
鸭子
带集合

图 6-1：
交换对象的术语是指交换两个对象的引用。

之后：

| planets[i] | "Mercury" |
| planets[j] | "Earth" |

![](img/36596fb11aa4233d5cab0d6ddd1d82e_142_0.png)

下面的程序演示了如何利用操作数组内元素的能力作为排序的一部分。这种特定的排序算法是冒泡排序。它对于具有数千个元素的大数组来说并不完美，但在小数组上简单且有效：

```csharp
// 给定一个行星列表，对它们的
// 名称进行排序：首先，按字母顺序。
// 第二，按名称长度排序，从短到长。
// 第三，从长到短排序。
// 此演示展示了如何使用和排序数组，通过
// 数组索引处理它们。使用了两种排序算法：
// 1. Array 类的 Sort() 方法使用的 Sort 算法。
// 2. 类的冒泡排序系统。
```

```csharp
namespace BubbleSortArray
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("离太阳最近的5个行星，顺序如下： ");
        string[] planets = new string[] { "Mercury", "Venus", "Earth", "Mars", "Jupiter" };
        foreach (string planet in planets)
        {
            // 使用特殊字符 t 插入到打印行中。
            Console.WriteLine("\t" + planet);
        }
    }
}
```

* 注意

# 118 数组数据排序

```csharp
Console.WriteLine("现在按字母顺序列出： ");
// 使用 Array 类内置的 Sort() 方法进行排序，
// 程序使用自定义排序对行星名称长度进行排序让你大惊。
Array.Sort(sortedNames);
foreach (string planet in sortedNames) {
    Console.WriteLine("\t" + planet);
}

Console.WriteLine("\n按长度： ");
// 该算法是“冒泡排序”：它是最简单
// 但性能最差的。Array.Sort() 方法效率
// 高得多。
int outer;
for (int outer = 0; outer < planets.Length; outer++) {
    int inner;
    for (int inner = 1; inner < planets.Length - outer - 1; inner++) {
        // 如果前面的一个比后面的
        // 元素，则交换它们。
        if (planets[inner - 1] > planets[inner]) {
            // 临时存储一个
            string temp = planets[inner - 1];
            // 用另一个元素覆盖那个行星。
            planets[inner - 1] = planets[inner];
            // 最后，从 temp 恢复行星
            planets[inner] = temp;
        }
    }
    Console.WriteLine("\t" + planets[outer]);
}

Console.WriteLine("\n现在长的在前： ");
// 即，只需遍历排序后的。
for (int i = planets.Length - 1; i >= 0; i--) {
    Console.WriteLine("\t" + planets[i]);
}

Console.WriteLine("\n按回车键终止...");
Console.Read();
```

下面的程序演示了如何将操作数组内元素的能力作为排序的一部分。这种特定的排序算法是冒泡排序。它对于具有数千个元素的大数组来说并不完美，但在小数组上简单且有效：

第二种排序的算法通过持续循环字符串列表，直到列表排序好为止。在每次遍历 `sortedNames` 数组时，程序比较每个字符串与它的邻居。如果发现两个顺序不对，方法将交换它们并标记列表为未排序。图 6-2 到 6-5 显示了每次通过后的行星列表。在图 6-5 中，注意倒数第二次通过产生了一个已排序的列表，最后一次通过由于没有变化而终止了排序。

