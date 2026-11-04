

![](img/3f5ef6be1748bb746e5f71a483bba4d0_266_0.png)

Fig. 8.20 | 使用二维数组的 GradeBook 输出。(第 2 部分，共 2 部分。)

```csharp
// Fig. 8.21: GradeBook.cs
// Grade book using a rectangular array to store grades.
using System;

class GradeBook
{
    private int[,] grades; // rectangular array of student grades

    // auto-implemented property CourseName
    public string CourseName { get; }

    // two-parameter constructor initializes
    // auto-implemented property CourseName and grades array
    public GradeBook(string name, int[,] gradesArray)
    {
        CourseName = name; // set CourseName to name
        grades = gradesArray; // initialize grades array
    }

    // display a welcome message to the GradeBook user
    public void DisplayMessage()
    {
        // auto-implemented property CourseName gets the name of course
        Console.WriteLine(
            $"Welcome to the grade book for\n{CourseName}!\n");
    }

    // perform various operations on the data
    public void ProcessGrades()
    {
        // output grades array
        OutputGrades();

        // call methods GetMinimum and GetMaximum
        Console.WriteLine(
            $"\nLowest grade in the grade book is {GetMinimum()}\n" +
            $"Highest grade in the grade book is {GetMaximum()}\n");

        // output grade distribution chart of all grades on all tests
        OutputBarChart();
    }
}
```

Fig. 8.21 | 使用矩形数组存储成绩的 GradeBook。(第 1 部分，共 4 部分。)

```csharp
// find minimum grade
public int GetMinimum()
{
    // assume first element of grades array is smallest
    var lowGrade = grades[0, 0];

    // loop through elements of rectangular grades array
    foreach (var grade in grades)
    {
        // if grade less than lowGrade, assign it to lowGrade
        if (grade < lowGrade)
        {
            lowGrade = grade;
        }
    }

    return lowGrade; // return lowest grade
}

// find maximum grade
public int GetMaximum()
{
    // assume first element of grades array is largest
    var highGrade = grades[0, 0];

    // loop through elements of rectangular grades array
    foreach (var grade in grades)
    {
        // if grade greater than highGrade, assign it to highGrade
        if (grade > highGrade)
        {
            highGrade = grade;
        }
    }

    return highGrade; // return highest grade
}

// determine average grade for particular student
public double GetAverage(int student)
{
    // get the number of grades per student
    var gradeCount = grades.GetLength(1);
    var total = 0.0; // initialize total

    // sum grades for one student
    for (var exam = 0; exam < gradeCount; ++exam)
    {
        total += grades[student, exam];
    }
}
```

```csharp
// return average of grades
return total / gradeCount;
}

// output bar chart displaying overall grade distribution
public void OutputBarChart()
{
    Console.WriteLine("Overall grade distribution:");

    // stores frequency of grades in each range of 10 grades
    var frequency = new int[11];

    // for each grade in GradeBook, increment the appropriate frequency
    foreach (var grade in grades)
    {
        ++frequency[grade / 10];
    }

    // for each grade frequency, display bar in chart
    for (var count = 0; count < frequency.Length; ++count)
    {
        // output bar label ("00-09: ", ..., "90-99: ", "100: ")
        if (count == 10)
        {
            Console.Write(" 100: ");
        }
        else
        {
            Console.Write($"{count * 10:D2}-{count * 10 + 9:D2}: ");
        }

        // display bar of asterisks
        for (var stars = 0; stars < frequency[count]; ++stars)
        {
            Console.Write("*");
        }

        Console.WriteLine(); // start a new line of output
    }
}

// output the contents of the grades array
public void OutputGrades()
{
    Console.WriteLine("The grades are:\n");
    Console.Write(" "); // align column heads

    // create a column heading for each of the tests
    for (var test = 0; test < grades.GetLength(1); ++test)
    {
        Console.Write($"Test {test + 1} ");
    }
}
```

```csharp
Console.WriteLine("Average"); // student average column heading
// create rows/columns of text representing array grades
for (var student = 0; student < grades.GetLength(0); ++student)
{
    Console.Write($"Student {student + 1,2}");
    // output student's grades
    for (var grade = 0; grade < grades.GetLength(1); ++grade)
    {
        Console.Write($"{grades[student, grade],8}");
    }
    // call method GetAverage to calculate student's average grade;
    // pass row number as the argument to GetAverage
    Console.WriteLine($"{GetAverage(student):9:F1}");
}
```

## Fig. 8.21 | 使用矩形数组存储成绩的 GradeBook。(第 4 部分，共 4 部分。)

五个方法执行数组操作来处理成绩。每个方法都与其在图 8.15 中的对应方法相似。方法 GetMinimum（图 8.21 中的第 44–60 行）确定任何学生的最低成绩。方法 GetMaximum（第 63–79 行）确定任何学生的最高成绩。方法 GetAverage（第 82–96 行）确定特定学生的学期平均成绩。方法 OutputBarChart（第 99–133 行）输出整个学期所有学生成绩分布的条形图。方法 OutputGrades（第 136–164 行）以表格格式输出二维数组，并附带每个学生的学期平均成绩。

## 使用 foreach 语句处理二维数组

方法 GetMinimum、GetMaximum 和 OutputBarChart 各自使用 foreach 遍历数组 grades——例如方法 GetMinimum 中的第 50–57 行。为了找到整体最低成绩，此 foreach 语句遍历矩形数组 grades 并将每个元素与变量 lowGrade 进行比较。如果某个成绩小于 lowGrade，则 lowGrade 被设为该成绩。

当 foreach 语句遍历数组 grades 的元素时，它按索引顺序查看第一行的每个元素，然后按索引顺序查看第二行的每个元素，以此类推。foreach 语句（第 50–57 行）遍历 grades 的元素顺序与以下使用嵌套 for 语句表示的等效代码相同：

```csharp
for (var row = 0; row < grades.GetLength(0); ++row)
{
    for (var column = 0; column < grades.GetLength(1); ++column)
    {
        if (grades[row, column] < lowGrade)
        {
            lowGrade = grades[row, column];
        }
    }
}
```

当 foreach 语句完成后，lowGrade 包含矩形数组中的最低成绩。方法 GetMaximum 的工作方式与方法 GetMinimum 类似。请注意使用 foreach 与前面嵌套 for 语句的简洁性。

> > **软件工程观察 8.2**
> >
> > *“保持简单”是对你编写的大多数代码的良好建议。*

## *方法 OutputBarChart*

方法 OutputBarChart（第 99–133 行）以条形图的形式显示成绩分布。foreach 语句（第 107–110 行）的语法对于一维和二维数组是相同的。

## *方法 OutputGrades*

方法 OutputGrades（第 136–164 行）使用嵌套 for 语句输出成绩值，以及每个学生的学期平均成绩。图 8.20 中的输出显示了结果，其类似于教师实体成绩簿的表格格式。图 8.21 中的第 142–145 行显示每个测试的列标题。我们在此使用 for 语句而不是 foreach 语句，以便可以用数字标识每个测试。同样，第 150–163 行中的 for 语句首先使用计数器变量输出行标签以标识每个学生（第 152 行）。尽管数组索引从 0 开始，但第 144 行和第 152 行分别输出 test + 1 和 student + 1，以生成从 1 开始的测试和学生编号（参见图 8.20）。图 8.21 中第 155–158 行的内部 for 语句使用外部 for 语句的计数器变量 student 遍历数组 grades 的特定行并输出每个学生的测试成绩。最后，第 162 行通过将 grades 的行索引（即 student）传递给方法 GetAverage 来获取每个学生的学期平均成绩。

## *方法 GetAverage*

方法 GetAverage（第 82–96 行）接受一个参数——特定学生的行索引。当第 162 行调用 GetAverage 时，参数是 int 值 student，它指定矩形数组 grades 的特定行。方法 GetAverage 计算该行数组元素的总和，将总数除以测试结果的数量，并将浮点结果作为 double 值返回（第 95 行）。

## *演示类 GradeBook 的类 GradeBookTest*

图 8.22 使用 gradesArray 引用的整型二维数组（图 8.22，第 9–18 行）创建类 GradeBook（图 8.21）的对象。第 20–21 行将课程名称和 gradesArray 传递给 GradeBook 构造函数。然后第 22–23 行分别调用 myGradeBook 的 DisplayMessage 和 ProcessGrades 方法，以显示欢迎消息并获取汇总学期学生成绩的报告。

```csharp
    // Fig. 8.22: GradeBookTest.cs
    // Create a GradeBook object using a rectangular array of grades.
    class GradeBookTest
    {
```

Fig. 8.22 | 使用矩形数组创建 GradeBook 对象。(第 1 部分，共 2 部分。)

