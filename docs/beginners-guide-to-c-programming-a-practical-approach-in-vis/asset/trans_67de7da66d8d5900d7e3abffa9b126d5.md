

代码 10.28（续）

- 11. 生成并运行项目。当我们点击**显示键和值**按钮时，键及其对应的值将显示在列表框中：

![](img/41d82527c4e41cdb7e56259564306ddc_271_0.png)

图 10.14。列表框中显示的键值对

## 10.2.2. ArrayList

ArrayList 是一种集合类型，是普通数组的灵活替代方案。ArrayList 具有两个主要优点：它们可以存储不同的数据类型，并且会在添加或删除新元素时自动调整大小。由于 ArrayList 的长度是动态的，因此在声明时不需要指定其长度。ArrayList 的另一个优点是，它提供了各种有用的方法，使我们能够动态地改变该结构中元素的顺序。

ArrayList 具有从 0 开始的整数索引，与普通数组一样。

让我们在一个小型项目中声明并使用 ArrayList。

- 1. 创建一个新的 C# 项目。
- 2. 在窗体上添加一个文本框、两个按钮和一个列表框。
- 3. 将文本框的 Name 属性设置为 `inputTextBox`。
- 4. 将第一个按钮的 Name 和 Text 设置为 `addButton` 和 `Add`。
- 5. 将第二个按钮的 Name 和 Text 设置为 `displayButton` 和 `Display`。

`myArrayList`。我输入了“Adam”、“Joseph”、“Peter”和“Benjamin”。当我点击 Display 按钮时，ArrayList 的内容将显示在列表框中：

![](img/41d82527c4e41cdb7e56259564306ddc_274_0.png)

图 10.17。列表框中显示的 ArrayList 元素

如果我们在 `inputTextBox` 中添加另一个字符串并点击 Add，它将被添加到 ArrayList 的末尾。当我们点击 Display 按钮时，它将显示如下：

![](img/41d82527c4e41cdb7e56259564306ddc_274_1.png)

图 10.18。添加到 ArrayList 中的新字符串“Britney”

- 11. 使用 ArrayList 的另一个优点是，可以通过 `ArrayList.Sort()` 方法轻松地对其元素进行排序。让我们再添加一个按钮，用于对 ArrayList 进行排序。在窗体上添加一个按钮，并将其 Name 和 Text 属性设置为 `sortButton` 和 `Sort`：

![](img/41d82527c4e41cdb7e56259564306ddc_275_0.png)

图 10.19。添加到窗体上的 Sort 按钮

- 12. 双击 Sort 按钮以创建其事件处理程序。我们将在此事件处理程序中使用 `Sort()` 方法，如下所示：

```csharp
private void sortButton_Click(object sender, EventArgs e)
{
    myArrayList.Sort();
}
```

代码 10.33

- 13. 再次生成并运行项目。我输入了与之前相同的字符串，然后点击 Sort 按钮。当点击 Display 按钮时，排序后的元素将显示在列表框中：

![](img/41d82527c4e41cdb7e56259564306ddc_275_1.png)

图 10.20。通过 Sort() 方法排序后的 ArrayList 元素

关于数组和集合，目前就介绍到这里；在接下来的项目中，我们将使用这些数据结构。下一章中，我们将了解如何通过在方法中使用重复代码来缩短程序。

## 11.2. 访问修饰符

如上所述，方法可以被调用的位置由其访问修饰符指定。访问修饰符可以采用以下值之一：

- 1. **private 关键字**：如果方法的访问修饰符设置为 private，则只能在该方法所属的类中调用它。例如，如果方法是在 Click 事件处理程序内部声明的，那么它只能在此事件处理程序内部调用，而不能从其他方法（如窗体默认的 Load 事件处理程序）中调用。
- 2. **public 关键字**：在这种情况下，可以从程序中的任何位置调用该方法。
- 3. **protected 关键字**：如果方法的访问修饰符为 protected，则还可以从其所属类的子类（派生类、子类）中调用该方法。
- 4. **internal 关键字**：在这种情况下，可以从其所属程序集（即 `.exe` 或 `.dll` 文件）中调用该方法。

## 11.3. 返回值方法示例

让我们在一个简单的项目中声明一个方法，该方法返回给定两个数字中较大的一个。

- 1. 创建一个新的 C# 项目。
- 2. 在窗体上添加三个文本框和一个按钮。
- 3. 将文本框的 Name 属性分别设置为 `input1`、`input2` 和 `output`。
- 4. 将按钮的 Name 和 Text 分别设置为 `findGreaterButton` 和 `Find the greater one`。窗体布局如下：

![](img/41d82527c4e41cdb7e56259564306ddc_277_0.png)

图 11.1。窗体布局

- 5. 首先声明方法。我们的方法将接收两个整数变量，确定这两个变量中较大的一个，并将该值作为整数返回。方法名称可以任意指定，我将其命名为 `FindGreater`。此时的问题是：我们应该在 `Form1.cs` 代码文件中的什么位置编写方法？虽然有几种可能性，但最方便的方式是将方法声明在代码中已经存在的 `public Form1()` 方法内部。在窗体上的空白处右键单击，然后选择 View Code，以打开 `Form1.cs` 文件的代码视图：

![](img/41d82527c4e41cdb7e56259564306ddc_278_0.png)

图 11.2。打开代码视图

如下所示，该方法将在 `Form1()` 方法内部声明：

![](img/41d82527c4e41cdb7e56259564306ddc_278_1.png)

图 11.3。声明方法的位置

- 6. 由于该方法只会在此窗体内部使用，因此可以将其声明为 public 或 private。让我们将其声明为 public：

```csharp
public int FindGreater(int number1, int number2)
```

代码 11.2

由于该方法将输出一个整数值，因此在 public 关键字之后将其返回类型设置为 int。然后写出方法名称：`FindGreater`。在名称之后声明方法的参数（输入）`number1` 和 `number2`，它们都是整数类型的变量。我们将在花括号内编写方法的内容，从而构成方法体：

```csharp
public int FindGreater(int number1, int number2)
{
    int greater;
    if (number1 > number2)
    {
        greater = number1;
    }
    else
    {
        greater = number2;
    }
    return greater;
}
```

代码 11.3

我们在方法内部声明了一个名为 `greater` 的整数变量，用于保存较大值。然后使用简单的 if-else 结构确定较大的数字，并将其赋值给变量 `greater`。最后，在代码行 `return greater;` 中使用 `return` 关键字返回变量 `greater`。请注意，我们使用 `return` 关键字从方法中返回（输出）一个值。完整的 `Form1.cs` 文件如下：

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
```

## 斯坦福大学发布2024年AI指数报告

近日，斯坦福大学以人为本人工智能研究所（Stanford HAI）发布了《2024年人工智能指数报告》（Artificial Intelligence Index Report 2024）。这份长达500页的报告是斯坦福大学迄今为止最全面的AI报告之一，追踪了2023年全球人工智能的发展趋势。

从研发到政策，从经济到教育，报告涵盖了AI在多个领域的进展和影响。以下是该报告的十大要点解读：

- 1. **AI在图像分类、视觉推理和英语理解等领域击败了人类，但在竞赛级数学、视觉常识推理和规划等更复杂的任务上仍落后于人类。**
- 2. **AI成为高薪职位的有力助推器。** 自2023年以来，AI相关职位的招聘数量持续增长，AI工程师和AI研究科学家等高技能职位的薪酬也因此水涨船高。
- 3. **生成式AI投资激增。** 2023年，全球对生成式AI的投资达到了创纪录的252亿美元，是2022年的约九倍。
- 4. **英伟达成为AI芯片领域的最大赢家。** 作为AI计算能力的核心供应商，英伟达凭借其在GPU市场的绝对主导地位，实现了利润的惊人增长。
- 5. **美国在顶级AI模型研发上领先全球。** 2023年，全球共诞生了51个著名的机器学习模型，其中美国贡献了27个，远超欧盟的15个和中国的8个。
- 6. **AI入门级壁垒正在降低。** 近年来，AI模型训练成本呈明显下降趋势，使得更多研究机构和个人开发者能够进入AI领域。
- 7. **美国AI相关法规数量显著增加。** 2023年，美国与AI相关的法规数量从2022年的1项增加到25项，增长幅度巨大。
- 8. **AI为普通民众带来更多实惠。** 由于技术进步和市场竞争，AI服务的价格正在大幅下降，让普通用户也能以更低成本使用先进的AI技术。
- 9. **中国在AI专利领域领先世界。** 2023年，中国在全球AI专利来源中占比超过60%，位居世界第一，显示出其在AI技术创新方面的强劲实力。
- 10. **AI的“智能化”与“情绪化”并存。** 报告指出，AI系统在理解复杂场景和人类情绪方面取得了巨大进步，但也引发了关于AI伦理和监管的更深层次讨论。

![](img/41d82527c4e41cdb7e56259564306ddc_280_0.png)

```csharp
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        public int FindGreater(int number1, int number2)
        {
            int greater;
            if (number1 > number2)
            {
                greater = number1;
            }
            else
            {
                greater = number2;
            }
            return greater;
        }

        private void findGreaterButton_Click(object sender, EventArgs e)
        {
            int input1Int = Convert.ToInt32(input1.Text);
            int input2Int = Convert.ToInt32(input2.Text);
            int outputValue = FindGreater(input1Int, input2Int);
            output.Text = outputValue.ToString();
        }
    }
}
```

代码 11.9（续）

- 11. 生成并运行项目。当我们输入两个整数并点击 Find the greater one 按钮时，程序将调用我们的方法，查找并返回较大的值，并将该值显示在 output 文本框中，如图 11.4 所示。

- 我们可以像在本项目中所做的那样，使用逗号作为分隔符，向方法传递任意数量的输入。
- 同样，如果需要，方法也可以返回多个以逗号分隔的值。

