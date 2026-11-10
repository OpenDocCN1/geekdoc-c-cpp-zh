

```c
/* third_prog.c: Uses repetition to print a character multiple times. */

#include <stdio.h>
int main(void)
{
    int your_number; int counter = 0; char character;

    /* Take user input first */
    printf("Enter the character to repeat: ");
    scanf("%c", &character);
    printf("Number of times to repeat '%c'?: ", character);
    scanf("%d", &your_number);
    printf("Printing '%c' %d times\n", character, your_number);

    /* Repetitive statement */
    while (counter < your_number) { /* Beginning of control block */
        printf("%c", character);
        counter = counter + 1;         /* Adds 1 to current value of counter */
    }                                  /* End of control block */
    printf("\n");                     /* Takes cursor to next line */

    return 0;
}
```

### 程序 4.3：**third_prog.c**

```text
Enter a character to repeat: *
Number of times to repeat '*': 20
Printing '*' 20 times
********************
```

### 程序输出：**third_prog.c**

语句 `counter = counter + 1;` 在代数中没有意义，但它是编程语言中用于递增变量的标准方法。循环每迭代一次，`counter` 的现有值就加 1，并将结果之和保存回同一个变量。这就是为什么用于计数的变量必须初始化为零。

> **注意：** 请做好准备，几乎在所有地方——常量、变量、表达式和函数中——都会看到真值和假值。在 C 语言中，任何能计算出数值的东西都可以被解释为真或假。

## 4.10 函数

C 语言严重依赖函数来完成所有工作。*函数*是表示一组语句的名称。提供给函数的输入被称为其*参数*。例如，函数 `printf("Dolly");` 只有 "Dolly" 这一个参数。如果 C 语言没有为特定任务提供函数，你就可以自己创建一个，我们将在下一个程序中这样做。

C 函数就像一个黑盒。我们只需要知道它做什么，而不需要知道它如何做。如果一个函数使用参数，我们必须知道参数的个数和数据类型。即使不了解 `printf` 的内部工作机制完全不影响我们使用它，我们也需要以不同的方式对待用户自定义函数。我们必须知道它们实际是如何工作的，否则维护起来会很困难。

一组函数的机器码保存在一个称为*库*的独立文件中。在 C 语言中，有一个库很特殊——*标准库*，它包含 `printf` 和 `scanf` 的机器码。当我们编译包含 `printf` 的程序时，链接器会从该库中提取其代码，并将其包含在程序可执行文件中（图 4.1）。

在所有 C 函数中，`main` 函数之所以特殊有两个原因。第一，它必须出现在每个可执行的 C 程序中（作为 `int main`）。第二，与 `printf` 这类定义（即实现）对我们隐藏的函数不同，`main` 在每个程序中都有定义。该定义以左花括号（{）开始，以右花括号（}）结束。程序的主体（不包括预处理指令）实际上就是 `main` 的主体，程序在遇到 `main` 时执行这个主体。

> **要点：** 我们不需要知道标准 C 函数是如何工作的，但必须以正确数量和类型的参数调用它们。如果一个函数定义指定了两个参数，类型分别为 int 和 float，那么我们必须严格按这种方式调用该函数。

> **注意：** 人们常说，预处理指令（如 `#define`）和函数（如 `printf`）不属于 C 语言。在 C 语言诞生初期，这种区分显然有其道理。如今，C 语言是一种标准化语言；ANSI 标准包含了预处理指令和标准函数。现在再把它们视为语言的“外部”部分就毫无意义了。

## 4.11 `fourth_prog.c`：一个包含用户自定义函数的程序

既然我们对函数有了一些了解，那就来创建一个包含用户自定义函数的程序吧。这个程序（程序 4.4）使用一个标准公式来计算定期存款的利息。该公式由函数 `calc_interest` 使用，调用时需要使用两组以下数据：本金、利率和期限。函数首先*声明*，然后*定义*，最后*调用*（或 *invoke*）。让我们逐一考察这些阶段。

函数的*声明*指定了其名称、参数的个数和数据类型，以及*返回*值的数据类型。`calc_interest` 需要三个参数，类型分别为 int、float 和 int，你必须严格按照指定方式调用它。并非所有函数都必须返回值，但 `calc_interest` 会返回值；它返回一个 float 类型的值（声明中的第一个单词）。注意终止该声明的分号（;）。

现在我们来看位于 `main` 主体下方的 `calc_interest` 的*定义*。定义的开头一行没有分号（;）作为结尾，但除此之外，它是声明的翻版。编译器会将定义与声明进行比较，如果它们的参数不匹配，就会输出错误。**calc_interest** 的定义指定了（i）三个参数及其数据类型，（ii）一组用于计算利息的语句，（iii）使用 **return** 语句返回该值的机制。

```c
/* fourth_prog.c: A simple interest calculator using a function. */

#include <stdio.h>

/* Function declaration or prototype */
float calc_interest(int principal, float interest_rate, int years);

int main(void)
{
    float amount;

    /* Use calc_interest function */
    amount = calc_interest(100, 6, 2);
    printf("Interest on 100 for 2 years = %f\n", amount);
    amount = calc_interest(200, 6, 3);
    printf("Interest on 300 for 3 years = %.2f\n", amount);

    return 0;
}

/* Function definition */
float calc_interest(int principal, float interest_rate, int years)
{
    float interest_amount;
    interest_amount = principal * (interest_rate / 100) * years;
    return interest_amount;
}
```

### 程序 4.4：fourth_prog.c

```text
Interest on 100 for 2 years = 12.000000
Interest on 300 for 3 years = 36.00
```

### 程序输出：fourth_prog.c

**main** 的主体两次调用 **calc_interest**，但使用了不同的参数集。在每种情况下，返回值都会在打印前保存到变量 amount 中。注意，**printf** 是一个真正的格式化工具；它最多可以打印两位小数（`%.2f`）。我们稍后将学习如何在不将函数返回值保存到变量的情况下直接打印它。

通过使用函数计算利息，我们在两个方面受益。第一，我们使代码*可重用*。我们可以在同一个程序中或在不同程序中多次调用这个函数，而无需复制代码。第二，代码维护也更加容易，因为如果公式发生变化，只需在*单一*位置进行修改。

> **注意：** C 语言是在一个前提下开发的：较低层的函数完成所有工作，而 `main` 函数（或其他高层函数）调用它们。如果一个函数被设计为独立单元，它可以存储在单独的库中供多个应用程序使用。在这种情况下，链接器必须知道该库的名称和位置。

## 4.12 C 语言的特点

尽管我们在本章的四个示例程序中只看到了少数 C 语言结构，但我们已经接触了该语言的大部分关键特性。C 语言与其他编程语言共享许多特性，但它也有自己的一些特殊之处。这门语言是由里奇（Ritchie）为自用而开发的，因此有些意外之处在所难免：

- *紧凑高效* — C 语言的词汇量很小，仅包含 30 个关键字，但其大部分能力来自于对键盘上所有符号的利用。C 语言的可执行文件体积小，这在为资源有限的手持设备开发应用程序时成为一个优势。
- *可移植的语言* — C 语言可运行在各种设备上，从手机到超级计算机。由于 C 语言不对硬件做任何假设，符合 ANSI 标准的 C 程序只需少量修改甚至无需修改即可移植到其他平台。
- *自由格式的语言* — 指令或语句可以从一行的任意位置开始。以前，C 语言要求 `#define` 语句从第 1 列开始，但 ANSI C 已经取消了这一限制。
- *强类型语言* — C 语言支持大量数据类型，使程序员能够选择不浪费内存的类型。整数类型多达五种，浮点数类型有三种。不过，C 语言不支持字符串或布尔数据类型。字符串在 C 语言中通过使用 `char` 数据类型的字符数组来实现。
- *区分大小写的语言* — C 语言的关键字和标识符名称（例如变量）区分大小写。所有关键字都被设计为小写，因此你只能使用 `while` 而不能使用 `WHILE` 作为循环语句。变量可以使用任何一种大小写形式，只要记住 `p` 和 `P` 是两个不同的变量即可。
- *语句以分号结尾。* 行的概念在 C 语言中意义不大。只要用分号分隔，一行可以包含多条语句。这一规定也适用于使用花括号定义函数体的结构。例如，下面这个通常需要四行的 `while` 循环也可以写成一行：

  ```c
  while (count < number) { printf("%c", '*'); count = count + 1; }
  ```

  将这个循环与上一个程序 `third_prog.c` 中使用的类似语句进行比较，你就会毫无疑问地认为上述形式看起来并不令人愉快。
- *C 语言可通过函数库进行扩展。* 标准库包含大量有用的函数，用于处理各种编程任务。程序员在处理字符串操作、复杂算术等常规任务时需要用到这个库。你也可以创建自己的函数库，分发它，从而扩展这门语言。

