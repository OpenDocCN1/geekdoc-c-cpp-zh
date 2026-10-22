

-2 为真
-1 为真
0 为假

第一个循环在 n 为 3、2 和 1 时执行，但在 n 为 0 时终止。类似地，第二个循环在 n 为 -3、-2 和 -1 时执行，但在 n 为 0 时终止。更一般地，所有非零值都被视为真，只有 0 被识别为假。C 对真值有非常宽容的概念！

或者，你可以说 while 循环只要其测试条件求值为非零就会执行。这使得测试条件基于数值而非真/假。记住，关系表达式在为真时求值为 1，在为假时求值为 0，所以此类表达式确实是数值。

许多 C 程序员利用了测试条件的这一特性。例如，短语 while (goats != 0) 可以被 while (goats) 替换，因为表达式 (goats != 0) 和表达式 (goats) 只有在 goats 的值为 0 时才会变为 0 或假。第一种形式对于刚学习语言的人来说可能更清晰，但第二种形式是 C 程序员最常用的习惯用法。你应该努力熟悉 while (goats) 这种形式，使其对你来说变得自然。

## 真值的麻烦

C 宽容的真值概念会导致麻烦。例如，让我们对《图 6.1》中的程序做一个细微的改动，得到《图 6.8》所示的程序。

### Listing 6.8 The trouble.c Program

```
// trouble.c -- misuse of =
// will cause infinite loop
#include <stdio.h>
int main(void)
{
    long num;
    long sum = 0L;
    int status;

    printf("Please enter an integer to be summed ");
    printf("(q to quit): ");
    status = scanf("%ld", &num);
    while (status = 1)
    {
        sum = sum + num;
        printf("Please enter next integer (q to quit): ");
        status = scanf("%ld", &num);
    }
```

```
printf("Those integers sum to %ld.\n", sum);

return 0;
}
```

Listing 6.8 产生的输出如下：

```
Please enter an integer to be summed (q to quit): 20
Please enter next integer (q to quit): 5
Please enter next integer (q to quit): 30
Please enter next integer (q to quit): q
Please enter next integer (q to quit):
Please enter next integer (q to quit):
Please enter next integer (q to quit):
Please enter next integer (q to quit):
```

...然后一直持续下去，直到你杀掉程序——所以也许你不应该真的尝试运行这个例子。

这个麻烦的例子在 while 测试条件中做了一个改动，用 status = 1 替换了 status == 1。第二个语句是赋值语句，所以它给 status 赋值为 1。此外，赋值语句的值是左边的取值，所以 status = 1 的数值值为 1。因此在实际操作上，while 循环等同于使用 while (1); 也就是说，它是一个永不退出的循环。你输入 q，status 被设为 0，但循环测试会把 status 重置为 1 并开始新一轮。

你可能会想知道，为什么程序一直循环，用户在输入 q 之后却没有机会再输入任何内容。当 scanf() 无法读取指定形式的输入时，它会把不符合规范的输入留在原地以便下次读取。当 scanf() 尝试把 q 读作整数并失败时，它会留下 q。在下一轮循环中，scanf() 会尝试从上次离开的地方继续读取——也就是 q。再次，scanf() 无法把 q 读作整数，所以这个例子不仅设置了一个无限循环，还创建了一个无限失败的循环，这是一个令人望而生畏的概念。幸运的是，计算机目前还没有感情。让计算机永远遵循愚蠢的指令，对它来说并不比成功预测未来 10 年的股市更好或更坏。

不要用 = 代替 ==。某些计算机语言（例如 BASIC）确实对赋值运算符和关系相等运算符使用相同的符号，但这两个操作完全不同（参见图 6.2）。赋值运算符把值赋给左变量。而关系相等运算符则检查左右两侧是否已经相等。它不会改变左手变量的值，如果存在的话。这里有一个例子：

```
canoes = 5      ←Assigns the value 5 to canoes
canoes == 5     ←Checks to see whether canoes has the value 5
```

要小心使用正确的运算符。编译器会让你使用错误的形式，从而产生意想不到的结果。（然而，由于人们经常误用 =，今天大多数编译器都会发出警告，提示你可能不小心使用了它。）如果比较的值之一是常量，你可以把它放在比较的左边以帮助捕获错误：

```
5 = canoes      ←syntax error
5 == canoes     ←Checks to see whether canoes has the value 5
```

要点是，给常量赋值是非法的，所以编译器会把赋值运算符的使用标记为语法错误。许多实践者在使用构造相等性测试的表达式时把常量放在前面。

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_231_0.png)

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_231_1.png)

Figure 6.2  The relational operator == and the assignment operator =.

总之，关系运算符用于形成关系表达式。关系表达式在为真时取值为 1，在为假时取值为 0。诸如 while 和 if 之类的语句通常使用关系表达式作为测试，但可以使用任何表达式作为测试，非零值被识别为“真”，零值被识别为“假”。

## 新的 _Bool 类型

传统上，代表真/假值的变量在 C 中由类型 int 表示。C99 增加了专门用于此类变量的 _Bool 类型。该类型以乔治·布尔命名，这位英国数学家开发了用于表示和解决逻辑问题的代数系统。在编程中，表示真或假的变量被称为布尔变量，因此 _Bool 是布尔变量的 C 类型名。_Bool 变量只能取值为 1（真）或 0（假）。如果你尝试给 _Bool 变量赋一个非零数值，变量会被设为 1，这反映了 C 认为任何非零值都是真的。

### Listing 6.9 The boolean.c Program

```
// boolean.c -- using a _Bool variable
#include <stdio.h>
int main(void)
{
    long num;
    long sum = 0L;
    _Bool input_is_good;

    printf("Please enter an integer to be summed ");
    printf("(q to quit): ");
    input_is_good = (scanf("%ld", &num) == 1);
    while (input_is_good)
    {
        sum = sum + num;
        printf("Please enter next integer (q to quit): ");
        input_is_good = (scanf("%ld", &num) == 1);
    }
    printf("Those integers sum to %ld.\n", sum);

    return 0;
}
```

注意代码如何把比较的结果赋给变量：

```
input_is_good = (scanf("%ld", &num) == 1);
```

这说得通，因为 == 运算符返回的值要么是 1 要么是 0。顺便说一下，包围 == 表达式的括号不是必需的，因为 == 运算符的优先级高于 =；然而，它们可能使代码更易读。还要注意变量名称的选择使 while 循环测试易于理解：

```
while (input_is_good)
```

C99 还提供了 stdbool.h 头文件。该头文件使 bool 成为 _Bool 的别名，并定义 true 和 false 为 1 和 0 的符号常量。包含此头文件允许你编写与 C++ 兼容的代码，C++ 将 bool、true 和 false 定义为关键字。

如果你的系统尚未支持 _Bool 类型，你可以用 int 替换 _Bool，示例将同样工作。

## 关系运算符的优先级

关系运算符的优先级低于算术运算符，包括 + 和 –，而高于赋值运算符。这意味着，例如，

```
x > y + 2
```

与

```
x > (y + 2)
```

相同。它还意味着

```
x = y > 2
```

意味着

```
x = (y > 2)
```

换句话说，如果 y 大于 2，则 x 被赋值为 1，否则为 0；x 并未被赋予 y 的值。

关系运算符的优先级高于赋值运算符。因此，

```
x_bigger = x > y;
```

意味着

```
x_bigger = (x > y);
```

关系运算符本身被组织成两个不同的优先级。

较高优先级组：< <= > >=
较低优先级组：== !=

像大多数其他运算符一样，关系运算符从左到右结合。因此，

```
ex != wye == zee
```

与

```
(ex != wye) == zee
```

相同。首先，C 检查 ex 和 wye 是否不相等。然后，将得到的值 1 或 0（真或假）与 zee 的值进行比较。我们不期望使用这种构造，但我们认为有责任指出这种旁注。

表 6.2 显示了迄今为止引入的运算符的优先级，附录 B 参考部分 II“ C 运算符”中提供了所有运算符的完整优先级排名。

