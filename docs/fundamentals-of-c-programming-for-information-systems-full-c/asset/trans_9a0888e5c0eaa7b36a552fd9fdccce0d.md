

`ArrayName` 是 一维数组的名称，`SearchValue` 是你在数组中尝试查找的值。该方法返回与指定值匹配的第一个元素的索引。如果未找到值，则方法返回 -1。

例如，

```csharp
Array.IndexOf(names, "Mike Burns")
```

返回 names 数组中与指定值 Mike Burns 匹配的第一个元素的索引。

图 8-14 显示了使用此方法通过搜索指定名称来查找供应商电话号码的代码。

## 图 8-14：使用 IndexOf 方法查找电话号码的代码

```
private void btnFindPhone_Click(object sender, EventArgs e)
{
    string searchName = txtVendorName.Text;
    string fmtStr = "{0,-15}{1,8}";
    lstDisplay.Items.Clear();

    // Method 1: Use IndexOf method to find the record
    int index = Array.IndexOf(names, searchName);
        //if there is no match, index would be -1.
    if (index >= 0)
        lstDisplay.Items.Add(string.Format(fmtStr, searchName,
                                           phoneNumbers[index]));
    else
        MessageBox.Show("Sorry, name not found");
}
```

**第 60 行** 使用 IndexOf 方法获取 Names 数组中与 SearchName 值匹配的元素的索引。

**第 62–64 行** 如果索引不为 -1，则显示 phoneNumbers 数组中的对应元素。如果不是，则显示一条消息。

图 8-15 显示了使用循环将 SearchName 的值与 Names 数组中的每个元素进行比较的替代方法。

## 图 8-15：使用循环搜索字段

```
// Method 2: Use for loop to find the record
for (index = 0; index < recordCount; index++)
{
    if (searchName == names[index])
    {
        lstDisplay.Items.Add(String.Format(fmtStr, names[index],
                                            phoneNumbers[index]));
        return;
    }
}
MessageBox.Show("Sorry, there is no Vendor by that name");
```

步骤 2-5：添加图 8-15 中的代码。

通过输入 AMTRAK 进行代码测试，AMTRAK 是 Vendor.txt 文件中的供应商名称之一。

## 教程 3：使用 ComboBox 选择搜索名称

本教程创建了应用程序的另一个版本，其中供应商名称被添加到 ComboBox 中，并且当用户选择一个名称时，电话号码会自动显示在名为 SmallFiles 的表单上的 ListBox 中，如图 8-16 所示。仅当供应商数量相对较少时，使用 ComboBox 选择供应商才合适。将大量数据集加载到 ComboBox 中会花费时间。

## 图 8-16：带 ComboBox 选择名称的 SmallFiles 表单

![](img/143bad48262566137acc9c41f668a88f_265_0.png)

在此名为 SmallFiles 的表单中，你学习如何从文件中向 ComboBox 添加项目，并了解 SelectedIndexChanged 事件的应用。

步骤 3-1：打开表单 SmallFiles。

修订后代码的两个主要方面是

- 1. 表单的 load 事件处理程序，它从 Vendor.txt 读取数据到两个数组中，同时将供应商名称添加到 ComboBox。
- 2. ComboBox 的 SelectedIndexChanged 事件在用户选择供应商时查找所选名称的电话号码。

完整的代码如图所示 8-17。由于仅当供应商数量相对较少时使用 ComboBox 选择供应商才合适，因此代码不包括数组的调整大小。你使用相同的供应商文件 Vendor.txt。

## 8.5 写入文本文件

你可以使用框架类库 System.IO 命名空间中可用的 StreamWriter 类将数据写入文本文件。

## 教程 4：将分数写入文本文件

让我们开发一个表单，将文本框中的数据写入文本文件。图 8-18 显示了名为 WriteToTextFile 的表单。

## 图 8-18：WriteToTextFile 表单

![](img/143bad48262566137acc9c41f668a88f_268_0.png)

### StreamWriter 对象

StreamWriter 类可用于将数据写入文本文件。StreamWriter 对象使用以下语法创建：

```
StreamWriter VariableName = new StreamWriter(@"Path and FileName", append flag);
```

如果 append flag 为 true，则数据会被追加到现有数据之后（如果有）。如果 append flag 为 false，则现有数据（如果有）将被覆盖。在这两种情况下，如果指定的文件不存在，则会创建一个新文件。

如果未指定路径，则假定为项目目录的 Bin\Debug 文件夹。 当未指定路径时，“@”前缀不是必需的。例如，要以追加选项将数据写入 Exams.txt，StreamWriter 对象创建如下：

```
StreamWriter examsWriter = new StreamWriter("Exams.txt", true);
```

### StreamWriter 的 WriteLine 方法

StreamWriter 的 WriteLine 方法将字符串作为单独的行写入文件。使用此方法将每个学生的三个数据项写入 Exams.txt 文件的单独行中。

### 在类级别声明变量

由于数据要多次写入 Exams.txt（每次用户单击保存按钮时），因此你在表单加载时创建一次 StreamWriter，每次单击保存按钮时使用它，并在表单关闭时关闭 StreamWriter。这意味着引用 StreamWriter 的变量（examsWriter）在三个不同的方法中使用：

- 表单的 Load 事件，
- 保存按钮的 Click 事件，

步骤 4-5：运行表单。

程序在创建 examsWriter 对象的第 25 行中断。此时表单不可见，因为代码是 Load 事件处理程序的一部分。
单击运行以完成表单的加载。
删除断点。

由于 examsWriter 在 Load 事件中创建，因此在表单打开时可用，并且在保存按钮的 Click 事件处理程序中准备好用于写入，如图 8-20 所示。

## 图 8-20：将数据写入 Exams.txt 的代码

```
private void btnSave_Click(object sender, EventArgs e)
{
    string name, score1, score2;
    // Store all data in string variables.
    name = txtName.Text;
    score1 = txtScore1.Text;
    score2 = txtScore2.Text;
    // Combine name & scores and store in Exams.txt
    examsWriter.WriteLine(name + "," + score1 + "," + score2);
    MessageBox.Show("Data Saved.");
}
```

请注意，上面的代码在用户每次单击保存按钮时使用 StreamWriter 写入数据，而无需每次创建和关闭 StreamWriter。

要写入数据，name、score1 和 score2 被合并为一个字符串，(name + "," + score1 + "," + score2)，每个数据项之间用逗号分隔。插入逗号是为了便于在程序中读取数据时拆分字符串。

步骤 4-6：打开保存按钮的 Click 事件处理程序。从图 8-20 填写缺失的代码以将数据写入 Exams.txt 文件。

步骤 4-7：运行表单。输入 name、score1 和 score2 的数据，然后单击保存。

在出现“Data Saved.”消息时单击确定。

步骤 4-8：查看项目目录的 Bin\Debug 文件夹。打开在表单 ReadTextFile 中创建的 Exams.txt 文件。你将找不到你输入并本应写入其中的记录。发生了什么？

数据仅在关闭 StreamWriter 时才写入外部设备（硬盘、闪存驱动器等）。在此之前，StreamWriter 写入的数据保留在缓冲区临时内存中。你尚未添加关闭 Stream Writer 的代码。

### 表单的 FormClosing 事件

StreamWriter 对象应一直可用，直到表单关闭。因此，你只应在表单关闭时关闭 StreamWriter。这可以通过在 FormClosing 事件中关闭 StreamWriter 来完成

步骤 4-13：在第 25 行，将 append 标志更改为 false 如下：

```csharp
examsWriter = new StreamWriter("Exams.txt", false);
```

添加第三组数据并保存它。关闭表单。
打开 Exams.txt 并查看。你应该只看到第三组数据，因为之前的记录已被覆盖。
现在，将 append 标志改回 true。

是时候练习了！做练习 8-3

### Directory 类

System.IO 命名空间中的 Directory 类提供了多个用于处理目录（文件夹）的方法，包括创建文件夹和检查指定路径是否存在的方法。图 8-23 显示了 Directory 类的两个常用方法。

## 图 8-23：Directory 类的方法

| 方法 | 功能 |
|---|---|
| Exists(path) | 如果路径存在则返回 true，如果路径不存在则返回 false |
| CreateDirectory(path) | 创建指定路径中的目录 |

你可以通过指定除默认目录之外的其他路径，在 WriteToTextFiles 表单中创建 Exams.txt 文件。使用上述方法检查指定路径中的目录是否存在，并在不存在时创建它们。图 8-24 显示了创建路径 E:\Csharp\output（如果不存在）的代码，并使用该路径写入数据。

## 图 8-24：使用 Directory 类创建路径

```csharp
string path = @"E:\Csharp\output\";
if (!(Directory.Exists(path)))
    Directory.CreateDirectory(path);
examsWriter = new StreamWriter(path + "Exams.txt", true);
```

如果驱动器 E: 无效，你将收到错误。如果目录 Csharp 不存在，则会创建它，并在 Csharp 内创建目录 output。如果 Csharp 文件夹存在但 output 文件夹不存在，则会创建它。

最后一条语句，

examsWriter = new StreamWriter(path + "Exams.txt", true);

使用新创建的路径写入数据。

步骤 4-14：

暂时用图 8-24 中的代码替换第 25 行中的语句以创建目录并使用它写入数据。运行项目。
输入新记录并保存它。验证是否创建了新的目录 Csharp\output，并在其中创建了文件 Exams.txt。
删除你插入的代码，并将第 25 行改回其原始形式，不指定路径。

