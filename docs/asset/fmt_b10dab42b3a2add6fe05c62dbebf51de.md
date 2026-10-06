
# (b) `main()`

```
{
    int i = 1;
    while (i <= 10)
    {
        printf("%d\n", i);
        i++;
    }
}
```

注意，自增运算符 `++` 在每次执行语句 `i++` 时都会将 `i` 的值加 1。同样，为了将变量的值减 1，也提供一个自减运算符 `--`。

然而，永远不要使用 `n++` 来将 `n` 的值加 2，因为 C 语言不识别运算符 `+++`。

## (c) `main()`

```
{
    int i = 1;
    while (i <= 10)
    {
        printf("%d\n", i);
        i++;
    }
}
```

注意 `+=` 是一个复合赋值运算符。它将 `i` 的值加 1。同样，`j = j + 10` 也可以写为 `j += 10`。其他的复合赋值运算符还有 `-=`, `*=`, `/=` 和 `%=`。

## (d) `main()`

```
{
    int i = 0;
    while (i++ < 10)
}
```

## 第 3 章：循环控制结构

```c
printf("%d\n", i);
```

在语句 `while ( i++ < 10 )` 中，首先执行 `i` 的值与 `10` 的比较，然后进行 `i` 的递增。由于 `i` 的递增发生在其使用之后，在这里 `++` 运算符被称为后自增运算符。当控制到达 `printf()` 时，`i` 已经增加了，因此 `i` 必须初始化为 `0`。

```
main()
{
    int i = 0;
    while (++i <= 10)
        printf("%d\n", i);
}
```

在语句 `while ( ++i <= 10 )` 中，首先执行 `i` 的值与 `10` 的比较。由于 `i` 的递增发生在其使用之前，在这里 `++` 运算符被称为前自增运算符。

## for 循环

也许程序员很少使用 `while` 的原因之一是他们太忙于使用 `for` 了，而 `for` 可能是最流行的循环指令。`for` 允许我们在单行中指定关于循环的三点内容：

- (a) 设置循环计数器的初始值。
- (b) 测试循环计数器以确定其值是否达到了预期的重复次数。
- (c) 每当循环内的程序段执行完毕后，增加循环计数器的值。

**`for`** 语句的一般形式如下：

```
for ( initialise counter ; test counter ; increment counter )
{
    do this;
    and this;
    and this;
}
```

让我们使用 **`for`** 写一个简单的单利程序。将此程序与我们使用 **`while`** 编写的程序进行比较。为了更好地理解，下面给出了流程图。

![](img/0a2b9a1d8482fa3ff7aa8a4a25b7ce2b_127_0.png)

图 3.3

```c
/* 计算 3 组 p, n 和 r 的单利 */
main ( {
    int p, n, count;
    float r, si;

    for (count = 1; count <= 3; count = count + 1) {
        printf("Enter values of p, n, and r ");
        scanf("%d %d %f",&n, &r);

        si = p * n * r / 100;
        printf("Simple Interest = Rs.%f\n", si);
    }
}
```

如果将此程序与使用 **`while`** 编写的程序相比，可以看到循环结构所需的三个步骤——初始化、测试和递增——现在已并入 **`for`** 语句。

现在让我们检查 **`for`** 语句是如何执行的：

- 当第一次执行 **`for`** 语句时，`**count**` 的值被设定为初始值 `1`。
- 现在测试条件 **`count <= 3`**。由于 **`count`** 是 `1`，循环体被第一次执行。
- 当到达 **`for`** 的右括号时，控制被传回 **`for`** 语句，在那里 **`count`** 的值增加了 `1`。

## 嵌套循环

正如 `if` 语句可以嵌套一样，**`whiles`** 和 **`for`** 也可以嵌套。为了理解嵌套循环的工作原理，请看下面的程序：

```c
/* 嵌套循环演示 */
main()
{
    int r = 1; r<= 3; r++) /* 外层循环 */
    for (c c = 1; c<= 2; c++) /* 内层循环 */
    {
        sum = r + c;
        printf ("r = %d c = %d sum = %d\n", r, c, sum);
    }
}
```

当你运行此程序时，将得到以下输出：

r = 1 c= 1 sum = 2

r = 1 c= 2 sum = 3

r = 2 c= 1 sum = 3

r = 2 c= 2 sum = 4

r = 3 c= 1 sum = 4

r = 3 c= 2 sum = 5

在这里，对于每个 `r` 的值，内层循环都会循环两次，变量 `c` 的值从 `1` 到 `2`。内层循环

## 第 3 章：循环控制结构

当 `c` 的值超过 `2` 时，循环终止；当 `r` 的值超过 `3` 时，外层循环终止。

如你所示，外层 `for` 循环的体被缩进，内层 `for` 循环的体进一步缩进。这些多级缩进使得程序更易理解。

与其使用两个语句（一个用于计算和，另一个用于打印），你也可以通过以下方式将其合并为单个语句：

```c
printf("r = %d c = %d\n", r, r + c);
```

在这里 `for` 循环的嵌套方式是类似的，`while` 循环也可以进行嵌套。不仅如此，`for` 循环可以出现在 `while` 循环内部，或者 `while` 循环可以出现在 `for` 循环内部。

## for 循环中的多重初始化

```c
for (i = 1, j = 2; j <= 10; j++)
```

多个语句也可以用于 `for` 循环的递增表达式；即，你可以同时递增（或递减）两个或多个变量。然而，在测试表达式中只允许一个表达式。该表达式可以包含多个用逻辑运算符连接的条件。

在初始化表达式中使用多个语句也说明了为什么在 `for` 循环中使用分号来分隔这三个表达式。如果使用了逗号，它们就无法再次用于分隔初始化表达式中的多个语句，而会混淆编译器。

## 无循环循环

Let Us C (让我们学习 C)

我们目前为止的循环执行其内部语句的次数是有限的。但在现实世界的编程中，你会遇到一种情况，即预先不知道循环中的语句将执行多少次。这种情况可以如下所示进行编程：

```c
/* 执行未知次数的循环 */
main() {
    char another;
    int num;
    do {
        printf("Enter a number ");
        scanf("%d",&num);
        printf("square of %d is %d", num * num);
        printf("\nWant to enter another number y/n ");
        scanf("%c",&another);
    } while (another == 'y');
}
```

这里是示例输出...

Enter a number 5

square of 5 is 25

Want to enter another number y/n y

Enter a number 7

square of 7 is 49

Want to enter another number y/n n

在这个程序中，`do-while` 循环将一直执行，直到用户继续回答 `y`。一旦他回答 `n`，循环就会终止，因为条件 `( another == 'y' )` 失败了。这个循环确保了即使第一次提供的就是 `n`，循环中的语句也会至少执行一次。

Javasimplify.blogspot.com

## 第 3 章：循环控制结构

虽然使用 `while` 循环编写此类需求更为简单，但如果需要相同的功能，也可以像下面所示使用 `for` 和 `while` 循环来实现：

```c
/* 使用 for 循环实现的无循环 */
main()
{
    char another = 'y';
    int num;
    for ( ; another == 'y'; )
    {
        printf ("Enter a number ");
        scanf("%d", &num);
```

```c
/* 使用 while 循环实现的无循环 */
main()
{
    char another = 'y';
    int num;

    while ( another == 'y')
    {
        printf ("Enter a number ");
        scanf("%d", &num);
```

## break 语句

我们经常遇到想要立即跳出循环的情况，而不需要等待返回条件测试。`break` 关键字允许我们做到这一点。当在任何循环内部遇到 `break` 时，控制会自动传递到循环后的第一个语句。`break` 通常与 `if` 关联。例如，让我们考虑下面这个例子。

示例：编写一个程序判断一个数是否为素数。素数只能被 1 或它本身整除。

判断一个数是否为素数，我们需要用从 2 到减 1 的所有数字连续除它。如果这些除法中任何一个余数为 0，则该数不是素数。如果没有，则该数是一个素数。以下程序实现了这一逻辑：

```c
main()
{
  int num, i;

  printf ("Enter a number ");
  scanf("%d",&num);

  i=2;
  while (i<= num - 1)
  {
    if ( num % i == 0)
    {
      printf ("Not prime number");
      break;
    }
    i++;
  }
```

## 第 3 章：循环控制结构

在这个程序中，一旦 `num % i` 变为 `0`（即 `num` 可以被 `i` 整除），就会打印 "Not prime number"，并且控制跳出 `while` 循环。为什么 `while` 循环后面还需要 `if` 语句呢？控制有两种方式可以到达循环外部：

(a) 跳出是因为证明 `num` 是素数。
(b) 循环结束是因为 `i` 变成了 `num`。

在第二种情况下，循环终止意味着在 2 到 `num - 1` 之间没有数字可以正好整除 `num`。如果是这样，程序应该打印 "Prime number"。

`break` 关键字只会从它所在的 `while` 循环跳出控制。考虑下面的程序说明了这一事实：

```c
main()
{
    int i=1, j=1;

    while (i++ <= 100)
    {
        while (j++ <= 200)
        {
            if (j == 150)
                break;
            else
                printf("%d %d\n", i, j);
        }
    }
}
```

## continue 语句

在这个程序中，当 `j` 等于 `150` 时，`break` 将控制带出内层 `while` 循环，因为它是放在内层 `while` 中的。

在某些编程情况下，我们想要将控制带到循环的开头，跳过循环内部尚未执行的语句。`continue` 关键字允许我们这样做。在任何循环内部遇到 `continue` 时，控制会自动传递到循环开头。

`continue` 通常与 `if` 关联。例如，考虑下面的程序：

```c
main()
{
  int i, j;

  for (i = 1; i <= 10; i++)
  {
    if (i == 5)
        continue;
    printf("%d\n", i);
  }
}
```

上述程序的输出将：

1 2 3 4 6 7 8 9 10

## 第 3 章：循环控制结构

虽然使用 `while` 循环编写此类需求更为简单，但如果需要相同的功能，也可以像下面所示使用 `for` 和 `while` 循环来实现：

```c
/* 使用 for 循环实现的无循环 */
main()
{
    char another = 'y';
    int num;
    for ( ; another == 'y'; )
    {
        printf ("Enter a number ");
        scanf("%d", &num);
```

```c
/* 使用 while 循环实现的无循环 */
main()
{
    char another = 'y';
    int num;

    while ( another == 'y')
    {
        printf ("Enter a number ");
        scanf("%d", &num);
```

## do-while 循环

注意当 `i` 的值等于 `j` 时，`continue` 语句将控制带到循环开头，跳过循环内部尚未执行的语句。

`do-while` 循环看起来如下：

```c
do
{
  this;
  this;
} while (true);
```

`while` 循环和 `do-while` 循环的工作之间存在细微。。区别在于测试条件的地方。`while` 在执行任何语句之前测试条件。与之相反，`do-while` 在执行语句后测试条件。图 3.5 将解释 `do-while` 的执行。

![](img/02b9a1d8482fa3ff7aa8a45ce2b_140)

这意味着 **`do-while`** 即使条件第一次失败也会至少执行一次其语句。另一方面，**`while`** 如果条件第一次失败将不执行其语句。下面的程序更清楚地说明了这种差异。

```c
main()
{
    while (4 < 1)
        printf ("Hello there\n");
}
```

## break 和 continue 语句

`break` 和 `continue` 在 `do-while` 中的用法与它们在 `while` 或 `for` 循环中的用法一样。`break` 将你带出 `do-while` 并跳过条件测试。`continue` 将你直接送往循环末尾的测试。

## 总结

- (a) C 中提供的三种类型的循环是 `for`、`while` 和 `do-while`。`break` 语句将执行流带出循环。
- (b) `continue` 语句跳过其后语句的执行，并将控制带到循环开头。
- (d) `do-while` 循环用于确保循环内的语句至少执行一次。
- (e) `++` 运算符使操作数加 1，而 `--` 运算符使其减 1。
- (f) `+=`, `-=`, `*=`, `/=`, `%=` 运算符是复合赋值运算符。它们修改左侧操作数的值。

## 练习

## while 循环

[A] 下面程序的输出是什么：

```c
(a) main()
{
  int j;
  while (j <= 10)
  {
    printf("\n%d", j);
    j = j + 1;
  }
}
```

```c
(b) main()
{
  int i = 1;
  while (i <= 10)
  {
    printf("\n%d", i);
  }
}
```

```c
i++;
}
```

```c
(c) main()
{
  int j;
  while ( j <= 10 )
  {
    printf("\n%d", j);
    j = j + 1;
  }
}
```

```c
(d) main()
{
  int x = 1;
  while ( x == 1 )
  {
    x = x - 1;
    printf("\n%d", x);
  }
}
```

```c
(e) main()
{
  int x = 1;
  while ( x == 1)
  x = x - 1;
  printf("\n%d", x);
}
```

```c
(f) main()
{
  char x;
```

```c
while ( x = 0; x <= 255; x++ )
  printf("\nAscii value %d Character %c", x, x);
```

- (g) `main()` {

    int x = 4, y, z;

    y = -x;

    z = x--;

    printf("\n%d %d %d", x, y, z);

}

- (h) `main()` {

    int x = 4, y = 3;

    z = x---y;

    printf("\n%d %d %d", x, y, z);

}

- (i) `main()` {

    while ('a' < 'b')

      printf("\nmalyam is a palindrome"); }

}

- (j) `main()` {

    int i = 10;

    while (i = 20)

      printf("\na computer buff!"); }

}

- (k) `main()` {

    int i;

    while (i = 10)

    {

      printf("\n%d", i);

      i = i + 1;

    }

}
