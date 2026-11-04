
仅链接到地址。这应让你想起第 2 章中的按引用调用。大多数情况下，它们是受限指针，正如你所回忆的那样，它们使我们能够从子程序内部同时访问和修改传递的变量。这赋予我们将这些值用作全局变量的能力，但同时具有局部变量增加的即插即用能力，这使得指针非常有用，但也可能很危险。因此，C# 允许指针操作，但仅在新定义的不安全模式下。

## 启用不安全模式

一旦项目加载到 .Net 编译器中，只需简单地更改该项目的构建配置即可启用不安全模式。从标记为“视图”的文件夹中，选择标题为“解决方案资源管理器”的文件（见屏幕截图 4.1）。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_264_0.png)

将打开第二个侧窗口；确保突出显示项目而不是文件名。选择“属性”，即该较小的窗口中显示的第三个图标（见屏幕截图 4.2）。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_265_0.png)

现在转到标记为“配置属性”的列表。从该子列表中选择“生成”，并点击“允许不安全代码块”下的“False”值。从那里，将出现一个箭头——使用它选择“True”设置并按下“应用”（见屏幕截图 4.3）。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_265_1.png)

## 指针变量

指针变量与所有其他类型的变量一样需要声明，但由于它们需要指向的位置，因此在被引用之前也需要被赋值。指针也像标准变量一样受其数据类型和命名规则的限制。因此，可以推断出，声明为整数的指针只能指向也声明为整数的标准变量，双精度与双精度，浮点与浮点，字符与字符。声明指针时唯一的视觉区别是插入星号符号（*），它放在数据类型的引用前面。这个星号告诉编译器该数据类型实际上 intended 用于声明指针变量。在这种情况下，星号被称为解引用运算符，变量被称为解引用变量。第二步是为指针赋值；这是通过使指针等于标准变量来完成的。必须在标准变量前加上与号符号（&）（与号被称为地址运算符）。记住，未赋值的指针没有指向的对象，不能使用（见示例 4.25）。注意：还有一种 void 数据类型指针，这是一种通用指针，可以链接到其他任何数据类型。Void 指针数据类型将在本章后面讨论。

### 示例 4.25. 指针。

```
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int* pointer1;
            int variable1 = 1;
            float* pointer2;
            float variable2 = 2.0f;
            double *pointer3;
            double variable3 = 3.01;
            char *pointer4;
            char variable4 = 'A';

            pointer1 = &variable1;
            pointer2 = &variable2;
            pointer3 = &variable3;
            pointer4 = &variable4;
            Console.WriteLine ("{0}    {1}", variable1, *pointer1);
            Console.WriteLine ("{0}    {1}", variable2, *pointer2);
            Console.WriteLine ("{0}    {1}", variable3, *pointer3);
            Console.WriteLine ("{0}    {1}", variable4, *pointer4);
        }
    }
}
```

我们也可以为指针分配数值，但只有在它们已被分配内存位置之后。同样，我们将使用等号来分配值并使用星号符号来引用指针。你应该注意，由于指针将其新值放在标准变量使用的内存位置中，任何先前的信息都会被覆盖。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_267_0.png)

> "我刚拿到这张新的指针 VISA——上面有我的名字，但费用却关联到别人的账户。"
> "你确定这合法吗？"
> "嗯，并不总是，我必须在不安全县使用它。"

指针也可以为其他指针分配位置——见示例 4.26 中的代码。

### 示例 4.26. 为指针分配值和内存位置。

```
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int* pointer1, pointer2;
            // Warning, pointer3 is not an actual pointer!
            int variable1 = 1, pointer3;
            // Assigning a pointer to a value
            pointer1 = &variable1;
            // Pointer to pointer assignments DO NOT require the asterisk.
            pointer2 = pointer1;
            // Pointers can also pass values to variables.
            pointer3 = *pointer2;
            Console.WriteLine("{0}  {1}  {2}  {3}",
                variable1, *pointer1, *pointer2, pointer3);

            *pointer1 = 20;  // the value inside that address is now 20.

            Console.WriteLine("{0}  {1}  {2}  {3}",
                variable1, *pointer1, *pointer2, pointer3);
        }
    }
}
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_268_0.png)

### 关键字 null

关键字 null 是唯一可以分配给未分配指针而不会导致错误的值。null 语句在向通用函数传递无意义值时也很方便，如 MyFunction (SomeNumber, null); 当第一个值代表短路事件时，第二值不是必需的。null 值的工作方式基本上与 C++ 中的 NULL 值相同，只是现在它实际上是一个关键字。

## 使用指针参数的按引用调用值

正如你从第 2 章中回忆的那样，我们能够将函数调用写成按值调用和按引用调用，但按引用调用也让我们能够更改原始变量的值。你还应该回忆起（从我们对指针的介绍中）按引用调用实际上是指针的受限形式。这使得我们可以重写这些程序，使其使用实际的指针表示法，而不会显著改变这些程序（见示例 4.27）

### 示例 4.27. 使用指针参数的按引用调用。

```
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            string input;
            char race = 'y';
            int winner, number1 = 0, number2 = 0, number3 = 0;

            Console.WriteLine("Let's have a horse race.\n"
                + "To play select one of the horses below");

            while (char.ToUpper (race) != 'N') {
                Console.WriteLine("(1) for Whitefire\n"
                    + "(2) for The Train and, \n"
                    + "(3) for Noisy Glue");

                input = Console.ReadLine();

                the_race(&number1, &number2, &number3);
                tie_breaker(&number1, &number2);
                tie_breaker(&number2, &number3);
                tie_breaker(&number1, &number3);

                winner = the_winner(&number1, &number2, &number3);
                Console.Write("And the winner is ");

                if (winner == '1')
                    Console.WriteLine("Whitefire");
                else if (winner == '2')
                    Console.WriteLine("The Train");
                else
                    Console.WriteLine("Noisy Glue");

                Console.Write("Would you like to play again (Y/N)?");
                input = Console.ReadLine();
                race = char.Parse(input);
            }
        }

        static unsafe void the_race(int *number1, int *number2,
            int *number3) {
            Random rnd = new Random();

            *number1 = (int)(rnd.NextDouble() * 100);
            *number2 = (int)(rnd.NextDouble() * 100);
            *number3 = (int)(rnd.NextDouble() * 100);
            Console.Write(".");
        }

        static unsafe void tie_breaker(int *num1, int *num2) {
            if (*num1 == *num2)
                *num2 = *num2 - 1;
            Console.Write(",");
        }

        static unsafe char the_winner(int *num1, int *num2, int *num3) {
            char winner;
            if (*num1 > *num2 && *num1 > *num3)
                winner = '1';
            else if (*num2 > *num1 && *num2 > *num3)
                winner = '2';
            else winner = '3';
            Console.Write(".");

            return(winner);
        }
    }
}
```

## 指针算术

指针算术只是应用于指针的变量算术（注意：需要星号）。在指针算术中，指针像变量一样用于对存储的值进行加、减、乘、除和求余运算。指针也可以与简写表示法以及递增和递减运算符一起使用（递增和递减运算符也需要插入括号——见示例 4.28 和 4.29）。

### 示例 4.28. 指针的算术运算。

```
using System;

namespace Chapter4 {
    class Class1 {
        static unsafe void Main() {
            int number1 = 0, number2 = 0;
            int* pointer1 = &number2;

            number1 = number1 + 10;       // Addition
            *pointer1 = *pointer1 + 10;
            Console.WriteLine("{0}    {1}", number1, number2);

            number1 = number1 - 1;       // Subtraction
```
