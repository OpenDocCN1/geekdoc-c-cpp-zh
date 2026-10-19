
第31行使用指定月份的索引从 unitsSold 数组中查找销量。
步骤2-3：运行窗体并测试代码。

## 使用循环在数组中查找值

使用 `Array.IndexOf` 方法查找数据项索引的替代方法是使用循环，将数组的每个元素与要查找索引的数据项进行比较。例如，要查找 months 数组中“March”的索引，请将 months 数组中的每个月与“March”进行比较，直到找到匹配项或比较完所有元素。图7-22显示了使用for循环的代码。

### 图7-22：使用for循环查找销量

```
// Alternate method using a loop:
// Compare each month in the array to the specified month
int index = 0;
for (index = 0; index < months.Length; index++)
{
    if (months[index] == monthName)
    {
        unitsSoldInMonth = unitsSold[index];
        lblUnitsSold.Text = unitsSoldInMonth.ToString();
        break; // if month is found jump out of the loop
    }
}
// Display a message, if month was not found
if (index >= months.Length)
{
    MessageBox.Show("Month not found");
    return;
}
```

第42行和第44行：第42行中的for循环使index的值从0到11按1递增，因此第44行中的语句

```
if (months[index] == monthName)
```

将等同于12条不同的语句：

```
if (months[0] == monthName)
if (months[1] == monthName)
...
if (months[11] == monthName).
```

第48行：如果指定的月份与数组中的某个月份匹配，则第48行中的break语句将控制权转移出循环。

第52行：如果指定月份与数组中的任何月份都不匹配，则index的值将等于数组的大小（12），该大小由Length属性给出。第52行检查index是否大于或等于数组大小。

步骤2-4：注释掉第29-37行中的语句，并添加图7-22中第38-55行的代码。运行窗体并测试代码。

## 是时候练习了！完成练习7-2和7-3。

## 练习

### 练习 7-1

从Tutorial_Starts文件夹中打开项目Ch7_Arrays。打开名为Exercise 7_1的窗体。在btnDisplayMonth的Click事件处理器中添加必要的代码，以显示用户输入的月份编号对应的月份名称。例如，如果用户输入数字3，代码应显示“March”，如下所示：

![](img/143bad48262566137acc9c41f668a88f_243_0.png)

提示：创建一个字符串数组，并将十二个月份名称（January 到 December）分配给它作为初始值。为了避免每次单击按钮时都创建数组，请在Click事件处理器之外、类级别创建数组。在Click事件处理器中使用该数组查找并显示月份名称。

### 练习 7-2

A部分：本练习查找并显示销售额最高的月份。向你在教程2中使用的LookUpUsingArray窗体添加一个名为btnTopMonths的按钮。在按钮的Click事件处理器中添加必要的代码，以在ListBox中查找并显示最高销售额及销售额最高的月份。可以使用以下方法：

首先，通过循环遍历unitsSold数组查找最高销售额，如下所示：
- 将最高销售额设置为unitsSold的第一个元素（`int highestSale = unitsSold[0];`）
- 将highestSalePosition设置为零。
- 使用一个循环（初始化并递增索引）将每个数组元素与最高销售额进行比较。如果数组元素大于最高销售额，则使用以下逻辑更新最高销售额和highestSalePosition：
  - 如果（数组元素 > 最高销售额）
  - 将highestSale设置为unitsSold的当前元素
  - 将highestSalePosition设置为index的当前值

接下来，显示highestSale以及highestSalePosition处的月份。

B部分：本练习与A部分类似，不同之处在于查找并显示销售额最低的月份。向你在教程2中使用的LookUpUsingArray窗体添加一个名为btnBottomMonths的按钮。在按钮的Click事件处理器中添加必要的代码，以在ListBox中查找并显示最低销售额及销售额最低的月份。可以使用以下方法：

首先，通过循环遍历unitsSold数组查找最低销售额，如下所示：
- 将最低销售额设置为unitsSold的第一个元素（`int lowestSale = unitsSold[0];`）
- 将lowestSalePosition设置为零。
- 使用一个循环（初始化并递增索引）将每个数组元素与最低销售额进行比较。如果数组元素小于最低销售额，则使用以下逻辑更新最低销售额和lowestSalePosition：

```
if (array element < lowestSale)
set lowestSale to the current element of unitsSold
set lowestSalePosition to the current value of index
```

接下来，显示lowestSale以及lowestSalePosition处的月份。

### 练习 7-3

Tutorial_Starts/Ch7_Arrays项目中的TheaterTicketsWithArray窗体执行的功能与Ch6_GUIcontrols中的TheaterTickets窗体基本相同。TheaterTicketsWithArray窗体不是使用按钮来计算费用，而是将计算费用和显示费用合并到ComboBox的SelectedIndexChanged事件处理器中。此外，该窗体不使用单独的方法来计算折扣。

修改此窗体，使应付金额包含所选节目的加价。当用户从ComboBox中选择一个节目时，将该节目的加价添加到应付金额中并显示该金额。可以使用以下方法：

在窗体中添加必要的语句，创建一个名为markups的第二个数组，其中包含每个节目的加价金额（正值或负值）。

将代码添加到ComboBox的SelectedIndexChanged事件处理器中，以查找所选节目的加价金额，并将该金额添加到应付金额中。在ListBox中显示该金额。确保数组的引用变量shows在类级别声明，以便可以在窗体的Load事件和ComboBox的SelectedIndexChanged事件处理器中使用。

## 顺序文件和数组

存储在变量和数组中的数据在程序终止时会丢失。顺序访问文件提供了一种相对简单的方法，可以将数据长期存储在硬盘、磁带和闪存驱动器等设备中。本章讨论将数据写入顺序文件以及从文件读取数据。此外，我们还将研究如何将文件中的数据读取到一维和二维数组中。

## 主题

| 8.1 | 文本文件简介 | 8.5 | 写入文本文件 |
| 8.2 | 拆分行：Split方法 | 8.6 | SaveFileDialog控件 |
| 8.3 | 从文件读取数据到数组 | 8.7 | 将数组传递给方法 |
| 8.4 | 数组的其他方法 | 8.8 | 二维（2-D）数组 |

### 8.1 文本文件简介

在顺序访问文件中，数据按顺序访问，从第一组数据项开始，然后是后续各组。要查找特定数据项，需要先遍历它之前的所有数据，就像在盒式磁带上播放歌曲一样。相比之下，可以直接从直接访问（随机访问）文件中访问数据，类似于在CD上播放歌曲。

顺序文件有两种类型：文本文件和二进制文件。在文本文件中，所有数据（包括数字和日期）都以文本形式存储。例如，数字9.95存储为四个字符（三位数字和一个小数点）的组合，构成一个字符串。因此，可以使用记事本之类的文本编辑器创建和编辑文本文件。二进制文件（在附录A中讨论）以原始形式存储数据，而不将其转换为文本。数字9.95使用数字的标准内部表示形式存储为单个数字。

## 从文本文件读取行

通常，文本文件将每条记录存储在单独的一行中，数据项由逗号、制表符或竖线字符（|）等分隔符分隔。由于文本文件是顺序访问文件，因此数据从文件开头到结尾按顺序读取。

## 示例1：读取并显示考试成绩

下面是一个文本文件示例，其中包含学生的姓名和两个考试成绩：
- Mike Burns, 75, 92
- Cathy Arnold, 86, 95
- Wesley Mathews, 82, 90
- Jerry Luke, 70, 89

