

```
for(i=0, j=10; i < j; i++, j--)
    Console.WriteLine("i and j: " + i + " " + j);
}
```

程序的输出如下：

```
i and j: 0 10
i and j: 1 9
i and j: 2 8
i and j: 3 7
i and j: 4 6
```

这里，逗号分隔两个初始化语句和两个迭代表达式。循环开始时，i 和 j 都会被初始化。每次循环重复时，i 递增，j 递减。多个循环控制变量通常很方便，可以简化某些算法。初始化语句和迭代语句的数量可以任意，但在实践中，超过两个会使 for 循环变得笨拙。

下面是在 for 语句中使用多个循环控制变量的一个实际例子。该程序在单个 for 循环内使用两个循环控制变量来找出一个数（这里是 100）的最大和最小因子。特别注意终止条件。它依赖于两个循环控制变量。

// Use commas in a for statement to find the largest and
// smallest factor of a number.

using System;

class Comma {
    static void Main() {
        int i, j;
        int smallest, largest;
        int num;

        num = 100;

        smallest = largest = 1;

        for(i=2, j=num/2; (i <= num/2) & (j >= 2); i++, j--) {
            if((smallest == 1) & ((num % i) == 0))
                smallest = i;

            if((largest == 1) & ((num % j) == 0))
                largest = j;
        }

        Console.WriteLine("Largest factor: " + largest);
        Console.WriteLine("Smallest factor: " + smallest);
    }
}

程序输出如下：

```
    Largest factor: 50
    Smallest factor: 2
```

通过使用两个循环控制变量，单个 **for** 循环可以同时找出一个数的最小因子和最大因子。控制变量 *i* 用于搜索最小因子。它最初设为 2，并递增直到其值超过 *num* 的一半。控制变量 *j* 用于搜索最大因子。它的值最初设为 *num* 的一半，并递减直到小于 2。循环运行直到 *i* 和 *j* 都达到各自的终止值。循环结束时，两个因子都已找到。

## 条件表达式

控制 **for** 循环的条件表达式可以是任何产生 **bool** 结果的有效表达式。它不需要涉及循环控制变量。例如，在下一个程序中，**for** 循环由 **done** 的值控制。

```
    // Loop condition can be any bool expression.

    using System;

    class forDemo {
        static void Main() {
            int i, j;
            bool done = false;

            for(i=0, j=100; !done; i++, j--) {

                if(i*i >= j) done = true;

                Console.WriteLine("i, j: " + i + " " + j);
            }
        }
    }
```

输出如下：

```
    i, j: 0 100
    i, j: 1 99
    i, j: 2 98
    i, j: 3 97
    i, j: 4 96
    i, j: 5 95
    i, j: 6 94
    i, j: 7 93
    i, j: 8 92
    i, j: 9 91
    i, j: 10 90
```

在这个示例中，**for** 循环迭代直到 **bool** 变量 *done* 为 true。当 *i* 的平方大于或等于 *j* 时，该变量在循环内被设为 true。

## 省略的部分

通过将循环定义的某些部分留空，可以创建一些有趣的 for 循环变体。在 C# 中，for 循环的初始化、条件或迭代部分中的任意一个或全部都可以为空。例如，考虑以下程序：

```
// Parts of the for can be empty.

using System;

class Empty {
    static void Main() {
        int i;

        for(i = 0; i < 10; ) {
            Console.WriteLine("Pass #" + i);
            i++; // increment loop control var
        }
    }
}
```

这里，for 的迭代表达式为空。相反，循环控制变量 i 在循环体内递增。这意味着每次循环重复时，都会测试 i 是否等于 10，但不会发生进一步的动作。当然，由于 i 在循环体内递增，循环会正常运行，显示以下输出：

```
Pass #0
Pass #1
Pass #2
Pass #3
Pass #4
Pass #5
Pass #6
Pass #7
Pass #8
Pass #9
```

在下一个示例中，初始化部分也被移出 for：

```
// Move more out of the for loop.

using System;

class Empty2 {
    static void Main() {
        int i;

        i = 0; // move initialization out of loop
        for(; i < 10; ) {
            Console.WriteLine("Pass #" + i);
            i++; // increment loop control var
        }
    }
}
```

在这个版本中，i 在循环开始之前初始化，而不是作为 **for** 的一部分。通常，你会希望在 **for** 内部初始化循环控制变量。只有当初始值通过复杂过程得出、不适合放在 **for** 语句内部时，通常才会把初始化放在循环之外。

## 无限循环

通过将条件表达式留空，可以使用 **for** 创建 *无限循环*（永不终止的循环）。例如，下面的片段展示了许多 C# 程序员创建无限循环的方式：

```
for(;;) // intentionally infinite loop
{
    //...
}
```

这个循环将永远运行。尽管有些编程任务（例如操作系统命令处理器）需要无限循环，但大多数“无限循环”*实际上*只是具有特殊终止要求的循环。（参见本章后面的“使用 **break** 退出循环”。）

## 无循环体的循环

在 C# 中，与 **for** 循环（或任何其他循环）关联的循环体可以为空。这是因为 *空语句* 在语法上是有效的。无循环体的循环通常很有用。例如，下面的程序使用无循环体循环对 1 到 5 求和：

```
// The body of a loop can be empty.

using System;

class Empty3 {
    static void Main() {
        int i;
        int sum = 0;

        // Sum the numbers through 5.
        for(i = 1; i <= 5; sum += i++) ;

        Console.WriteLine("Sum is " + sum);
    }
}
```

程序输出如下：

```
Sum is 15
```

注意，求和过程完全在 **for** 语句内处理，不需要循环体。特别注意迭代表达式：

```
sum += i++
```

不要被这种语句吓倒。它们在专业编写的 C# 程序中很常见，如果拆解成各部分就很容易理解。用文字来说，这条语句表示“把 i 的值加到 sum 上，然后递增 i”。因此，它等同于下面这组语句：

```
sum = sum + i;
i++;
```

## 在 for 循环内声明循环控制变量

控制 for 循环的变量通常只在循环内部需要，不在其他地方使用。在这种情况下，可以在 for 的初始化部分声明该变量。例如，下面的程序计算 1 到 5 的和与阶乘。它在 for 内声明循环控制变量 i。

// Declare loop control variable inside the for.
using System;
class ForVar {
    static void Main() {
        int sum = 0;
        int fact = 1;

        // Compute the factorial of the numbers 1 through 5.
        for(int i = 1; i <= 5; i++) {
            sum += i; // i is known throughout the loop.
            fact *= i;
        }

        // But, i is not known here.

        Console.WriteLine("Sum is " + sum);
        Console.WriteLine("Factorial is " + fact);
    }
}

在 for 循环内声明变量时，有一点很重要：该变量的作用域在 for 语句结束时结束。（也就是说，该变量的作用域仅限于 for 循环。）在 for 循环之外，该变量将不再存在。因此，在前面的示例中，i 在 for 循环之外不可访问。如果需要在程序其他地方使用循环控制变量，就不能在 for 循环内声明它。

在继续之前，你也许想尝试自己对 for 循环的各种变体。你会发现，它是一个迷人的循环。

## while 循环

C# 的另一种循环是 while。while 循环的一般形式是

    while(condition) statement;

其中 statement 可以是单条语句或语句块，condition 定义控制循环的条件，可以是任何有效的布尔表达式。当条件为真时执行该语句。当条件变为假时，程序控制转到紧跟在循环之后的行。

