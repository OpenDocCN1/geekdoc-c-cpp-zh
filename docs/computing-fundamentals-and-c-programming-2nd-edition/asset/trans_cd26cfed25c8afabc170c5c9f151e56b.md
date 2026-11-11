
示例：

```c
enum day {Monday,Tuesday, ... Sunday};
enum day week_st, week_end;
week_st = Monday;
week_end = Friday;
if(week_st == Tuesday)
    week_end = Saturday;
```

编译器会自动从 0 开始为所有枚举常量分配整数值。也就是说，枚举常量 value1 被赋值为 0，value2 被赋值为 1，依此类推。不过，可以通过显式地为枚举常量赋值来覆盖自动分配的值。例如：

```c
enum day {Monday = 1, Tuesday, ... Sunday};
```

这里，常量 Monday 被赋值为 1，其余常量依次递增 1。

枚举变量的定义和声明可以合并在一条语句中。示例：

```c
enum day {Monday, ... Sunday} week_st, week_end;
```

## 4.9 存储类别声明

![](img/11b034a94fc590add0a7808250a38792_146_0.png)

C 语言中的变量不仅具有**数据类型**，还具有**存储类别**，存储类别提供了有关变量位置和可见性的信息。存储类别决定了程序中可以识别该变量的部分。请看下面的例子：

```c
/* 存储类别示例 */
int m;
main()
{
    int i;
    float balance;
    ....
    ....
    function1();
}
function1()
{
    int i;
    float sum;
    ....
    ....
}
```

在 **main** 之前声明的变量 **m** 称为*全局变量*。它可以在程序中的所有函数中使用，无需在其他函数中声明。全局变量也称为*外部变量*。

变量 **i**、**balance** 和 **sum** 称为*局部变量*，因为它们在函数内部声明。局部变量仅在其被声明的函数内部可见和有效，其他函数无法识别它们。

注意，变量 i 在两个函数中都进行了声明。一个函数中 i 值的任何改变都不会影响另一个函数中的 i 值。

C 语言提供了多种存储类别说明符，可用于显式声明变量的作用域和生存期。作用域和生存期的概念仅在多函数和多文件程序中尤为重要，因此存储类别将在后面讨论函数时详细说明。现在只需记住有四种存储类别说明符（auto、register、static 和 extern），其含义如表 4.10 所示。

存储类别是另一种限定符（类似于 long 或 unsigned），可以添加到变量声明中，如下所示：

```c
auto int count;
register char ch;
static int x;
extern long total;
```

静态变量和外部（extern）变量会自动初始化为零。自动（auto）变量除非显式初始化，否则包含未定义的值（称为“垃圾值”）。

**表 4.10** 存储类别及其含义

| 存储类别 | 含义 |
| :--- | :--- |
| **auto** | 局部变量，仅对声明它的函数可见。*默认为 auto。* |
| **static** | 局部变量，即使控制权转移回调用函数后，它仍然存在并保留其值。 |
| **extern** | 全局变量，对文件中的所有函数可见。 |
| **register** | 存储在寄存器中的局部变量。 |

## 4.10 给变量赋值

变量是为在程序语句中使用而创建的，例如：

```c
value = amount + inrate * amount;
while (year <= PERIOD)
{
    ....
    ....
    year = year + 1;
}
```

在第一条语句中，变量 **inrate** 中存储的数值乘以 **amount** 中存储的值，乘积再加上 **amount**，结果存储在变量 **value** 中。只有在变量 **amount** 和 **inrate** 已经被赋予值的情况下，这个过程才有可能完成。变量 **value** 称为*目标变量*。虽然所有变量都声明了其类型，但在表达式中使用的变量（位于计算语句等号（=）右侧的变量）在程序遇到它们之前*必须*被赋值。同样，**while** 语句中的变量 **year** 和符号常量 **PERIOD** 也必须在遇到该语句之前被赋值。

### 4.10.1 赋值语句

可以使用赋值运算符 = 为变量赋值，如下所示：

```
variable_name = constant;
```

我们在第 3 章中已经使用过这样的语句。更多示例如下：

```
initial_value     = 0;
final_value       = 100;
balance           = 75.84;
yes               = 'x';
```

C 语言允许在一行中进行多重赋值。例如：

```
initial_value = 0; final_value = 100;
```

都是有效的语句。

赋值语句意味着“等号”左边变量的值被设置为右边量（或表达式）的值。语句

```
year = year + 1;
```

意味着 **year** 的“新值”等于 **year** 的“旧值”加 1。

在赋值操作期间，C 语言会将右侧值的类型转换为左侧的类型。当实数值被转换为整数时，这可能会涉及截断。

也可以在声明变量时为其赋值。其形式如下：

```
data-type variable_name = constant;
```

一些示例如下：

```
int final_value       = 100;
char yes              = 'x';
double balance        = 75.84;
```

给变量赋予初始值的过程称为*初始化*。C 语言允许使用多重赋值运算符在一条语句中*初始化*多个变量。例如，以下语句

```
p = q = s = 0;
x = y = z = MAX;
```

是有效的。第一条语句将变量 **p**、**q** 和 **s** 初始化为零，第二条语句将 **x**、**y** 和 **z** 初始化为 **MAX**。注意 **MAX** 是在开头定义的符号常量。

请记住，外部变量和静态变量会*默认*初始化为零。未显式初始化的自动变量将包含垃圾值。

## 例题 4.2

图 4.8 中的程序说明了 `scanf` 函数的用法。

程序中第一条可执行语句是一个 `printf`，要求用户输入一个整数。这被称为“提示消息”，显示在屏幕上，如下所示：

```
Enter an integer number
```

一旦用户输入一个整数，计算机就会将该值与 100 进行比较。如果输入的值小于 100，则屏幕上会打印消息

```
Your number is smaller than 100
```

否则，会打印消息

```
Your number contains more than two digits
```

程序针对两种不同输入运行时的输出也显示在图 4.9 中。

```
Program

main()
{
    int number;

    printf("Enter an integer number\n");
    scanf ("%d", &number);

    if ( number < 100 )
        printf("Your number is smaller than 100\n\n");
    else
        printf("Your number contains more than two digits\n");
}

Output

Enter an integer number
54
Your number is smaller than 100
Enter an integer number
108
Your number contains more than two digits
```

**图 4.8** *使用 scanf 函数进行交互式计算*

一些编译器允许将“提示消息”作为 **scanf** 控制字符串的一部分，例如：

```
scanf("Enter a number %d",&number);
```

在图 4.8 中，我们使用了决策语句 **if...else** 来判断数字是否小于 100。

## 例题 4.3

图 4.9 中的程序展示了典型的声明、赋值以及存储在不同类型变量中的值。

变量 **x** 和 **p** 被声明为浮点型变量。注意，我们赋值给 **x** 的 1.234567890000 在不同的输出格式下是如何显示的。在 %.12lf 格式下，**x** 的值显示为 1.234567880630，而实际赋值为 1.234567890000。这是因为变量 **x** 被声明为 **float** 类型，它只能存储到小数点后六位。

被声明为 **int** 类型的变量 **m** 无法正确存储值 54321，而是包含了一些垃圾值。由于该程序是在 16 位机器上运行的，int 变量能存储的最大值仅为 32767。然而，变量 **k**（声明为 **unsigned**）正确存储了值 54321。类似地，**long int** 变量 **n** 正确存储了值 1234567890。

赋值给声明为 **double** 类型的 **y** 的值 9.87654321 被正确存储，但该值在 %lf 格式下打印为 9.876543。请注意，除非另有指定，**printf** 函数总是会将 **float** 或 **double** 值显示到小数点后六位。我们将在后面讨论用于显示数字的输出格式。

