
IEnumerable 不满足这两个接口中的任何一个。为了解决这个问题，程序调用结果的 ToArray 方法，将其转换为 DataSource 属性可以处理的数组。

显示此结果后，程序执行另外两个 LINQ 查询，并以类似方式显示它们的结果。第一个查询选择欠款至少为 $50 的 Customers。最后一个查询选择欠款至少为 $50 且 DueDate 已过去超过 30 天的 Customers。

## ORDER BY 子句

如果对选中的值进行排序，查询结果通常会更易读。可以通过在 where 子句和 select 子句之间插入 order by 子句来实现。

order by 子句以关键字 orderby 开头，后跟一个或多个用逗号分隔的值，这些值决定结果的排序方式。

可以选择在值后面加上关键字 ascending（默认）或 descending，以确定结果是按升序（1-2-3 或 A-B-C）还是降序（3-2-1 或 C-B-A）排序。

例如，以下查询选择余额为负的 Customers，并对它们排序，使值最小（负得最多）的 Customers 排在前面：

```
var negativeQuery =
    from Customer cust in customers
    where cust.Balance < 0
    orderby cust.Balance ascending
    select cust;
```

以下版本先按 balance 对结果排序，然后如果两个 customers 的 balance 相同，则按 last name 排序：

```
var negativeQuery =
    from Customer cust in customers
    where cust.Balance < 0
    orderby cust.Balance, cust.LastName
    select cust;
```

## SELECT 子句

select 子句确定从数据源中提取并存储在结果中的是什么数据。前面所有示例都选择它们所遍历的数据。例如，Find Customers 示例程序遍历 Customer 对象数组，并选择某些 Customer 对象。

程序可以不选择查询范围中的对象，而只选择这些对象的某些属性、由这些属性计算出的结果，甚至全新的对象。从现有数据中选择一种新的数据称为转换或投影数据。

图 36-2 所示的 Find Students 示例程序（也可从本书网站的课程代码下载中获取）使用以下简单的 Student 类：

```
class Student
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public List<int> TestScores { get; set; }
}
```

该程序使用以下查询选择所有学生的姓名和测试平均分，并按姓名排序：

```
// Select all students and their test averages ordered by name.
var allStudents =
    from Student student in students
    orderby student.LastName, student.FirstName
    select String.Format("{0} {1} {2:0.00}",
        student.FirstName, student.LastName,
        student.TestScores.Average());
allListBox.DataSource = allStudents.ToArray();
```

![](img/d5be6ade75773ca6cec5c78f96a98bb1_544_0.png)

图 36-2

此查询的 select 子句不选择范围变量 student，而是选择一个字符串，其中包含学生的名、姓以及学生的测试分数平均值。（请注意，代码如何调用 TestScore 列表的 Average 方法获取测试分数的平均值。）查询结果是 List<string>，而不是 List<Student>。

接下来，程序使用以下代码列出平均分至少为 60 的学生，使他们获得及格成绩：

```
// Select passing students ordered by name.
var passingStudents =
    from Student student in students
    orderby student.LastName, student.FirstName
    where student.TestScores.Average() >= 60
    select student.FirstName + " " + student.LastName;
passingListBox.DataSource = passingStudents.ToArray();
```

这段代码同样选择一个字符串，而不是 Customer 对象。选择不及格学生的代码类似，因此此处未显示。

该程序使用以下代码选择平均分低于班级平均分的学生：

```
// Select all scores and compute a class average.
var allAverages =
    from Student student in students
    select student.TestScores.Average();
double classAverage = allAverages.Average();

// Display the average.
this.Text = "FindStudents: Class Average = " +
    classAverage.ToString("0.00");
```

```
// Select students with average below the class average ordered by average.
var belowAverageStudents =
    from Student student in students
    orderby student.TestScores.Average()
    where student.TestScores.Average() < classAverage
    select new {Name = student.FirstName + " " + student.LastName,
        Average = student.TestScores.Average()};

foreach (var info in belowAverageStudents)
    belowAverageListBox.Items.Add(info.Name + "\t" + info.Average);
```

此代码片段首先选择所有学生的测试分数平均值。这会返回一个 List<double>。程序调用该列表的 Average 函数获取班级平均分。

接下来，代码再次查询学生数据，这次选择平均分低于班级平均分的学生。

此查询演示了一种新的 select 子句，它创建一个对象列表。新对象有两个属性 Name 和 Average，由 select 子句赋值。这些新对象的数据类型是自动创建的，并且没有显式名称，因此称为匿名类型。

创建查询后，代码循环遍历其结果，使用每个对象的 Name 和 Average 属性在 ListBox 中显示低于平均分的学生。请注意，代码为循环变量 info 指定了隐式数据类型 var，因此无需确定它实际具有的数据类型。

> **注意** 具有匿名数据类型的对象实际上有一个真实的数据类型，只是这个类型并非你愿意去弄清楚的类型。例如，可以在前面代码的 foreach 循环内添加以下语句，查看这些对象实际具有什么数据类型：
> 
> `Console.WriteLine(info.GetType().ToString());`
> 
> 如果查看“输出”窗口，你会看到这些对象具有如下难看的类型：
> 
> `<>f__AnonymousType0`2[System.String,System.Double]`
> 
> 尽管你多少能看出这里发生了什么（该对象包含一个字符串和一个 double），但即使可以，你大概也不想把这一团乱麻输入到代码中。在这种情况下，var 类型要易读得多。

LINQ 还提供了许多其他功能，本课无法一一涵盖。它允许你：

- 对结果进行分组，生成包含其他列表的列表
- 仅取一定数量的结果，或在某个条件为真时取结果
- 跳过一定数量的结果，或在某个条件为真时跳过结果
- 联接从多个数据源选择的结果
- 使用聚合函数，如 Average（你已经见过）、Count、Min、Max 和 Sum

Microsoft 的“Language-Integrated Query (LINQ)”页面（msdn.microsoft.com/library/bb397926.aspx）是进一步了解 LINQ 的良好起点。

## 试一试

在第 29 课的“试一试”中，你构建了一个程序，该程序使用 DirectoryInfo 类的 GetFiles 方法搜索与模式匹配且包含目标字符串的文件。例如，该程序可以从 C:\Projects 开始搜索目录层次结构，查找扩展名为 .cs 且包含字符串 "DirectoryInfo." 的文件。

在本课的“试一试”中，你修改该程序，以使用 LINQ 执行相同的搜索。你不必编写代码来循环遍历 GetFiles 返回的文件并逐个检查，而是让 LINQ 为你检查这些文件。

## 课程要求

在本课中，你需要：

- 复制你为第 29 课“试一试”构建的程序（或从本书网站下载第 29 课的版本），并修改代码以使用 LINQ 搜索文件。

> 注意 你可以从网站 www.wrox.com/go/csharp24hourtrainer2e 下载本课的代码和资源。

## 提示

- 在查询的 from 子句中使用 DirectoryInfo 对象的 GetFiles 方法。
- 在查询的 where 子句中，使用 File 类的 ReadAllText 方法获取文件内容。将其转换为小写，并使用 Contains 查看文件是否包含目标字符串。

## 分步操作

- 复制你为第 29 课“试一试”构建的程序（或从本书网站下载第 29 课的版本），并修改代码以使用 LINQ 搜索文件。

1. 复制该程序相当简单。
2. 要使用 LINQ 搜索文件，请修改 Search 按钮的 Click 事件处理程序，使其如下所示。粗体行显示修改后的代码：

```
// Search for files matching the pattern
// and containing the target string.
private void searchButton_Click(object sender, EventArgs e)
{
    // Get the file pattern and target string.
    string pattern = patternComboBox.Text;
    string target = targetTextBox.Text.ToLower();

    // Search for the files.
    DirectoryInfo dirinfo =
        new DirectoryInfo(directoryTextBox.Text);
    var fileQuery =
        from FileInfo fileInfo
        in dirinfo.GetFiles(pattern,
            SearchOption.AllDirectories)
        where
        File.ReadAllText(fileInfo.FullName).ToLower().Contains(target)
        select fileInfo.FullName;
```
