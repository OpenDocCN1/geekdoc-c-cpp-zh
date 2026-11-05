

- 19. 给定以下任务，哪个是最合适的方法头？一个方法接收三个整数作为输入。这些值代表成绩。它们在方法中应不可更改。该方法应返回带有小数部分的平均值。
  - a. `static double DetermineGrade(int grade1, int grade2, int grade3)`
  - b. `static int DetermineGrade(int grade1, int grade2, int grade3)`
  - c. `static int int int DetermineGrade(double finalAverage)`
  - d. `static double DetermineGrade(ref int grade1, ref int grade2, ref int grade3)`
  - e. `static void DetermineGrade()`

- 20. 给定以下任务，哪个是最合适的方法头？已计算出 taxAmount 和 totalSales 的结果。编写一个方法头，接受这些值作为输入用于显示。
  - a. `public static DisplayResults()`
  - b. `public DisplayResults(double)`
  - c. `public static void DisplayResults()`
  - d. `public static void DisplayResults(double taxAmount, double totalSales)`
  - e. `public static void DisplayResults(taxAmount, totalSales)`

- 21. 使用以下方法头回答下面的问题：

```csharp
public static int DetermineResult(int value1, ref double value2)
public static void DisplayResult(int value1, double value2)
public static int GetValue()
```

  - a. 每个方法有多少个参数？
  - b. 每个方法的返回类型是什么？
  - c. 上述哪些方法的主体中会有 return 语句？

- 22. 编写方法实现以下功能：
  - a. 在屏幕上显示三整行星号。
  - b. 接受你的年龄作为参数，显示该值并附上适当的标签。
  - c. 接受两个浮点值作为参数。显示这些值，并格式化为小数点后三位。
  - d. 接受三个 `int` 参数并返回它们的和。
  - e. 不接受参数且不返回任何值。将一个局部 Boolean 变量初始化为 `true`。让该方法打印该 Boolean 的值。

- 23. 以下预定义的 `Math` 类方法调用将产生什么结果？
  - a. `Console.WriteLine(Math.Abs(-98887.234));`
  - b. `Console.WriteLine(Math.Pow(4,3));`
  - c. `Console.WriteLine(Math.Sign(-56));`
  - d. `Console.WriteLine(Math.Sqrt(81));`
  - e. `Console.WriteLine(Math.Min(-56, 56));`

- 24. 以下程序存在若干语法错误以及风格不一致。纠正语法错误并指出风格违规之处。

```csharp
/* ********************************************
 * AgeIncrementer.cs                       Author: Doyle
 * Prompts the users for their ages in
 * a class method. Prints the value
 * entered back in the Main() method.
 */

using System;

namespace AgeExample
{
    public class AgeIncrementer
    {
        public static void Main()
        {
            int AGE;
            string aValue;

            age = GETAge(aValue);
            Console.WriteLine("Your age next year will be {0}",
                              ++age);
            Console.Read();
        }

        public static GETAge()
        {
            Console.Write("Enter your age: ");
            aValue = Console.ReadLine();
            age = int.Parse(aValue);
            return int AGE;
        }
    }
}
```

## 编程练习

- 1. 编写一个应用程序，除 `Main()` 方法外还包含两个额外的方法。一个方法应返回一个由四五行关于你所在学校的信息组成的字符串。另一个方法应返回一个由星号组成的字符串。首先调用返回星号字符串的方法。在调用显示学校信息的方法之后，再次调用返回星号的方法。可以包含的项目有学校名称、在校学生人数和学校校色。包含适当的标签。显示效果应当美观，因此要包含足够的星号以环绕你的列表。

- 2. 设计一个消息显示应用程序。允许用户在一个方法中输入他们的姓名和最喜欢的谚语，该方法被调用两次。第一次调用该方法时要求输入人名。发送一个字符串参数，指示应输入什么值。第二次调用该方法以获取最喜欢的谚语。将字符串值返回给 `Main()` 方法。调用另一个方法，传入姓名和谚语。在该方法中，显示包含人名及其谚语的消息，并用大于/小于符号（<>><<>><>）的行环绕。

- 3. 编写一个应用程序，允许用户输入矩形的宽度和高度，并输出面积和周长。使用方法来输入数值、执行计算和显示结果。结果应格式化并以表格形式打印。

- 4. 设计一个使用方法的应用程序，将整数秒数转换为等效的小时、分钟和秒数。使用方法来输入初始秒数、执行计算和显示结果。结果应格式化并以表格形式打印。

- 5. 编写一个程序，将华氏温度转换为摄氏温度。允许用户输入原始的华氏温度值。显示原始温度和格式化后的转换值。使用适当的方法进行输入、计算和输出结果。

- 6. 编写一个程序，用于将米转换为英尺和英寸。允许用户在方法中输入公制米值。为你的解决方案编写适当的方法。

- 7. 编写一个程序，用于确定应添加到餐厅账单中的小费金额。允许用户输入税前总额和小费百分比（15% 或 20%）。输出显示计算值，包括 15% 和 20% 小费下的应付总额。在确定小费之前，应先将 9% 的税添加到账单中。为你的解决方案编写适当的方法。

- 8. 编写一个程序，计算计算机俱乐部从其格兰诺拉燕麦棒销售项目中获得的收益金额。允许用户输入售出的箱数和每根燕麦棒的售价。每箱包含 12 根燕麦棒；每箱以 $5.00 从当地供应商处购买。俱乐部需要将收益的 10% 交给学生会。以货币格式显示他们的收益。为你的解决方案编写适当的方法。

- 9. 编写一个程序，计算并打印佣金制销售员工的实得工资。允许用户输入员工姓名和本周的销售金额。员工获得总销售额的 7%。联邦税率为 18%。退休金缴款为 15%。社会保障税率为 9%。使用适当的常量。编写输入、显示和计算方法。最终输出应显示所有计算值，包括总扣除额和所有定义的常量。

- 10. 编写一个应用程序，帮助土地所有者确定他们当年的房产税。税费基于房产的评估价值和年度千分税率。当前年度的既定千分税率为每 $1000 价值 $10.03。房主可获得 $25,000 的税收减免，这意味着他们可以在计算应税价值之前从评估价值中减去 $25,000。允许用户输入房产地址和上一年度的评估价值。镇政府已决定将本年度所有房产的评估价值提高 2.7%，以增加学校预算项目的额外资金。提供计算并返回新评估价值和本年度拟定税费的方法。再提供另一个显示格式化值的方法。

