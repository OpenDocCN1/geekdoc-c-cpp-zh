

```
class MathOperations
{
    public static double MultiplyByTwo(double value) => value * 2;
    public static double Square(double value) => value * value;
}
```

你可以按如下方式调用这些方法（代码文件 SimpleDelegate/Program.cs）：

```
using static System.Console;

namespace Wrox.ProCSharp.Delegates
{
    delegate double DoubleOp(double x);

    class Program
    {
        static void Main()
        {
            DoubleOp[] operations =
            {
                MathOperations.MultiplyByTwo,
                MathOperations.Square
            };

            for (int i=0; i < operations.Length; i++)
            {
                WriteLine($"Using operations[{i}]:");
                ProcessAndDisplayNumber(operations[i], 2.0);
                ProcessAndDisplayNumber(operations[i], 7.94);
                ProcessAndDisplayNumber(operations[i], 1.414);
                WriteLine();
            }
        }

        static void ProcessAndDisplayNumber(DoubleOp action, double value)
        {
            double result = action(value);
            WriteLine($"Value is {value}, result of operation is {result}");
        }
    }
}
```

在这段代码中，你实例化了一个 `DoubleOp` 委托数组（请记住，定义了一个委托类之后，基本上就可以像普通类一样实例化它的实例，所以把一些实例放到数组中是没有问题的）。数组中的每个元素都被初始化为引用 `MathOperations` 类实现的不同操作。然后，你遍历这个数组，将每个操作应用于三个不同的值。这展示了委托的一种使用方式——将方法分组到数组中，以便在循环中调用多个方法。

这段代码中的关键行是实际将每个委托传递给 `ProcessAndDisplayNumber` 方法的那些行，例如：

```
ProcessAndDisplayNumber(operations[i], 2.0);
```

上面的代码传入了一个委托的名称，但没有带任何参数。鉴于 `operations[i]` 是一个委托，从语法上讲：

- `operations[i]` 表示*委托*（即由该委托所表示的方法）
- `operations[i](2.0)` 表示*实际调用这个方法，并把括号中的值传进去*

`ProcessAndDisplayNumber` 方法被定义为将委托作为其第一个参数：

```
static void ProcessAndDisplayNumber(DoubleOp action, double value)
```

然后，在该方法内部，你调用：

```
double result = action(value);
```

这实际上会调用被 `action` 委托实例所包装的方法，并将其返回值存储在 `result` 中。运行这个示例会得到以下结果：

```
SimpleDelegate
Using operations[0]:
Value is 2, result of operation is 4
Value is 7.94, result of operation is 15.88
Value is 1.414, result of operation is 2.828

Using operations[1]:
Value is 2, result of operation is 4
Value is 7.94, result of operation is 63.0436
Value is 1.414, result of operation is 1.999396
```

## Action\<T\> 与 Func\<T\> 委托

与其为每个参数和返回类型定义一个新的委托类型，你可以使用 `Action<T>` 和 `Func<T>` 委托。泛型 `Action<T>` 委托用于引用具有 `void` 返回类型的方法。这个委托类有不同的变体，以便你可以传递多达 16 种不同的参数类型。不带泛型参数的 `Action` 类用于调用没有参数的方法。`Action<in T>` 用于调用带一个参数的方法；`Action<in T1, in T2>` 用于调用带两个参数的方法；`Action<in T1, in T2, in T3, in T4, in T5, in T6, in T7, in T8>` 用于调用带八个参数的方法。

`Func<T>` 委托可以用类似的方式使用。`Func<T>` 允许你调用具有返回类型的方法。与 `Action<T>` 类似，`Func<T>` 也有不同的变体，可以传递多达 16 种参数类型以及一种返回类型。`Func<out TResult>` 是用于调用具有返回类型且无参数的方法的委托类型。`Func<in T, out TResult>` 用于带一个参数的方法，而 `Func<in T1, in T2, in T3, in T4, out TResult>` 用于带四个参数的方法。

前一节的示例声明了一个带 double 参数和 double 返回类型的委托：

```
delegate double DoubleOp(double x);
```

与其声明自定义委托 `DoubleOp`，你可以使用 `Func<in T, out TResult>` 委托。你可以声明一个该委托类型的变量，或者像这里所示，声明一个该委托类型的数组：

```
Func<double, double>[] operations =
{
    MathOperations.MultiplyByTwo,
    MathOperations.Square
};
```

并将其作为参数与 `ProcessAndDisplayNumber` 方法一起使用：

```
static void ProcessAndDisplayNumber(Func<double, double> action, double value)
{
    double result = action(value);
    WriteLine($"Value is {value}, result of operation is {result}");
}
```

## BubbleSorter 示例

现在你已经准备好来看一个能够真正展示委托实用价值的示例。你将编写一个名为 `BubbleSorter` 的类。该类实现一个静态方法 `Sort`，该方法将对象数组作为其第一个参数，并将该数组重新排列为升序。例如，如果你传入这样一个 int 数组 {0, 5, 6, 2, 1}，它会将该数组重新排列为 {0, 1, 2, 5, 6}。

冒泡排序算法是一种众所周知且非常简单的数字排序方法。它最适合于小规模数字集合，因为对于较大规模的数字集合（超过大约 10 个），有高效得多的算法可用。它的工作方式是反复循环遍历数组，比较每对数字，并在必要时交换它们，从而使最大的数字逐渐向数组末尾移动。对于 int 排序，执行冒泡排序的方法可能类似于下面这样：

```
bool swapped = true;
do
{
    swapped = false;
    for (int i = 0; i < sortArray.Length-1; i++)
    {
        if (sortArray[i] > sortArray[i+1]) // problem with this test
        {
            int temp = sortArray[i];
            sortArray[i] = sortArray[i + 1];
            sortArray[i + 1] = temp;
            swapped = true;
        }
    }
} while (swapped);
```

这对于 int 来说没问题，但你希望你的 `Sort` 方法能够对任意对象进行排序。换句话说，如果某些客户端代码向你传递一个 `Currency` 结构体数组，或者其他任何它可能定义的类或结构体的数组，你需要能够对该数组进行排序。这在前面的代码行 `if (sortArray[i] > sortArray[i+1])` 中带来了一个问题，因为那要求你比较数组中的两个对象以确定哪个更大。你可以对 int 这样做，但对于一个没有实现 `<` 运算符的新类，你该如何做呢？答案是，知道该类的客户端代码必须传入一个委托，该委托包装一个执行比较的方法。另外，不要为临时变量使用 int 类型，而是可以使用泛型类型来实现一个泛型 `Sort` 方法。

对于一个接受类型 T 的泛型 `Sort<T>` 方法，需要有一个比较方法，该方法带有两个类型为 T 的参数，并且返回类型为 bool，以便用于 `if` 比较。这个方法可以由 `Func<T1, T2, TResult>` 委托来引用，其中 T1 和 T2 是相同的类型：`Func<T, T, bool>`。

这样一来，你就为你的 `Sort<T>` 方法赋予了以下签名：

```
static public void Sort<T>(IList<T> sortArray, Func<T, T, bool> comparison)
```

该方法的文档说明，`comparison` 必须引用一个接受两个参数的方法，并且当第一个参数的值小于第二个参数时返回 true。

现在一切就绪。以下是 `BubbleSorter` 类的定义（代码文件 BubbleSorter/BubbleSorter.cs）：

```
class BubbleSorter
{
    static public void Sort<T>(IList<T> sortArray, Func<T, T, bool> comparison)
    {
        bool swapped = true;
        do
        {
            swapped = false;
            for (int i = 0; i < sortArray.Count-1; i++)
            {
                if (comparison(sortArray[i+1], sortArray[i]))
                {
                    T temp = sortArray[i];
                    sortArray[i] = sortArray[i + 1];
                    sortArray[i + 1] = temp;
                    swapped = true;
                }
            }
        } while (swapped);
    }
}
```

要使用这个类，你需要定义另一个类，用于设置一个需要排序的数组。对于这个示例，假设 Mortimer Phones 移动电话公司有一个员工列表，希望按照薪水对他们进行排序。每个员工都由一个 `Employee` 类的实例表示，该类看起来类似于下面这样（代码文件

