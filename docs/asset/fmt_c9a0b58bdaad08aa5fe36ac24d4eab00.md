
在这里，`ExceptionType` 是发生的异常类型。当异常被抛出时，它会被相应的 `catch` 子句捕获，由其处理异常。正如通用形式所示，一个 `try` 可以关联多个 `catch` 子句。异常类型决定了执行哪个 `catch`。也就是说，如果 `catch` 指定的异常类型与异常匹配，则执行与该 `catch` 关联的代码块。

## C# 3.0: 入学者指南

（其他 `catch` 子句将被跳过）。当异常被捕获时，异常变量 `exOb` 将接收其值。

实际上，指定 `exOb` 是可选的。如果异常处理程序不需要异常对象（通常情况下如此），那么就没有需要指定 `exOb`。由于这个原因，本章中的许多示例将不会指定 `exOb`。

这里有一个重要的点：如果没有抛出异常，则所有的 `catch` 块都将被跳过。异常将从最后一个 `catch` 之后的第一个语句继续；只有在抛出异常时，才会执行 `catch`。

# 简单的异常示例

下面的示例说明了如何监控并捕获异常。如你所知，尝试访问数组边界之外的索引是一个错误。当这种情况发生时，C# 运行时会抛出一个 `IndexOutOfRangeException`，这是一个标准异常。接下来的程序故意生成了这样一个异常并捕获了它：

```c
// 演示异常处理。

using System;

class ExcDemo1 {

    static void Main() {

        int[] nums = new int[4];

        try {

            Console.WriteLine("Before exception is generated.");

            // 生成索引越界异常。

            nums[7] = 10;

            Console.WriteLine("this won't be displayed");

        } catch (IndexOutOfRangeException) {

            // 捕获异常

            Console.WriteLine("Index out-of-bounds!");

        }

        Console.WriteLine("After catch block.");

    }

}
```

该程序显示以下内容：

Before exception is generated.
Index out-of-bounds!
After catch block.

虽然很短，但前面的程序说明了异常处理的几个关键点。首先，你想要监控错误的代码包含在 `try` 块中。其次当发生异常时（在本例中，是因为尝试访问边界内的索引），异常会被抛出 `try` 块并被 `catch` 捕获。此时，控制权传递到 `catch` 块，`try` 块终止。也就是说，`catch` 没有被调用。

# 第 10 章：异常处理

相反，程序执行被转移到了它。因此，越界索引之后的 `WriteLine()` 语句永远不会执行。在 `catch` 块执行后，程序控制将继续执行 `catch` 之后的语句。因此，你的异常处理程序的任务是修复导致异常的问题，以便程序执行能够正常继续。

注意，`catch` 子句中没有指定异常变量。相反，需要异常的类型（在本例中为 `IndexOutOfRangeException`）。如前所述，只有在需要访问异常对象时才需要异常变量。在某些情况下，异常处理程序可以使用异常对象的值来获取有关错误的额外信息。因此，`catch` 异常变量缺失并不罕见，正如前面的程序中的所示。

正如所解释的，如果 `try` 块没有抛出异常，则没有 `catch` 会被执行，程序控制将在 `catch` 之后恢复。为了确认这一点，在前面的程序中，将该行：

`nums[7] = 10;`

改为

`nums[0] = 10;`

现在，没有生成异常，`catch` 块也不会被执行。

## 第二个异常示例

理解 `try` 块中的所有代码都受到异常监控是非常重要的。这包括由从 `try` 块内部调的方法可能生成的异常。从 `try` 块内部调用的方法抛出的异常可以被该 `try` 块捕获——当然，假设方法本身没有捕获该异常。例如，这是一个有效的程序：

```csharp
// 异常可以由一个方法生成并由另一个方法捕获。

using System;

class ExcTest {

    // 生成异常。

    public static void GenException() {

        int[] nums = new int[4];

        Console.WriteLine("Before exception is generated.");

        // 生成索引越界异常。

        nums[7] = 10;

        Console.WriteLine("this won't be displayed");

    }

}
```

```csharp
class ExcDemo2 {

    static void Main() {

        try {

            ExcTest.GenException();

        } catch (IndexOutOfRangeException) {

            // 捕获异常。

            Console.WriteLine("Index out-of-bounds!");

        }

        Console.WriteLine("After catch block.");

    }

}
```

此程序产生以下输出，与之前的第一个版本相同：

Before exception is generated.
Index out-of-bounds!
After catch block.

由于 `GenException()` 是从 `try` 块调用的，它生成的（且未捕获的）异常被 `Main()` 中的 `catch` 捕获了。理解，如果 `GenException()` 捕获了异常，它将永远不会传回 `Main()`。

## 未捕获异常的后果

捕获 C# 的标准异常有一个好处：它可以防止程序终止。当异常抛出时，它必须被某些代码捕获。通常情况下，如果你的程序没有捕获异常，会导致异常终止。虽然这种消息对调试有用，但并不是你希望用户看到的。例如，下面的代码显示了异常未被正确捕获时发生的情况：

```csharp
// 这无效

using System;

class TypeMismatch {

    static void Main() {

        int[] nums = new int[4];

        try {

            Console.WriteLine("Before exception is generated.");

            // 生成索引越界异常。

            nums[7] = 10; 

            Console.WriteLine("this won't displayed");

        } catch (DivideZeroException) {

            /* 无法捕获数组错误。 */

            Console.WriteLine("Index out-of-bounds!");

        }

        Console.WriteLine("After catch block.");

    }

}
```

在这里显示输出：

Before exception is generated.

Unhandled Exception: System.IndexOutOfRangeException outside the array.
at TypeMismatch.Main()

### 异常让你优雅处理

异常处理的一个关键优势是它允许你的程序响应错误并继续。例如，考虑下面的示例，它将一个数组的元素除以另一个数组的元素。如果发生了除以零，就会生成一个 `DivideZeroException`。在程序中，通过报告错误并继续来处理。

```csharp
// 优雅地处理错误并继续。

using System;

class ExcDemo3 {

    static void Main() {

        int[] numer = { 4, 8, 16, 32, 64, 128 };

        int[] denom = { 2, 0, 4, 4, 0, 8 };

        for(int i=0; i < numer.Length; i++) {

            try {

                Console.WriteLine(numer[i] + " / " + 

                denom[i] + " is " + 

                numer[i]/denom[i]);

            } catch (DivideZeroException) {

                Console.WriteLine("Can't divide by Zero!");

            }

        }

    }

}
```

程序的输出在这里：

```
4 / 2 is 2
Can't divide by Zero!
16 / 4 is 4
32 / 4 is 8
Can't divide by Zero!
128 / 8 is 16
```

这个示例说明了另一个重要的点：一旦异常被处理，它就会从系统中移除。因此，在程序中，循环的每次都会都会进入进入块——之前的异常已经被处理过了。这使得你的程序能够处理重复的错误。

### 使用多个 catch 子句

你可以与 `try` 块关联多个一个 `catch` 子句。事实上，这样做非常常见。然而，每个 `catch` 必须捕获不同类型的异常。例如，此处显示的程序同时捕获了数组边界错误和除零错误：

```csharp
// 使用多个 catch 子句。

using System;

class ExcDemo4 {

    static void Main() {

        // 这里，numer 的长度比 denom 长。

        int[] numer = { 4, 8, 16, 32, 64, 128, 256, 512 };

        int[] denom = { 2, 0, 4, 4, 0, 8 };

        for(int i=0; i < numer.Length; i++) {

            try {

                Console.WriteLine(numer[i] + " / " +

                                denom[i] + " is " +

                                numer[i]/denom[i]);

            }

            catch (DivideByZeroException) {

                Console.WriteLine("Can't divide by Zero!");

            }

            catch (OutOfRangeException) {

                Console.WriteLine("No matching element found.");

            }

        }

    }

}
```

该程序产生以下输出：

```
4 / 2 is 2
Can't divide by Zero!
16 / 4 is 4
32 / 4 is 8
Can't divide by Zero!
128 / 8 is 16
No matching element found.
No matching element found.
```
