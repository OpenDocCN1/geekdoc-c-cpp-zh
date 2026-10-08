

## 342 查看一个**可以作为示例的**程序

类通过实现 `CompareTo()` 方法来实现 `Comparable<T>` 接口。注意 `CompareTo()` 接收一个类型为 `T` 的参数，这是你在为特定数据类型实例化接口时提供的类型——如本例所示：

```sharp
class SoAndSo : Comparable<SoAndSo> // 使我变得可比较。
```

这听起来有点像达尔文主义，但你可以说，如果一个 `Student` 对象的平均学分更高，那么它就“大于”另一个 `Student` 对象。（好吧，无论是一个更优秀的学生，还是一个更会拍马的人——这并不重要。）

实现 `CompareTo()` 方法意味着对象具有排序顺序。如果一个学生“大于”另一个学生，你必须能够将学生从“最小”到“最大”进行排序。事实上，大多数集合类（包括数组但不包括字典）都提供类似下面所示的 `Sort()` 方法：

```sharp
void Sort(Comparable<T> objects) {
```

此方法对实现了 `Comparable<T>` 接口的对象集合进行排序。这些对象属于哪个类并不重要。例如，它们可以是 `Student` 对象。像数组或 `List<T>` 这样的集合类甚至可以排序这个版本的 `Student`：

```sharp
// Student -- 带有名字和成绩的学生
class Student : Comparable<Student>, IDisplayable
{
    // 构造函数 -- 初始化一个新的学生对象。
    public Student(double grade)
        { Grade = grade;
    public double Grade { get; private set; }
    // 实现 Comparable<T> 接口：
    public int CompareTo(Student other)
    {
        // 比较另一个对象（在此类中为 Student 对象）并
        // 决定哪一个在排序中排在另一个后面。
        Student rightStudent = other;
        
        // 将当前的学生（设为 'left'）与另一个
        // 学生（设为 'right'）进行比较。
        Student leftStudent = this;

        // 现在根据排序标准（学生的成绩）生成 -1, 0 或 1。
        // 我也可以使用 Double 类的 CompareTo() 方法。
        {
            if (rightStudent.Grade < leftStudent.Grade)
                return -1;
        }
}
}
}
```

## 查看一个**可以作为示例的**程序 343

```sharp
if (rightStudent.Grade > leftStudent.Grade)
    return 1;
else
    return 0;
```

对 Students 数组进行排序被简化为这一个调用：

```sharp
void MyMethod(Student[] students) // Student 实现了 IComparable<T>
    Array.Sort(students); // 排序 IComparable<Student> 数组
```

你提供比较器（`CompareTo()`），而 `Array` 完成所有工作——对我来说这很公平。

## 整合一切

这是你一直等待的时刻：一个使用了本章之前描述的特完整接口程序：

```sharp
// 接口 -- 展示了如何使用接口概念
// 在类的类的构和实现中提供更增强的// 灵活性。
using System;
namespace SortInterface
{
    // IDisplayable -- 一个可以将自己转换为可显示
    // 字符串格式的对象（重复了通过重写
    // ToString() 可以实现的功能，这有助于我说明观点）
    interface IDisplayable
    {
        // Display -- 返回你自己的字符串表示。
        string Display();
    }
    class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("正在排序学生列表:");
            // 获取一个无序的学生数组。
            Student[] students = Student.CreateStudentList();
            // 使用 IComparable<T> 接口对数组排序。
            Array.Sort(students);
            // 现在使用 IDisplayable 接口显示结果
            DisplayArray(students);

            // 现在使用相同的例程按名称对鸟数组排序
            // 尽管 Bird 和 Student 类没有共同的基类。
            Console.WriteLine("正在排序鸟列表:");
            Bird[] birds = Bird.CreateBirdList();
            // 注意，没有将对象显式转换为
            // IDisplayables 数组（对于 Students 也是如此）
            Array.Sort(birds);
            DisplayArray(birds);
            // 等待用户确认结果。
            Console.WriteLine("按回车键退出...");
            Console.Read();
        }

        // DisplayArray -- 显示一个实现了
        // IDisplayable 接口的对象数组。
        public static void DisplayArray(IDisplayable[] displays)
        {
            foreach (IDisplayable displayable in displays)
            {
                Console.WriteLine("*", displayable.Display());
            }
        }

        // Students -- 按成绩排序学生
        // Student -- 带有名字和成绩的学生
        class Student : IComparable<Student>, IDisplayable
        {
            // 构造函数 -- 初始化新对象。
            public Student(string name, double grade)
            {
                Name = name;
                grade = grade;
            }
            // CreateStudentList -- 为了节省空间返回学生列表。
            static string[] names = { "Peter", "Marge", "Bart", "Maggie" };
            static double[] grades = { 85, 100, 30 };
            public static Student[] CreateStudentList()
            {
                Student[] students = new Student[names.Length];
                for (int i = 0; i < names.Length; i++)
                {
                    students[i] = new Student(names[i], grades[i]);
                }
                return students;
            }
            // 只读属性。
            public string Name { get; private set; }
            public double Grade { get; private set; }
            // 实现 IComparable<T> 接口
            public int CompareTo(Student other)
            {
                // 比较另一个对象（在此类中为 Student 对象）并
                // 决定哪一个在排序中排在另一个后面。
                Student rightStudent = other;
                // 将当前的学生（设为 'left'）与另一个
                // 学生（设为 'right'）进行比较。
                Student leftStudent = this;
                // 现在根据排序标准（学生的成绩）生成 -1, 0 或 1。
                // 我也可以使用 Double 类的 CompareTo() 方法。
                if (rightStudent.Grade < leftStudent.Grade)
                    return -1;
                if (rightStudent.Grade > leftStudent.Grade)
                    return 1;
                else
                    return 0;
            }
            // Display -- 实现 IDisplayable 接口：
            public string Display()
            {
                string padName = Name.PadRight(9);
                return String.Format("{0}: {1}", padName, Grade);
            }
        }

        // 按名称排序鸟
        // Bird -- 仅仅鸟的名字数组。
        class Bird : IComparable<Bird>, IDisplayable
        {
            // 构造函数 -- 初始化一个新的 Bird 对象。
            public Bird(string name) {}
            // CreateBirdList -- 向调用者返回鸟列表；
            static string[] _birdNames = { "Robin", "Cardinal", "Bluejay", "Finch", "Sparrow" };
            public static Bird[] CreateBirdList()
            {
                Bird[] birds = new Bird[_birdNames.Length];
                for (int i = 0; i < _birdNames.Length; i++)
                {
                    birds[i] = new Bird(_birdNames[i]);
                }
                return birds;
            }
            public string Name { get; set; }
            // 实现 IDisplayable 接口：
            // 按名称比较鸟；使用内置的
            // String.Compare 方法。
            public int CompareTo(Bird right)
            {
                // 将“当前”鸟与“右对象”鸟进行比较。
                Bird leftBird = this;
                return String.Compare(leftBird.Name, right.Name);
            }
            // Display -- 实现 IDisplayable 接口。
            public string Display()
            {
                return Name;
            }
        }
    }
}
```
