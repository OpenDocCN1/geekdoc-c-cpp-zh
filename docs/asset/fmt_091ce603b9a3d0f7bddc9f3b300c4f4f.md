
运行此程序时，你会看到显示从 0 到 9 的数字。一旦 `number` 变成 10 或大于 10，程序将退出循环序列。正如你所看到的，`do` 循环的功能方式与 `while` 循环类似，但它是在执行序列后检查条件。

## for 循环

`for` 循环与 `do` 或 `while` 循环不同。`for` 循环通常用于你确切知道想要迭代次数的情况。当你有特定的循环次数时也可以使用它。下面的示例展示了 `for` 循环的使用。

```cs
using System;

namespace ConsoleApplication1
{
class Program
{
    static void Main(string[] args)
    {
        int number = 10;
        for (int i = 0; i < number; i++)
        {
            Console.WriteLine(i);
        }
        Console.ReadLine();
    }
}
}
```

运行这段代码时，你会发现 `for` 循环与 `while` 循环相似，但它在代码结构上更紧凑。`for` 循环包含三个部分：首先初始化变量，然后是条件检查，最后是循环后的操作。
