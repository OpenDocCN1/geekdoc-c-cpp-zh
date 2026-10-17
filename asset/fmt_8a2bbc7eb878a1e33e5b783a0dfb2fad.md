
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
using System.IO;

namespace Test_Score_List
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        // ReadScores 方法从 TestScores.txt 文件
        // 读取分数并存 scoresList 参数。
        private void ReadScores(List<int> scoresList)
        {
            try
            {
                // 打开 TestScores.txt 文件。
                StreamReader inputFile = File.OpenText("TestScores.txt");
                // 将分数读取到列表中。
                while (!inputFile.EndOfOfStream)
                {
                    scoresList.Add(int.Parse(inputFile.ReadLine()));
                }
                // 关闭文件。
                inputFile.Close();
            }
            catch (Exception ex)
            {
                // 显示错误消息。
                MessageBox.Show(ex.Message);
            }
        }

        // DisplayScores 方法在 ListBox 控件中
        // 显示 scoresList 参数的内容。
        private void DisplayScores(List<int> scoresList)
        {
            foreach (int score in scoresList)
            {
                testScoresListBox.Items.Add(score);
            }
        }

        // Average 方法返回 scoresList 参数
        // 中数值的平均值。
        private double Average(List<int> scoresList)
        {
            int total = 0;
            // 累加器
            double average; // 用于持有平均值

            // 计算分数的总和。
            foreach (int score in scoresList)
            {
                total += score;
            }

            // 计算分数的平均值。
            average = (double)total / scoresList.Count;
            // 返回平均值。
            return average;
        }

        // AboveAverage 方法返回 scoresList 中
        // 高于平均分的个数。
        private int AboveAverage(List<int> scoresList)
        {
            int numAbove = 0;
            // 累加器
            // 获取平均分。
            double avg = Average(scoresList);
            // 统计高于平均分数的个数。
            foreach (int score in scoresList)
            {
                if (score > avg)
                {
                    numAbove++;
                }
            }
            // 返回高于平均分数的个数。
            return numAbove;
        }

        // BelowAverage 方法返回 scoresList 中
        // 低于平均分数的个数。
        private int BelowAverage(List<int> scoresList)
        {
            int numBelow = 0; // 累加器
            // 获取平均分。
            double avg = Average(scoresList);
            // 统计低于平均分数的个数。
            foreach (int score in scoresList)
            {
                if (score < avg)
                {
                    numBelow++;
                }
            }
            // 返回低于平均分数的个数。
            return numBelow;
        }

        private void getScoresButton_Click(object sender, EventArgs e)
        {
            double averageScore; // 用于持有平均分
            int numAboveAverage; // 高于平均分的个数
            int numBelowAverage; // 低于平均分的个数
            // 创建一个 List来持有分数。
            List<int> scoresList = new List<int>();
            // 从文件读取分数到 List 中。
            ReadScores(scoresList);
            // 显示分数。
            DisplayScores(scoresList);
            averageScore = Average(scoresList);
            numAboveAverage = AboveAverage(scoresList);
            numBelowAverage = BelowAverage(scoresList);

            averageScoreLabel.Text = averageScore.ToString("N2");
            aboveAverageLabel.Text = numAboveAverage.ToString();
            belowAverageLabel.Text = numBelowAverage.ToString();
        }

        private void exitButton_Click(object sender, EventArgs e)
        {
            this.Close();
        }
    }
}
```

## 检查

- **7.22** 使用语句初始化 List。

- **7.23** 使用语句向 List 添加新值。

- **7.24** 使用语句清空 List 内容。

- **7.25** 是否可以执行顺序搜索、二分搜索等？

## 7.10 ImageList 控件

ImageList允许你存储一组图像。在运行时，你可以从 ImageList 控件中检索图像并显示在 PictureBox 控件中。

ImageList 控件正如其名是一个列表。你可以使用索引从 ImageList 控件中检索图像并显示。

有一些你应该遵循的指南：

- ImageList 中的所有图像应具有相同的大小。

- 存储在 ImageList 中的图像不能超过 256 像素。

- 存储在 ImageList 中的图像应具有相同的格式（.bmp,.jpg 等）。

尽管这些指南看起来很严格，但请记住 ImageList 控件设计用于存储图标。

你可以在工具箱的组件部分找到 ImageList 控件。双击工具箱中的 ImageList 工具时，会在设计器底部创建一个 ImageList 控件。（ImageList 控件不会出现在表单上。）图 7-44 显示了一个示例。创建 ImageList 控件时，它们被命名为 imageList1、imageList2 等。

在创建 ImageList 控件后，你应该将其 ImageSize 属性设置为计划存储在控件中的图像的大小。默认大小为 16,16。（如果 ImageSize 属性的值与存储的图像的大小不匹配，图像将失真。）

然后，你可以使用 Images 属性向控件添加图像。在属性窗口中，点击 Images 属性旁边出现的省略号按钮。这将显示图 7-45 所示的图像集合编辑器窗口。点击 Add 按钮，会出一个打开对话框。对话框用于定位并选择你想添加到 ImageList 控件的图像（或多个图像文件）。图 7-46 显示了添加四个图像后的图像集合编辑器窗口。Members 列表中的图像名称分别为 2_Clubs.bmp、2_Diamonds.bmp、2_Hearts.bmp 和 2_Spades.bmp。注意每个图像旁边都出现了一个索引值。当你添加了所有需要的图像后，点击 OK 按钮。

## 图 7-46 添加了四张图像

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1026_0.png)

如果你知道特定图像的索引值，可以从 ImageList 控件中检索该图像并将其显示在 PictureBox 中。下面的代码显示了一个示例。假设 `myImageList` 是 ImageList 控件的名称，`myPictureBox` 是 PictureBox 的名称。

```
myPictureBox.Image = myImageList.Images[5];
```

该语句从 `myImageList` 中获取索引为 5 的图像，并将其赋值给 `myPictureBox` 控件的 `Image` 属性。结果图像显示在 PictureBox 中。

在代码中，你可以通过获取控件的 `Images.Count` 属性值来确定 ImageList 控件中存储的图像数量。下面的代码显示了一个示例。假设 `myImageList` 是 ImageList 控件的名称，`numberImages` 是一个 int 型变量的名称。

```
numberImages = myImageList.Images.Count;
```

在教程 7-5 中，你完成了一个应用程序，该程序从 ImageList 控件中随机选择图像并显示在 PictureBox 中。

## 图 7-47 随机卡片程序的表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1027_0.png)

教程

## 7-5: 完成随机卡片应用程序

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1028_0.png)

在本教程中，你将完成随机卡片应用程序，该程序会随机显示从 ImageList 控件中选择的扑克牌图像。应用程序的表单已经为你创建，如图 7-47 所示。注意，PictureBox 控件已经显示了卡片背面的图像。

- 步骤 1：启动 Visual Studio。在 Student Sample Programs 的 Chap08 文件夹中打开名为 Random Card 的项目。

- 步骤 2：确保在设计器中打开了 Form1 表单。在工具箱（Toolbox）中向下滚动，直到看到组件（Components）部分，双击 ImageList 工具。这将创建一个名为 `imageList1` 的 ImageList 控件，你应该在组件树中能看到它。

- 步骤 3：将 imageList 控件的名称更改为 `cardImageList`。

- 步骤 4：你添加到 `cardImageList` 控件的每张图像大小均为 50 x 70 像素。将 `cardImageList` 控件的 `ImageSize` 属性更改为 50, 70。

- 步骤 5：接下来，你向 `cardImageList` 控件添加图像。你要添加的图像位于 Student Sample Programs 中的 `Images/Cards/Poker Small` 文件夹中。在属性（Properties）窗口中，点击 `Images` 属性旁出现的省略号按钮。这将显示图像集合编辑器（Images Collection Editor）窗口。

点击 Add 按钮，会出现一个打开对话框。使用该对话框选择你想添加到 ImageList 控件的任意卡片图像文件（在点击文件名时可以使用 Shift 或 Ctrl 键来选择多个文件）。当你选好所有想要添加的图像后，点击 OK 按钮。

- **步骤 6：** 现在为 `getCardButton` 控件创建 Click 事件处理程序。在设计器中双击 `getCardButton` 控件。这将打开代码编辑器，你会看到一个空的事件处理程序 `getCardButton_Click`。通过输入 **Program 7-6** 中第 22–29 行的代码来完成事件处理程序。让我们回顾这段代码。

**第 23 行：** 该语句创建了一个 Random 对象，由变量 `rand` 引用。

**第 26 行：** 该语句声明了一个 int 变量 `index`。该变量用 `rand.Next` 方法返回的随机数初始化。注意 `imageList.Images.Count` 被作为参数传递给该方法。结果，我们得到了一个从 0 到 `imageList.Images.Count` 之间的随机数。

**第 29 行：** 该语句将图像赋值给 `PictureBox` 的 `Image` 属性。结果，图像显示在 PictureBox 中。

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Random
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void getCardButton_Click(object sender, EventArgs e)
        {
            Random rand = new Random();
            int index = rand.Next(imageList.Images.Count);
            myPictureBox.Image = myImageList.Images[index];
        }
    }
}
```

### Check点

- 7.26 如何确定 ImageList 控件中存储的图像数量？

- 7.27 ImageList 工具箱的哪个部分？

- 7.28 使用 ImageList 控件时应遵循哪些准则？

- 7.29 如何向 ImageList 控件添加图像？

- 7.30 哪个值决定了显示哪张图像？

### 关键术语

- Add method

- array

- binary search

- Clear method

- Count property

- elements

- foreach loop

- collection

- ImageList control

- IndexOf method

- initialization list

- Insert method

- iteration variable

- jagged array

- List

- new operator

- off-by-one error

- one-dimensional

- rectangular arrays

- reference

- reference copy

- reference types

- reference variable

- Remove method

- RemoveAt method

- search algorithm

- sizeator
