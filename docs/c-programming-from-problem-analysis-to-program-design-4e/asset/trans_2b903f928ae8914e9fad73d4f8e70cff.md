
调用时使用的是 Student 类的一个对象。示例 4-15 展示了使用接受一个参数的构造函数实例化另一个 Student 对象（回顾示例 4-3）。示例 4-15 还演示了使用其属性为分数赋值，然后用该对象调用实例方法。这一次，CalculateAverage() 方法的返回值被传递给 WriteLine() 方法。

## 示例 4.15

```csharp
Student secondStudentObject = new Student("*2345*");
secondStudentObject.Score1 = 95;
secondStudentObject.Score2 = 62;
secondStudentObject.Score3 = 87;
Console.WriteLine("Student Number: " +
    secondStudentObject.StudentNumber +
    "\nAverage: {0:F1}",
    secondStudentObject.CalculateAverage());
```

注意，CalculateAverage() 方法不需要任何参数。这是因为 CalculateAverage() 是 Student 类的成员，可以完全访问 Student 类的所有数据成员。属性 Score1、Score2 和 Score3 具有公共访问模式。它们用于将值赋给私有实例数据成员 score1、score2 和 score3。

> **注意**
> 回想一下，要清除控制台窗口并将光标重新定位到显示区顶部，请调用 Console.Clear()。

## 测试新类

测试和使用你的类需要另一个不同的类。如果你按照前面的建议，将你的类作为第二个类添加到应用程序中，那么你已经有了那个类。这个类就是包含 Main() 的类。在这里的 Main() 中，你可以构造你的类的对象，使用属性赋值和检索值，并使用你构造的对象调用实例方法。示例 4-16 演示了如何测试你的类。

## 示例 4.16

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace StudentApp
{
    public class StudentApp
    {
        static void Main(string[] args)
        {
            Student firstStudentObject = new Student();
            firstStudentObject.StudentFirstName =
                AskForStudentName("First");
            firstStudentObject.StudentLastName =
                AskForStudentName("Last");
            firstStudentObject.StudentNumber = AskForStudentNumber();
            firstStudentObject.Major =
                AskForMajor(firstStudentObject.StudentFirstName);
            firstStudentObject.Score1 = AskForExamScore(1);
            firstStudentObject.Score2 = AskForExamScore(2);
            firstStudentObject.Score3 = AskForExamScore(3);

            Console.Clear();
            Console.WriteLine("First Student");
            Console.WriteLine(firstStudentObject.ToString());

            Student secondStudentObject = new Student("*2345*");
            secondStudentObject.Score1 = 95;
            secondStudentObject.Score2 = 62;
            secondStudentObject.Score3 = 87;
            Console.WriteLine("\n\nSecond Student");
            Console.WriteLine("Student Number: " +
                secondStudentObject.StudentNumber +
                "\nAverage: {0:F1}",
                secondStudentObject.CalculateAverage());

            Student thirdStudentObject = new
                Student("*5432*", "Randolph", "Wonder");
            thirdStudentObject.Major = "Math";
            thirdStudentObject.Score1 = 95;
            thirdStudentObject.Score2 = 87;
            thirdStudentObject.Score3 = 72;
            Console.WriteLine("\n\nThird Student");
            Console.WriteLine(thirdStudentObject);

            Student aStudentObject = new Student("*1234*", "Maria",
                "Smith", 97, 75,
                87, "CS");

            Console.WriteLine("\n\nLast Student");
            Console.WriteLine("Student Name: " +
                aStudentObject.StudentFirstName + " " +
                aStudentObject.StudentLastName +
                "\nStudent Number: " +
                aStudentObject.StudentNumber +
                "\nMajor: " + aStudentObject.Major +
                "\nExam Score 1: " + aStudentObject.Score1 +
                "\nExam Score 2: " + aStudentObject.Score2 +
                "\nExam Score 3: " + aStudentObject.Score3 +
                "\nExam Average: " +
                aStudentObject.CalculateAverage().ToString("F1"));
            Console.ReadKey();
        }

        public static int AskForExamScore(int whichOne)
        {
            string inValue;
            int aScore;
            Console.Write("Enter a value for Score {0}: ", whichOne);
            inValue = Console.ReadLine();
            aScore = int.Parse(inValue);
            return aScore;
        }

        public static string AskForStudentName(string whichOne)
        {
            string inValue;
            Console.Write("Enter Student {0} Name: ", whichOne);
            inValue = Console.ReadLine();
            return inValue;
        }

        public static string AskForMajor(string name)
        {
            string inValue;
            Console.Write("Enter {0}'s Major: ", name);
            inValue = Console.ReadLine();
            return inValue;
        }

        public static string AskForStudentNumber()
        {
            string inValue;
            Console.Write("Enter Student Number: ");
            inValue = Console.ReadLine();
            return inValue;
        }
    }
}
```

仔细查看示例 4-16。每个构造函数都经过了测试，并使用 Console.WriteLine() 方法显示值。在键入程序语句时，IntelliSense 会提供帮助，如图 4-4 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_252_0.png)

### 图 4-4 IntelliSense 显示可用的构造函数

除了如图 4-4 所示显示可用的构造函数方法外，一旦实例化对象，IntelliSense 还会显示该类的所有公共成员。查看图 4-5 时，请注意没有任何数据成员出现。

![](img/36e48639a06772bcb0fa1ea2525b33a3_252_1.png)

### 图 4-5 Student 类的公共成员

这些数据成员定义时使用的访问模式是 private。它们只能在 Student 类内部访问。你将在第 11 章进一步了解另外两种访问修饰符：protected 和 internal。internal 成员只能在同一程序集中的文件内访问。protected 成员可由任何派生自它们的类（子类）访问，但不能由任何其他类访问。第四种访问说明符 public 则没有访问限制。

StudentApp 类有许多从 Main() 调用的类方法。你会记得，类方法需要关键字 static，并且不与特定对象关联。它们被称为静态方法，是因为它们在编译时静态解析；因此不与任何特定对象数据实例关联。这些静态方法或类方法 AskForExamScore()、AskForStudentName()、AskForMajor() 和 AskForStudentNumber() 由 Main() 使用，以便用户输入数据。返回的值被赋给 firstStudentObject 的数据成员。然而，由于该类的数据成员定义为 private，因此必须使用公共属性来完成赋值。应用程序的输出如图 4-6 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_253_0.png)

查看示例 4-16 中的代码时，请注意 firstStudentObject 是通过显式调用 ToString() 方法显示的。第一个对象和第三个对象显示了相同类型的信息。两次都调用了 ToString()。回顾示例 4-16 中的代码时，请注意第三个对象是通过 Console.WriteLine(thirdStudentObject); 显示的。这里自动调用了 ToString() 方法。aStudentObject 也调用了 ToString()。这一次，它用于格式化 CalculateAverage() 方法返回的值。格式说明符 "F1" 作为参数发送。这里执行的是 double.ToString() 方法。

定义多类解决方案时，所有数据的输入和输出都应包含在具有 Main() 方法的类（文件）中。最终目标是将你的类文件（如 Student 和 CarpetCalculator）放入一个库中，以便这些类可供不同的应用程序使用。其中一些应用程序可能是 Windows 应用程序。有些可能是控制台应用程序。Web 应用程序也可以实例化你的类的对象。因此，绝不要在你的类方法中包含 ReadLine() 或 WriteLine()。这些方法只与控制台应用程序关联。

> **注意**
> 
> 始终在你定义的每个类中重写 ToString() 方法。这样，你就可以决定在打印对象时显示什么内容。

供你复习，Student 类中的代码显示在示例 4-17 中。
