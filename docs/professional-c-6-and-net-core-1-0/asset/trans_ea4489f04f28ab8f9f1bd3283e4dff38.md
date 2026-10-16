
```
{
    // etc.
}
```

在前面的示例中，你也可以对迭代变量 `i` 使用类型推断。使用类型推断后，循环结构如下所示：

```
for (var i = 0; i < 100; i++)
{
    // etc.
}
```

嵌套 `for` 循环并不罕见，这样对于外层循环的每次迭代，内层循环都会完整执行一次。这种方法通常用于遍历矩形多维数组中的每个元素。最外层循环遍历每一行，内层循环遍历特定行中的每一列。下面的代码显示多行数字。它还使用了另一个 `Console` 方法 `Console.Write`，该方法与 `Console.WriteLine` 的功能相同，但不会向输出发送回车符（代码文件 `ForLoop/Program.cs`）：

```
using static System.Console;

namespace Wrox
{
    class Program
    {
        static void Main()
        {
            // This loop iterates through rows
            for (int i = 0; i < 100; i+=10)
            {
                // This loop iterates through columns
                for (int j = i; j < i + 10; j++)
                {
                    Write($"  {j}");
                }
                WriteLine();
            }
        }
    }
}
```

尽管 `j` 是整数，但它会自动转换为字符串，以便进行串联。

上述示例产生如下输出：

```
0   1   2   3   4   5   6   7   8   9
10  11  12  13  14  15  16  17  18  19
20  21  22  23  24  25  26  27  28  29
30  31  32  33  34  35  36  37  38  39
40  41  42  43  44  45  46  47  48  49
50  51  52  53  54  55  56  57  58  59
60  61  62  63  64  65  66  67  68  69
70  71  72  73  74  75  76  77  78  79
80  81  82  83  84  85  86  87  88  89
90  91  92  93  94  95  96  97  98  99
```

从技术上讲，`for` 循环的测试条件中也可以计算计数器变量以外的内容，但这肯定不是典型的用法。`for` 循环中也可以省略一个（甚至全部）表达式。不过，在这种情况下，你应该考虑使用 `while` 循环。

## while 循环

与 `for` 循环一样，`while` 是一种前测循环。语法类似，但 `while` 循环只接受一个表达式：

```
while(condition)
    statement(s);
```

与 `for` 循环不同，`while` 循环最常用于在循环开始前不知道次数的情况下重复执行一条语句或一个语句块。通常，`while` 循环体内的语句会在某次迭代时将布尔标志设置为 `false`，从而触发循环结束，如下例所示：

```
bool condition = false;
while (!condition)
{
    // This loop spins until the condition is true.
    DoSomeWork();
    condition = CheckCondition();  // assume CheckCondition() returns a bool
}
```

## do...while 循环

`do...while` 循环是 `while` 循环的后测版本。这意味着循环的测试条件在循环体执行之后才进行求值。因此，`do...while` 循环适用于必须至少执行一次语句块的情况，如下例所示：

```
bool condition;
do
{
    // This loop will at least execute once, even if Condition is false.
    MustBeCalledAtLeastOnce();
    condition = CheckCondition();
} while (condition);
```

## foreach 循环

`foreach` 循环使你可以遍历集合中的每一项。目前，不必担心集合到底是什么（将在第 11 章“集合”中全面解释）；只需理解它是一个表示对象列表的对象。从技术上讲，一个对象要算作集合，必须支持名为 `IEnumerable` 的接口。集合的示例包括 C# 数组、`System.Collections` 命名空间中的集合类，以及用户定义的集合类。如果你假设 `arrayOfInts` 是一个 `int` 数组（这并不令人意外），那么可以从下面的代码中了解 `foreach` 的语法：

```
foreach (int temp in arrayOfInts)
{
    WriteLine(temp);
}
```

在这里，`foreach` 逐个元素地遍历数组。对于每个元素，它将该元素的值放入名为 `temp` 的 `int` 变量中，然后执行一次循环迭代。

这里是可以使用类型推断的另一种情况。`foreach` 循环将变成如下形式：

```
foreach (var temp in arrayOfInts)
{
    // etc.
}
```

`temp` 将被推断为 `int`，因为这就是集合项的类型。

使用 `foreach` 时需要注意的重要一点是，你不能更改集合中项的值（前面代码中的 `temp`），因此如下代码将无法编译：

```
foreach (int temp in arrayOfInts)
{
    temp++;
    WriteLine(temp);
}
```

如果需要遍历集合中的项并更改其值，则必须改用 `for` 循环。

## 跳转语句

C# 提供了许多语句，使你可以立即跳转到程序中的另一行。其中第一个当然就是臭名昭著的 `goto` 语句。

### goto 语句

`goto` 语句使你可以直接跳转到程序中由*标签*（只是一个标识符后跟一个冒号）指示的另一指定行：

```
goto Label1;
    WriteLine("This won't be executed");
Label1:
    WriteLine("Continuing execution from here");
```

`goto` 涉及一些限制。你不能跳入 `for` 循环这样的代码块，不能跳出类，也不能在 `try...catch` 块之后退出 `finally` 块（第 14 章“错误和异常”将介绍如何使用 `try...catch...finally` 进行异常处理）。

`goto` 语句的名声可能早已为人所知，而且在大多数情况下，使用它是极不受欢迎的。总的来说，它肯定不符合良好的面向对象编程实践。

### break 语句

你已经简要了解了 `break` 语句——在 `switch` 语句中使用它退出某个 `case` 时。实际上，`break` 也可以用于退出 `for`、`foreach`、`while` 或 `do...while` 循环。控制权会切换到循环结束后的下一条语句。

如果该语句出现在嵌套循环中，控制权会切换到最内层循环的末尾。如果 `break` 出现在 `switch` 语句或循环之外，则会发生编译时错误。

### continue 语句

`continue` 语句与 `break` 类似，你必须在 `for`、`foreach`、`while` 或 `do...while` 循环中使用它。不过，它只退出当前循环迭代，这意味着执行会从循环的下一次迭代开始处重新开始，而不是完全在循环外部重新开始。

### return 语句

`return` 语句用于退出类的方法，并将控制权返回给方法的调用者。如果方法具有返回类型，`return` 必须返回该类型的值；否则，如果方法返回 `void`，则应使用不带表达式的 `return`。

## 使用枚举

*枚举*是一种用户定义的整数类型。声明枚举时，需要指定该枚举的实例可以包含的一组可接受值。不仅如此，你还可以为这些值指定用户友好的名称。如果在代码中的某处尝试将不在可接受值集合中的值分配给该枚举的实例，编译器会标记错误。

从长远来看，创建枚举可以节省大量时间和麻烦。使用枚举而不是普通整数至少有三个好处：

- 如前所述，枚举有助于确保你的变量只被赋予合法且预期的值，从而使代码更易于维护。
- 枚举允许你用描述性名称而非晦涩的“魔法数字”来引用整数值，从而使代码更清晰。
- 枚举使代码更易于输入。当你开始为枚举类型的实例赋值时，Visual Studio 2015 会使用 IntelliSense 弹出一个可接受值的列表框，以
