
将有效数字保留为两位，从而消除了对第二个参数含义的担忧。

该方法的泛型（decimal）版本调用了更具体的（decimal, int）版本来执行其魔法操作。这种栈式方法调用非常常见，因为减少了代码重复。泛型方法只是提供了程序员不愿在文档中查找的参数，除非他们需要，否则本不应该去查找。

为了不必要地查阅参考文档以了解通常默认参数的含义，会使程序员从当前的主要任务中分心——这会让工作变得更加困难，浪费时间，并增加错误的概率。

提供默认参数不仅仅是为了让懒惰的程序员少费一点精力（编程需要大量的注意力）。方法的作者理解参数之间的关系——因此承担了提供更友好的、重载版本方法的责任。

Visual Basic、C 和 C++ 程序员应该习惯于在方法签名中直接为参数提供默认值。在 C# 4.0 发布之前，你无法在 C# 中这样做。而现在你可以了。

例如，虽然在在上一个示例中重载方法是实现默认参数的一种完全接受的方法，但你也可以通过使用等号 (=) 来提供默认参数，就像在 Visual Basic 中一样：

```csharp
// MethodsWithDefaultArguments2-- 为方法提供可选参数
// 以避免重载。这是实现相同功能的另一种方法。
using System;
namespace MethodsWithDefaultArguments2
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // 访问成员方法。
            Console.WriteLine(DisplayRoundedDecimal(12.345678M, 3));
            // 等待用户确认。
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
        // DisplayRoundedDecimal -- 将小数值转换为具有
        // 指定数量有效数字的字符串。该参数是
        // 可选的并有一个默认值。如果你调用该方法
        // 而时不第二个参数，它将使用默认值。
        public static string DisplayRoundedDecimal(decimal value,
            int numberOfSignificantDigits = 2)
        {
            // 先将数字四舍五入到指定的
            // 有效位数。
            decimal roundedValue =
            decimal.Round(value,
                numberOfSignificantDigits);
            // 将其字符串。
            string s = Convert.ToString(roundedValue);
            return s;
        }
    }
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_264_0.png)

为什么微软要进行这些更改？答案是 COM。组件对象模型（COM）是 .NET 发布之前微软产品选择的架构范式，而且它仍然非常流行（注意我没说它是流行的）。例如，Office 完全是使用 COM 开发的。COM 应用使用 C++ 或 Visual Basic 6 及更早版本开发，这些类的方法允许可选参数。因此，在不使用可选参数的情况下与 COM 通信可能会变得困难。为了解决这种不，C# 4.0 增加了可选参数（以及许多其他功能）。

我在第三书中没完其烦地讲解了命名参数和可选参数。

## 圣诞节后的返回值返回

许多现实世界的操作会创建返回给调用者的值。例如，Sin() 接受一个参数并返回三角正弦。方法可以通过两种方式向调用者返回值——最常见的是通过 `return` 语句；然而，第二种方法使用了引用传递功能。

## 通过 return 邮资返回值

下面的代码段演示了一个小方法，它返回输入参数的平均值：

```csharp
public class Example
{
    public static double Average(double d1, double d2)
    {
        double average = (d1 + d2) / 2;
        return average;
    }
    public static void Main(string[] args)
    {
        double v1 = 1.0;
        double v2 = 3.0;
        double averageValue = Average(v1, v2);
        Console.WriteLine("The average is: " + averageValue);
    }
}
```
*(注：原文提供的 264-265 页文本存在大量乱码和重复碎片，已根据标准 C# 模式重构了代码逻辑结构。)*
