
```csharp
using System.Linq;
using System.IO;

class CountSubstringsAhoCorasick
{
    static void Main()
    {
        DateTime startTime = DateTime.Now;

        // 读取输入的词汇列表
        string[] wordsOriginal = File.ReadAllLines("words.txt");
        string[] wordsLowercase = wordsOriginal.Select(w => w.ToLower()).ToArray();

        // 读取文本
        string text = File.ReadAllText("text.txt").ToLower();

        // 查找所有单词匹配项并计数
        var search = new AhoCorasickSearch();
        var matches = search.SearchAll(text, wordsLowerCase);
        Dictionary<string, int> occurrences = new Dictionary<string, int>();
        foreach (string word in wordsLowercase)
        {
            occurrences[word] = 0;
        }
        foreach (var match in matches)
        {
            string word = match.Match;
            occurrences[word]++;
        }

        // 打印结果
        using (StreamWriter result = File.CreateText("result.txt"))
        {
            foreach (string word in wordsOriginal)
            {
                result.WriteLine("{0} -> {1}", word, occurrences[word.ToLower()]);
            }
        }

        Console.WriteLine(DateTime.Now - startTime);
    }
}
```

# 第 26 章. 编程考试示例 – 主题 #3 1099

我们用已有的所有用例对上述代码进行了测试，它似乎**运行正常**。我们尝试了**性能测试**，这次我们对它的速度感到非常惊讶**：

```
00:00:00.6540374
```

**它运行得非常快。** 这是我们需要的解决方案，如果考试时允许使用互联网，那么当我们遇到标准常见问题时，最好的开始方式就是寻找现解决方案。

# 第 3 题：学校

在**学校**中学习的**学生**被分为不同的**小组**。每个小组都有有一位**老师**。学生保留了以下信息：名和姓。小组保留的信息包括：名称、学生列表和老师。老师保留的信息包括：名、姓以及他所教的小组列表。每位老师可以教多个小组。学校保留的信息包括：名称、老师列表、小组列表和学生列表。你的任务是：

- 1. **设计一组类**以及它们之间的关系，以对学校、学生、老师和小组进行建模。
- 2. **实现添加/编辑/删除** 老师、学生、小组及其属性的功能。
- 3. **实现以人类可读的格式打印**学校、老师、学生、小组及其属性的功能。
- 4. 编写一个**示例测试程序**，用于演示所实现的类和方法的功能。

带有学生和小组的学校示例：

```
School "Freedom". 老师: Tom Johnson, Elizabeth Hall. "English" 小组: David Russell, Nicholas Grant, Emma Fletcher, John Brown, Emily Cooper, 老师 Elizabeth Hall. "French" 小组: Kevin Simmons, Ian Hayes, 老师 Elizabeth Hall.
"Informatics" 小组: Jessica Carter, Andrew Cooper, Ashley Moore, Olivia Adams, Jonathan Smith, 老师 Tom Johnson.
```

# 开始思考

这是一个很好的考试作业示例，其目的是测试你使用**面向对象编程 (OOP)** 对现实世界问题进行**建模**的能力、设计类以及它们之间的关系，以及处理集合的能力。

要解决这个问题，我们只需要使用从“面向对象编程原理”章节中学获得的面向对象建模技能，特别是“面向对象建模 (OOM)”部分的内容。

# 构思解决方案

在这项任务中，没有复杂的逻辑需要发明。对于问题描述，我们必须定义每个类的属性（学校、老师、小组等），并实现能够以人类可读的格式打印的功能。遵循“面向对象建模 (OOM)”章节的指导，我们可以通过类来描述学校的情况。通过分析问题描述中的名词，我们可以创建 `Student`、`Group`、`Teacher` 和 `School` 类来测试想法。

# 检查想法

我们不需要检查或验证想法，以建模一个现实情况：学校的学生、老师和小组。

# 将问题划分为子问题

我们已经识别出的类实现可以被视为对学校建模问题的子问题。因此，我们有以下子问题：

- 学生类：具有名、姓，以及以人类可读的格式打印的方法。
- 小组类：具有名称、学生列表，以及以人类可读的格式打印的方法。
- 老师类：具有名、姓以及所教的小组列表，以及以人类可读的格式打印的方法。
- 学校类：具有名称、老师列表、小组列表和学生列表。

# 类 26. 编程考试示例 – 主题 #3 1101

- 测试类 – School：创建学校的学生和小组。最后，它将打印学校及其老师、学生。

# 思考数据结构

这个问题需要的数据结构主要分为两组：类以及类之间的关系。这里没有需要决定的。有趣的是描述类之间的关系，例如当一个小组有一个学生集合时。

可以使用数组可以通过索引访问元素，但一旦创建就无法添加或删除项（固定大小的数组）。这对于我们的问题是不方便的，因为我们不知道学校里有多少学生，在创建后还可以增加学生。

`List<T>` 似乎很好。它具有数组的优点，而且具有可变长度——易于添加或删除元素。`List<T>` 存储学生列表（学校和小组内部）、老师列表以及小组列表。

目前为止，`List<T>` 是处理对象聚合最合适的。例如哈希表——在这种情况下是不合适的，因为学校、老师、学生和小组不是键值对类型。如果我们需要根据唯一 ID 搜索学生，哈希表将是合适的。栈和队列等结构是不合适的，因为我们没有 LIFO 或 FIFO 行为。

“集合”结构及其实现 `HashSet<T>` 可以在我们需要键的唯一性时使用。这意味着 `HashSet<T>` 要求 T 类型的 `GetHashCode` 和 `Equals` 方法是正确的。我们应该使用集合吗？在哪里？为了回答这个问题，我们需要回顾问题描述。它是怎么说的？我们需要设计一组类来建模学校、老师和小组，并实现添加/编辑/删除老师、学生、小组及其属性的功能。简单的实现方法是在学校中持有学生列表，为每位老师持有小组列表。列表更容易实现。集合提供唯一性，但需要 `Equals()` 和 `GetHashCode()`。我们可以使用列表来简化我们的工作。

# 1102 使用 C# 的编程基础

它已经有了添加和删除元素的方法，并且元素可以通过索引访问并进行编辑。它已经胜任了。

最后，我们决定在类中所有的聚合操作都使用 `List<T>`，并将所有类成员作为具有读和写访问权限的属性暴露出来。我们没有充分理由限制对成员的访问或实现不可变行为。

# 实现：逐步步进

从 `Student` 类开始实现是合适的，因为它不依赖于任何其他类。

## 第 1 步：Student 类

在问题定义中，我们只有两个代表学生名和姓的字段。我们可以添加一个 `Name` 属性，它返回一个包含学生全名的字符串，并实现 `ToString()` 方法以以人类可读的格式打印学生。我们可以这样定义 `Student` 类：

```cs
Student.cs
public class Student
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public Student(string firstName, string lastName)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
    }

    public string Name
    {
        get {
            return this.FirstName + " " + this.LastName;
        }
    }

    public override string ToString()
    {
        return "Student: " + this.Name;
    }
}
```

# 第 26 章 示例编程考试 – 主题 #3

我们希望类成员是可编辑的，因此我们将 `FirstName` 和 `LastName` 定义为公共的读写属性。

## 测试 Student 类

在继续之前，我们想要测试 `Student` 类以确保它是正确的。让我们创建一个带有 `Main()` 方法的测试类，在其中创建一个学生并打印该学生：

```cs
class TestSchool
{
    static void Main()
    {
        Student studentPeter = new Student("Peter", "Lee");
        Console.WriteLine(studentPeter);
    }
}
```

我们运行测试程序并得到了正确的结果：

Student: Peter Lee

现在我们可以继续实现其他类了。

## 第 2 步：Group 类

我们可以定义的下一个类是 `Group`。我们选择它是因为它的定义唯一需要的类是 `Student` 类。我们将定义的属性是：小组名称、属于该小组的学生列表，以及一个教授该小组的老师。为了实现学生列表，我们将使用 `List<Student>`。我们将在 `Group`类的实现中添加一个 `ToString()` 方法：

```cs
Group.cs
using System.Collections.Generic;
public class Group
{
    public string Name { get; set; }
    public List<Student> Students { get; set; }

    public Group(string name)
    {
        this.Name = name;
        this.Students = new List<Student>();
    }

    public override string ToString()
    {
        StringBuilder groupAsString = new StringBuilder();
        groupAsString.AppendLine("Group name: " + this.Name);
        groupAsString.Append("Students in the group: " + this.Students);
        return groupAsString.ToString();
    }
}
```

创建一个小组时，为它分配一个空的学生列表是非常重要的。如果我们不对学生列表赋值，当我们尝试添加学生时，它将为 `null`，导致会导致异常。

## 测试 Group 类

现在让我们测试 `Group` 类。创建一个示例小组，向其中添加几个学生并在控制台上打印该小组：

```cs
static void Main()
{
    Student studentPeter = new Student("Peter", "Lee");
    Student studentMaria = new Student("Maria", "Steward");
    Group groupEnglish = new Group("English language course");
    groupEnglish.Students.Add(studentPeter);
    groupEnglish.Students.Add(studentMaria);
    Console.WriteLine(groupEnglish);
}
```

我们运行上面的测试代码并发现了一个 bug：

| Group name: English language course |

| Students in the group |

| System.Collections.Generic.List`1[Student] |

似乎学生列表的打印不正确。很容易找到原因。`List<T>` 类没有正确实现 `ToString()`，我们需要另一种方法来打印学生列表。我们可以通过 `for` 循环来实现，但让我们尝试一种更短、更优雅的方法：

```cs
using System.Linq;
...
groupAsString.Append("Students in the group: " + string.Join(",", this.Students.Select(s => s.Name)));
```

# 第 26 章 示例编程考试 – 主题 #3

上面的代码使用了扩展方法和 Lambda 表达式来将所有学生的姓名选择为 `IEnumerable<string>`，然后用逗号分隔符将它们组合成字符串。修复后再次测试 `Group` 类：

| Group name: English language course |

| Students in the group: Peter Lee, Maria Steward |

`Group` 类现在工作正常了。

让我们思考一下：是谁在教小组里的学生？我们应该有一个老师，对吧。让我们尝试添加最简单的 `Teacher` 类，并在 `Group` 类中定义它的属性：

```cs
public class Teacher {
    public string FirstName { get; set; }
    public string LastName { get; set; }
}

public class Group {
    public string Name { get; set; }
    public List<Student> Students { get; set; }
    public Teacher Teacher { get; set; }

    public Group(string name)
    {
        this.Name = name;
        this.Students = new List<Student>();
    }

    public override string ToString()
    {
        StringBuilder groupAsString = new StringBuilder();
        groupAsString.AppendLine("Group name: " + this.Name);
        groupAsString.Append("Students in the group: " + string.Join(",", this.Students.Select(s => s.Name)));
        if (this.Teacher != null)
        {
            groupAsString.Append("\ngroup teacher: " + this.Teacher.Name);
        }
        return groupAsString.ToString();
    }
}
```

```csharp
string.Join(", ", this.Groups.Select(s => s.Name));
return teacherAsString.ToString();
}
```

就像 `Group` 类一样，创建一个空的分组列表比让 `Groups` 属性未初始化要重要。

## 测试 Teacher 类

在继续下去之前，让我们测试一下 `Teacher` 类。我们可以创建一个包含几个小组的教师并在控制台中打印出它：

```csharp
static void Main()
{
    Teacher teacherNatasha = new Teacher("Natasha", "Walters");
    Group groupEnglish = new Group("English language");
    Group groupFrench = new Group("French language");
    teacherNatasha.Groups.Add(groupEnglish);
    teacherNatasha.Groups.Add(groupFrench);
    Console.WriteLine(teacherNatasha)
}
```

结果是正确的：

Teacher name: Natasha Walters

Groups of this teacher: English language, French language
