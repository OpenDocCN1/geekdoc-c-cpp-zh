
`case 'o':`

`case 'u':`

如果逻辑表达式为真，则执行 `statement1`；否则，执行 `statement2`。

列表 4.8 所示的程序 `CondOperator1.cs` 的重点是解释如何使用条件运算符。程序要求用户输入产品的可用数量。如果可用数量小于100，则订购数量为 500；否则，为 250。

# 列表 4.8 CondOperator1.cs 文件中的程序代码

```
using System;

class CondOperator1 {

    static void Main() {

        int avqty, ordqty;

        Console.Write("Enter available quantity: ");

        avqty = Convert.ToInt32(Console.ReadLine());

        if(avqty < 100)ordqty=500;

        else ordqty=250;

        Console.WriteLine("Available Quantity: (0) and Ordered Quantity: (1)", avqty, ordqty);

        ordqty=avqty<100?500:250;

        Console.WriteLine("Available Quantity: (0) and Ordered Quantity: (1)", avqty, ordqty);

    }

}
```

输出：

```
Enter available quantity: 200

Available Quantity: 200 and Ordered Quantity: 250

Available Quantity: 200 and Ordered Quantity: 250
```

这里是另一个演示条件运算符使用的示例。列表 4.9 所示的程序 `CondOperator2.cs` 要求用户输入一个数字，并判断输入的数字是偶数还是奇数。

# 列表 4.9 CondOperator2.cs 文件中的程序代码

```
using System;

class CondOperator2 {

    static void Main() {

        int n;

        Console.Write("Enter a number: ");

        n = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine(n%2==0?"Number is an even number":"Number is an odd number");

    }

}
```

输出：

Enter a number: 20
Number is an even number

Enter a number: 7
Number is an odd number

如果三元运算符中提到的条件为真（即如果应用于变量 `n` 的取模运算结果为 0），则在屏幕上显示消息“Number is an even number”。否则，显示消息“Number is an odd number”。

## 循环

循环是指允许在给定的逻辑表达式求值为真时，重复执行一组语句的结构。本节讨论了以下三种循环：

- `while` 循环
- `do-while` 循环
- `for` 循环

## while 循环

`while` 循环只要逻辑表达式求结果为真，就会执行一组语句。布尔表达式包含在循环的开头。在求结果为真之前，不会执行循环体。

语法：

```
while(logical expression)

{

    ................

    // 循环体

}
```

当逻辑表达式求值为假时，程序控制权将传递到紧随循环之后的语句。

注意

如果循环体由单个语句组成，大括号是可选的。

列表 4.10 所示的程序 `while1.cs` 打印从 1 到 10 的序列号。

# 列表 4.10 while1.cs 文件中的程序代码

```
using System;

class while1 {

    static void Main() {

    int k;

    k=1;

    Console.WriteLine("The sequence numbers from 1 to 10 are:");

    while(k<=10) {

        Console.WriteLine(k);

        k++;

    }

}

}
```

## 输出：

The sequence numbers from 1 to 10 are:
1
2
3
4
5
6
7
8
9
10

你可以看到变量 `k` 初始化为 1。`while` 循环设置为只要变量 `k` 的值小于或等于 10 就执行。在 `while` 循环体内，显示变量 `k` 的值并递加 1。因此，循环显示了从 1 到 10 的序列号。

列表 4.11 所示的程序 `while2.cs` 打印从 a 到 z 的字符。

# 列表 4.11 while2.cs 文件中的程序代码

```
using System;

class while2 {

    static void Main() {

    char k;

    k='a';

    while(k<='z') {

Console.Write("(0) ",k);

k++;

}

}

}
```

输出：

a b c d e f g h i j k l n o p r s t u v w x y z

列表 4.12 所示的程序 `while3.cs` 打印用户输入的两个限制之间的序列号。

# 列表 4.12 while3.cs 文件中的程序代码

```
using System;

class while3 {

    static void Main() {

        int k,m,n;

        Console.WriteLine("Enter the beginning and ending limits of the sequence number you wish to print*");

        m = Convert.ToInt32(Console.ReadLine());

        n = Convert.ToInt32(Console.ReadLine());

        k = m;

        Console.WriteLine("The sequence numbers from (0) to (1) are:", m,n);

        while(k<=n) {

            Console.WriteLine(k);

            k++;

        }

    }

}
```

输出：

Enter the beginning and ending limits of the sequence number you wish to print*
5
9

The sequence numbers from 5 to 9 are:
5
6
7
8
9

## 循环

变量 `k` 被初始化为用户在变量 `m` 中输入的上限。只要变量 `k` 的值小于或等于在变量 `n` 中输入的下限，`while` 循环就会执行。因此，输入范围 `m` 和 `n` 之间的序列号将显示在屏幕上。

## do-while 循环

与 `while` 循环一样，`do-while` 用于在包含的逻辑表达式为真时执行一组语句。`while` 和 `do-while` 循环的区别在于逻辑表达式是在循环的底部评估，而不是在开头。此外，即使逻辑表达式为假，`do-while` 循环也会执行一次。`do-while` 循环的语法如下：

```
do {

  ...

  ....

  //循环体

} while(logical expression);
```

由于逻辑表达式在循环执行后进行评估，当逻辑表达式为真或假时，循环至少运行一次。

列表 4.13 显示的 `dowhile.cs` 程序打印从 1 到 10 的序列号。

列表 4.13 文件 `dowhile1.cs` 中的代码

```
using System;

class dowhile {

  static void Main() {

    int k;

    Console.WriteLine("The sequence numbers from 1 to 10 are:");

    k = 1;

    do {

      Console.WriteLine(k);

      k++;

    } while(k<=10);

  }

}
```

## 输出：

从 1 到 10 的序列号为：
1
2
3
4
5
6
7
8
9
10

如果在前面的程序中，你将变量 `k` 的初始值设置为 15，循环将执行一次，在屏幕上显示值 15。这是因为 `do-while` 循环中的逻辑表达式是在最后评估的。

`do-while` 循环的优点是它至少执行一次。因此，你可以用它从用户获取数据并根据接收到的数据做决策。列表 4.14 显示的 `dowhile2.cs` 程序累加用户输入的数值。程序继续累加用户输入的数值，直到输入 0 为止。

# 列表 4.14 文件 `dowhile2.cs` 中的代码

```
using System;

class dowhile {

    static void Main() {

        int k,s;

        s=0;

        Console.WriteLine("Enter the number you wish to add, enter 0 to quit:");

        do {

            k = Convert.ToInt32(Console.ReadLine());

            s+=k;

        }while(k !=0);

        Console.WriteLine("The sum of the numbers entered is {0}", s);

    }

}
```

## 输出：

输入你想累加的数字，输入 0 退出：
9
1
5
0

输入的数字之和为 15。

接下来，你将查看另一个循环：`for` 循环。

## for 循环

`for` 循环用于重复指定次数一组语句。
语法：

```
for(initializing variables(s); condition; increment/decrement)

{

    statement1;

    statement2;

    ...

}
```

其中，初始化变量意味着对执行循环起主要作用的变量分配一个初始值。只要布尔表达式（条件）为真，`for` 循环就会继续执行。当条件变为假时，程序控制将退出 `for` 循环，并从 `for` 循环后的语句继续执行程序。递增/递减决定了在循环的每次迭代中从变量上增加或减少的值。

## 注意

如果 `for` 循环体中使用的语句只有一个，大括号是可选的。

列表 4.15 显示的 `ForLoop1.cs` 程序使用 `for` 循环显示从 1 到 10 的序列号。

# 列表 4.15 `ForLoop1.cs` 中的代码

```c

using System;

class ForLoop {

    static void Main() {

        int i;

        Console.WriteLine("Sequence numbers from 1 to 10:");

        for(i = 1; i<=10; i++)

            Console.WriteLine(i);

    }

}

```

输出：

从 1 到 10 的序列号：
1
2
3
4
5
6
7
8
9
10

列表 4.16 显示的 `ForLoop2.cs` 程序演示了 `break` 语句如何终止并退出循环。程序显示从 1 到 10 的序列号。

# 列表 4.16 `ForLoop2.cs` 文件

```c

using System;

class ForLoop2 {

    static void Main() {

        int i;

        Console.WriteLine("Sequence numbers from 1 to 10:");

        for(i = 1; i <=15; i++)

        {

            if(i>10)break;

            Console.WriteLine(i);

        }

    }

}

```

输出：

从 1 到 10 的序列号：
1
2
3
4
5
6
7
8
9
10

`for` 循环只要变量 `i` 的值小于 15。在循环体内，`if` 语句用于在变量 `i` 大于 10 时退出循环。因此，循环在显示 10 后终止。

列表 4.17 显示的 `BreakExample.cs` 程序是 `break` 语句的另一个示例。程序显示从 1 到 10 的序列号。程序还演示了如何在没有初始化（语句）、条件和递增/递减的情况下运行循环。

# 列表 4.17 `BreakExample.cs` 中的代码

```c

using System;

class BreakExample {

    static void Main() {

        Console.WriteLine("Sequence numbers from 1 to 10:");

        int k=1;

        for(;;) {

            if(k>10)break;

            Console.WriteLine(k);

            k++;

        }

    }

}

```

从程序可以看出，变量 `k` 在循环之前初始化为 1。在 `for` 循环中，`if` 语句用于指定退出条件，变量 `k` 在循环体内递增。运行程序后，你得到了从 1 到 10 的序列号。

列表 4.18 显示的 `SumSeq.cs` 程序打印从 1 到 10 的序列号之和。

# 列表 4.18 `SumSeq.cs` 中的代码

```c

using System;

class SumSeq {

    static void Main() {

        int i;

        sum = 0;

        for(i=1;i<=10;i++) {

            sum += i;

        }

        Console.WriteLine("Sum of first 10 sequence numbers is " + sum);

    }

}

```

输出：

前 10 个序列号之和为 55

你可以看到用于放置序列号的变量 `sum` 初始化为 0。计数器 `i` 设置为循环 1 到 10 的值。当计数器 `i` 的值加到变量 `sum` 时。当 `for` 循环完成后，变量 `sum` 将计数器代表的所有值。

## continue 语句

`continue` 语句跳过循环体并继续循环的下次迭代。与 `break` 语句不同，`continue` 语句不会终止并退出循环；它只是跳过循环的剩余语句并执行下一个值。

列表 4.19 显示的 `ContinueExample.cs` 程序显示除 7 以外的 1 到 10 的序列号。

# 列表 4.19 `ContinueExample.cs` 中的代码

```c

using System;

class ContinueExample {

  static void Main() {

    int i;

    Console.WriteLine("Sequence numbers from 1 to 10 except 7:");

    for(i = 1; i<=10; i++)

    {

      if(i==7)continue;

      Console.WriteLine(i);

    }

  }

}

```

输出：

除 7 以外的 1 到 10 的序列号：
1
2
3
4
5
6
8
9
10

`for` 循环通过将变量 `i` 初始化为 1 并设置 `for` 循环只要变量 `i` 的值小于或等于 10 就执行，执行十次。在循环的每次迭代中，变量 `i` 递增 1。在循环中，显示变量 `i` 的值以在屏幕上打印序列号。如果循环中使用任何语句检查变量 `i` 的值是否等于 7，如果变量 `i` 的值等于 7，`continue` 语句将跳过循环体，它不在屏幕上显示值 7。此外，变量 `i` 的值在下次迭代时递增 1。程序显示变量 `i` 从 1 到 10 的所有值，除 7 以外。

列表 4.20 显示的 `AddEven.cs` 程序要求用户输入几个数字并打印输入的偶数之和。

# 列表 4.20 `AddEven.cs` 中的代码

```c

using System;

class AddEven {

    static void Main(){

        int n,i,k,sum;

        sum=0;

        Console.WriteLine("How many numbers are there?");

        k = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine("Enter {0} numbers", k);

        for (i = 1; i<k; i++)

        {

