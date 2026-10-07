
```csharp
// 返回最大值
return highest;
}

// Lowest 方法
// 接受一个 int 数组参数
// 并返回数组中的
// 最小值。
private int lowest(int[] iArray) {
  // 声明一个变量
  // 存储最小值，并
  // 使用数组中的
  // 第一个值进行初始化。
  int lowest = iArray[0];
  // 遍历数组的
  // 剩余部分，从元素
  // 1 开始。当找到
  // 小于 lowest 的值时，
  // 将该值赋值给
  // lowest。
  for (int index = 1; index < iArray.Length; index++) {
    {
      if (iArray[index] < lowest) {
        iArray[index];
        lowest =
      }
    }
  }
  // 返回最低值。
  return lowest;
}
```

```csharp
private void getScoresButton_Click(object sender, EventArgs e)
{
  try
  {
    // 本地变量
    const int SIZE = 5;
    // 测试次数
    int[] scores = new int[SIZE]; // 测试分数数组
    int index = 0;
    // 循环计数器
    int highestScore;
    // 用于存储最高分
    int lowestScore;
    // 用于存储最低分
    double averageScore;
    // 用于存储平均分
    StreamReader inputFile;
    // 用于文件输入
    // 打开文件并获取一个 StreamReader 对象。
    inputFile = File.OpenText("Scores.txt");
    // 将测试分数读入数组。
    while (!inputFile.EndOfStream && index < scores.Length)
    {
      scores[index] = int.Parse(inputFile.ReadLine());
      index++;
    }
    // 关闭文件。
    inputFile.Close();
    // 显示分数。
    foreach (int value in scores)
    {
      testListBox.Items.Add(value);
    }
  }
}
```

```csharp
)
  // 获取最高、
  // 最低和平均分数。
  highestScore = Highest(scores);
  lowestScore = Lowest(scores);
  averageScore = Average(scores);
  // 在 ListBox 中显示测试分数的最高、
  //最低和平均分。
  resultListBox.Text = highestScore.ToString() + ", " + lowestScore.ToString() + ", " + averageScore.ToString();
  }
}
catch (Exception ex)
{
  // 显示错误
  MessageBox.Show("发生错误: " + ex.Message);
}
}

private void exitButton_Click(object sender, EventArgs e)
{
  this.Close();
}
}
```

Figure 7-28 The Test Average[img/2e5a40b206ba3cf1f5ae128_95] (Note: Image inferred from context)

Figure 7-27 The Test application[img/2e5a40b206ba3cf1f5ae128_96]

## 7.6 Advanced Algorithms for Sorting and Searching

A sorting algorithm is used to organize data. A search algorithm is a method of locating an item in a collection.

### Selection Sort

Often the data in an array must be sorted. In this section, we explore how to write your own sorting algorithm. The selection sort scans the array, starting at element 0, and locates the element with the smallest value. Then, the contents of this element are swapped with the contents of element 0. After the swap, the array appears as shown in Figure 7-29.

Figure 7-29 Values in an array

| 5 | 7 | 2 | 8 | 9 | 1 |
|---|---|---|---|---|---|
| Element 0 | Element 1 | Element 2 | Element 3 | Element 4 | Element 5 |

Then, the algorithm repeats the process, but because element 0 already contains the smallest value, it can be left out of the procedure. This time, the algorithm begins the scan at element 1. In this example, the value in element 2 is swapped with the value in element 1. Then, the array appears as shown in Figure 7-30.

Figure 7-30 Values in the array after the first swap

| 1 | 7 | 2 | 8 | 9 | 5 |
|---|---|---|---|---|---|
| Element 0 | Element 1 | Element 2 | Element 3 | Element 4 | Element 5 |

Again, the process is repeated, but this time the scan begins at element 2. The algorithm will find that element 5 contains the next smallest value. This element's value is swapped with that of element 2, causing the array to appear as shown in Figure 7-31.

Figure 7-31 Values in the array after the second swap

| 1 | 2 | 5 | 8 | 9 | 7 |
|---|---|---|---|---|---|
| Element 0 | Element 1 | Element 2 | Element 3 | Element 4 | Element 5 |

Next, the scanning begins at element 3. Its value is swapped with that of element 5, causing the array to appear as shown in Figure 7-32.

Figure 7-32 Values in the array after the third swap

| 1 | 2 | 5 | 7 | 9 | 8 |
|---|---|---|---|---|---|
| Element 0 | Element 1 | Element 2 | Element 3 | Element 4 | Element 5 |

Figure 7-33 Values in the array after the fourth swap

| 1 | 2 | 5 | 7 | 8 | 9 |
|---|---|---|---|---|---|
| Element 0 | Element 1 | Element 2 | Element 3 | Element 4 | Element 5 |

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_965_0.png)

此时，只剩下两个元素需要排序。算法发现元素 5 的值小于元素 4 的值，因此两者进行了交换。这使得数组处于最终排列状态，如图 7-34 所示。

### 图 7-34 第次交换后数组中的值

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_965_1.png)

### 交换数组元素

正如你在选择排序算法描述中所看到的，当算法遍历数组时，某些元素会被交换。让我们简要讨论一下计算机内存中交换两个项目的过程。假设有以下变量声明：

```csharp
int a = 1;
int b = 9;
```

假设我们想要交换这些变量中的值，使得变量 `a` 包含 9，变量 `b` 包含 1。起初，你可能认为只需要将变量互相赋值，如下所示：

```
// 错误！以下代码并不会交换变量。
a = b;
b = a;
```

为了理解为什么这样做不起，让我们逐步执行代码。第一条语句是 `a = b`。这导致值 9 被赋值给 `a`。但是，之前存储在 `a` 中的值 1 发生了什么呢？记住，当你给变量赋一个新值时，新值将替换该变量中之前存储的任何值。因此，旧值 1 被丢弃了。接下来的语句是 `b = a`。由于变量 `a` 包含 9，这会将 9 赋值给 `b`。在执行这些语句后，变量 `a` 和 `b` 都包含值 9。

要成功地交换两个变量的内容，我们需要第三个变量来作为临时存储位置：

```csharp
int temp;
```

然后我们就可以执行以下步骤来交换变量 `a` 和 `b` 的值：

- 将 `a` 的值赋给 `temp`。
- 将 `b` 的值赋给 `a`。
- 将 `temp` 的值赋给 `b`。

图 7-35 显示了在执行这些每个步骤时这些变量的内容。注意，在步骤完成后，`a` 和 `b` 中的值已经交换了位置。

### 图 7-35 交换 a 和 b 的值

```csharp
int a = 1;
int b = 9;
temp temp;
```

```
temp = a;
```

| | a |

| b | 9 |

| temp | ? |

| | a |

| b | 9 |

| temp | 1 |

```
a = b;
```

```
b = temp;
```

| a | 9 |

| b | 9 |

| temp | 1 |

| a | 9 |

| b | 1 |

| temp | 1 |

这里是一个 `Swap` 方法的代码，我们可以用它来交换 `int` 类型的值：

```csharp
private void Swap(ref int a, ref int b)
(
  int temp = a;
  a = b;
  b = temp;
)
```

#### 注意

在 `Swap` 方法中使用引用参数（reference parameters）至关重要，因为该方法必须能够更改作为参数传递它的项目的值。

让我们来看演示选择排序算法的完整程序。在 Student Sample Programs 的 `Chap07` 文件夹中，你会找到一个名为 `Selection Sort` 的项目。图 7-36 显示了应用程序表单。在左侧，你看到设计器中的表单，带有各种控件的名称。在右侧，你看到运行时的表单。当你点击 `Go` 按钮时，会以下操作：

### 图 7-36 Selection Sort 应用程序的表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_969_0.png)

- 创建一个未排序值的 `int` 数组。数组的内容在 `originalListBox` 控件中显示。
- 数组作为参数传递给 `SelectionSort` 方法。该方法使用选择排序算法对数组进行排序。
- 数组的内容在 `sortedListBox` 控件中显示。程序 7 显示了 Selection Sort 应用程序的完整代码。

### Selection Sort 应用程序中 Form1 的完整代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Selection_Sort
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    }

    // SelectionSort 方法
    // 接收 int 数组作为参数。
    // 使用选择排序算法对数组进行排序。
    private void SelectionSort(int[] iArray)
    {}
```
