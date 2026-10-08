
# 数组与列表

> 注意：数组的 `Length` 属性是只读的，因此你无法更改它的值。

在教程 1 中，你将完成一个生成一组类似于彩票中随机数字的应用程序。这些数字将存储在数组中。

### 教程 1：使用数组存储随机彩票数字列表

在本教程中，你将完成一个随机生成彩票数字的应用程序。应用程序的表单如图 10 所示。点击生成数字（Generate Numbers）按钮时，应用程序将生成两位整数并将其存储在数组中。数组的内容将显示在 `Label` 标签控件中。

**图 10** 彩票数字表单

![](img/9467d25da5679b16515c9401daaae36c_414_0.png)

- **步骤 1：** `Visual Studio` 或 `Visual C#`。打开学生示例程序第 07 章中名为 `Lottery Numbers` 的项目。
- **步骤 2：** 在设计器中打开 `Form1`。双击 `generateButton` 控件。这将打开代码，你将看到一个名为 `generateButton_Click` 的空事件处理程序。通过输入 `Program 1` 中第 21–40 行所示的代码来完成 `generateButton_Click` 程序。让我们仔细观察：
  **第 22 行：** 该语句声明了一个名为 `SIZE` 的 `int` 常量，其设置为值 5。它被用作数组声明符。
  **第 23 行：** 该语句创建了一个名为 `lotteryNumbers` 的具有五个元素的数组。
  **第 26 行：** 该语句创建了一个 `Random` 对象，由变量 `rand` 引用。
  **第 30 行：** 该循环使用 `int` 变量 `index` 作为其计数器。`index` 变量被初始化为值 0，并在每次迭代后增加。只要 `index` 小于 `lotteryNumbers.Length` 即为 5，循环就会继续迭代。因此，循环将迭代五次。在迭代过程中，`index` 被赋值为 0, 1, 2, 3 和 4。
  **第 32 行：** 该语句获取一个 0 到 99 之间的随机数并将其赋值给 `lotteryNumbers[index]`。循环第一次迭代时，该语句将一个随机数赋值给 `lotteryNumbers[0]`。循环第二次迭代时，该语句将一个随机数赋值给 `lotteryNumbers[1]`。此过程持续到循环结束。此时，数组中的每个元素都被分配了一个随机数。
  第 36-40 行：这些语句在 `firstLabel`、`secondLabel`、`thirdLabel`、`fourthLabel` 和 `fifthLabel` 控件中显示数组元素。
- **步骤 3：** 将视图切换到设计器并双击退出 `exit` 按钮。在代码编辑器中，你将看到一个名为 `exitButton_Click` 的空处理程序。通过输入 `Program 1` 中第 45-46 行所示的代码来完成 `exitButton_Click` 事件。
- **步骤 4：** 保存项目。然后，在键盘上按 `[F5]`，或点击工具栏上的开始调试 `Start Debugging` 按钮来运行应用程序。当应用程序运行时，点击生成数字按钮。应用程序理应在 `Label` 控件中显示一组随机数。多次点击生成数字以查看不同的随机数组。完成后，点击退出 `Exit` 退出应用程序。

`Lottery Numbers` 应用程序中 `Form1` 的 `Program 1` 完成

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
```

```csharp
namespace Lottery_Numbers {
public class Form1 : Form {
    public Form1() {
        InitializeComponent();
    }
    private void voidGenerateButton_Click(object sender, EventArgs e) {
        // 创建一个数组来存储数字。
        const int SIZE = 5;
        int[] lotteryNumbers = new int[SIZE];
        // 创建一个 Random 对象。
        Random rand = new Random();
        // 用随机数填充数组，范围在
        // 0 到 99。
        for (int index = 0; index < lotteryNumbers.Length; index++) {
            lotteryNumbers[index] = rand.Next(100);
        }
```

```csharp
firstLabel.Text = lotteryNumbers[0].ToString();
secondLabel.Text = lotteryNumbers[1].ToString();
thirdLabel.Text = lotteryNumbers[2].ToString();
fourthLabel.Text = lotteryNumbers[3].ToString();
fifthLabel.Text = lotteryNumbers[4].ToString();
}
private void exitButton_Click(object sender, EventArgs e) {
    this.Close();
}
```

### 注意差一错误 Off-by-One Errors

当迭代次数多或少一次时就会发生差一错误。由于下标从 0 开始，让我们来看下：

```csharp
// 创建一个数组来存储数字。
const int SIZE = 5;
int[] lotteryNumbers = new int[SIZE];
// 用随机数填充数组，范围在
// 0 到 99。
for (int index = 0; index < lotteryNumbers.Length; index++) {
    lotteryNumbers[index] = rand.Next(100);
}
```

差一错误在遍历数组时很常见。例如，如果你使用以下代码：

```csharp
for (int index = 0; index <= lotteryNumbers.Length; index++) {
    // 这是一个差一错误
}
```

### `foreach` 循环与 `for` 循环

当你需要从第一个到最后一个读取数组中存储的值时，`foreach` 循环比 `for` 循环更易用。使用 `foreach` 循环时，你不需要担心数组的大小，也不需要创建一个计数来持有下标。然而，由于迭代变量是只读的，在某些情况下 `foreach` 循环是不够的。如果你需要执行以下操作，则无法使用 `foreach` 循环：
- 反向遍历数组元素
- 访问部分而非全部数组元素
- 在循环中同时处理两个或多个数组

在任何情况下，你都应该使用 `for` 循环处理数组。

### 重新赋值数组引用变量

可以将数组引用重新赋值为不同的数组，代码示例所示：

```csharp
// 创建由 numbers 变量引用的数组。
int[] numbers = new int[6];
// 将 numbers 变量重新赋值为新数组。
numbers = new int[3];
```

第 2 行创建一个六元素的 `int` 数组。数组的引用被赋值给 `numbers` 变量。图 11 显示了在该语句执行后 `numbers` 变量如何引用该六元素数组。

# 数组与列表

图 11 引用六元素数组的 `numbers` 变量

| numbers | 可以存储六个 int 值的数组 |
|---|---|
| variable | | | | | | | |

然后，第 5 行的语句创建了一个新的三元素数组。当第 5 行执行时，新数组的引用被赋值给 `numbers` 变量。存储在 `numbers` 变量中的引用将被指向三元素数组的引用所替换。在该语句执行后，`numbers` 变量将引用三元素数组而不是六元素数组。这在图 12 中所示。

图 12 引用三元素数组的 `numbers` 变量

| numbers | 可以存储六个 int 值的数组 |
|---|---|
| variable | | | | | |
| | 可以存储三个 int 值的数组 |
| | | | |

注意图 12，六元素数组仍然存在于内存中，但它不再被任何变量引用。由于它不再被引用，因此它无法被访问。当一个对象不再被引用时，它就符合垃圾回收条件。垃圾回收是一个定期运行的过程，用于从内存中移除所有未引用的对象。

### 检查点

- 5 编写一条语句，声明一个名为 `monthlyPay` 的引用变量，用于存储数值型数组。
- 6 编写一条语句，使得检查点 5 中的 `monthlyPay` 变量引用一个可以存储 12 个值的数值数组。
- 7 将检查点 5 和 6 的语句合并为一条语句，并使用常量作为大小声明符。
- 8 编写一条语句，创建一个并由名为 `fullName` 的变量引用的包含 3 个字符串值的数组。使用用于名、中间名和姓的字符串值为该数组提供初始化列表。
- 9 在什么情况下，你应该使用 `for` 循环而不是 `foreach` 循环来处理存储在数组中的数据？
- 10 当数组之类的对象不再被变量引用时，会发生什么？

### 处理文件和数组

**概念**：对于某些问题，文件和数组可以有效地结合使用。你可以轻松地编写一个循环，将数组的内容保存到文件中，反之亦然。

某些任务可能需要你将数组的内容保存到文件中，以便稍后使用这些数据。同样，某些情况可能需要你从文件中读取数据到数组中。例如，假设你有一个包含一组值的文件，并且你想反转这些值的顺序。实现此点的技术之一是将文件的值读取到数组中，然后从数组尾部部将值写回文件。

### 将数组内容写入文件

将数组的内容写入文件是一个简单的过程：打开文件，并使用循环遍历数组的每个元素，将其内容写入文件。例如，在 `Sample Programs` 的 `Chap7` 文件夹中，你会找到一个名为 `Array To File` 的项目。当你点击 `OK` 按钮时，应用程序会将 `int` 数组的内容写入文件。以下代码显示了 `OK` 按钮的 `Click` 事件处理程序。

```csharp
private void jButton_Click(object sender, EventArgs e)
{
    // 创建一个带有某些值的数组。
    int[] numbers = { 10, 20, 30, 40, 50 };
    // 声明一个 StreamWriter 变量。
    StreamWriter outputFile;
    // 创建文件并获取一个 StreamWriter 对象。
    outputFile = File.CreateText("Values.txt");
    // 将数组的内容写入文件。
```
