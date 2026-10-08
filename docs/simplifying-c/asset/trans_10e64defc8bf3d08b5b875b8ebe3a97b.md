
该头文件包含宏定义、常量，以及用于不同标准输入和输出操作的功能和类型的原型。我们已经学习了如何在程序中引入头文件。下一节将讨论格式化函数的用法。

## 4.3 格式化函数

格式化函数被认为是通用函数。正如表1所示，这些函数用于输入或输出所有类型的数据，无论是 char、int、float 还是 double。格式化函数的一般语法如3图所示：

![](img/5d422ba7108ffdf64376be51eaf0c459_75_0.png)

从3图可以看出，函数名可以是 `scanf` 或 `printf`。格式说明符字符串指定了变量值应被读取或写入的数据类型格式。标识符列表在 `scanf` 的情况下由变量的地址组成，而在 `printf` 的情况下由变量的名称组成。在我们继续深入之前，让我们理解一下变量地址和名称的概念。在 C 程序中定义的标识符与三个实体相关联，如4图所示：

![](img/5d422ba7108ffdf64376be51eaf0c459_75_1.png)

从4图中可以观察到，标识符具有名称、值和地址。有时我们需要在表达式中利用标识符的值并使用标识符的名称。另一方面，如果我们想存储用户输入的值，我们则引用标识符的地址。在 C 中，通过在标识符名称前加 & 符号（ampersand）来访问标识符的地址。新手程序员犯的最常见错误是在读取数据时不使用 & 符号。现在让我们看看格式化函数是如何工作的。

### 输入函数

接收用户输入的操作几乎存在于所有程序中。C 语言提供了一个名为 `scanf` 的预定义函数来获取输入。该函数的语法如下：

```c
scanf("format string", address list of identifiers);
```

上述语法由两部分组成，即标识数据类型的格式说明符和标识符的地址列表。格式字符串由一组预定义的字母组成。每个字母代表一个特定的数据类型。可以在一次 `scanf` 调用中读取多个数据。在这种情况下，格式说明符通常包含由空格分隔的格式代码，而地址列表则包含需要存储数据的标识符的地址。表2列出了用于读取或写入数据的格式说明符：

**表2：格式说明符字符串**

| 数据值 | 数据类型 | 格式代码 |
| :--- | :--- | :--- |
| 整数 | short int / int | %d 或 %i |
| | unsigned int | %u |
| | long unsigned int | %lu |
| | long int | %ld |
| 十六进制 | int | %x 或 %p |
| 八进制 | int | %o |
| 字符 | signed char | %c |
| | unsigned char | %c |
| | char * (字符串) | %s |
| 实数 | float | %f 或 %g |
| | double | %lf |
| | long double | %Lf |

从表2可以观察到，不同的数据类型有不同的格式说明符。格式说明符需要按照希望数据输入的顺序书写。前一章编写的程序已经使用了 `scanf` 函数。程序1展示了 `scanf` 函数的使用：

#### 程序 1

```c
/* 演示 scanf 用法的程序 */
#include <stdio.h>
/* main 函数开始 */
main()
{
    /* 声明变量 */
    int i_first;
    double d_second;
    char c_choice;

    /* 读取并打印值 */
    printf( "\nEnter the values : ");
    scanf ( "%d%lf%c",&i_first, &d_second, &c_choice);
    printf( "\nValues of the variables are %d %lf %c\n" ,i_first,d_second,c_choice);
    return;
}
/* main 函数结束 */
```

**输出 1：**

```
Enter the values: 45 57.76 g
Values of the variables are 4557 0.760000 g
```

**输出 2：**

```
Enter the values: 75 65.50 t
Values of the variables are 75 65.500000
```

在程序1中，我们使用了三个变量：两个数值型和一个字符型。程序只是要求我们输入值，但没有指定输入的顺序。此外，我们注意到格式字符串中没有分隔符来分隔格式代码。

在输出1中，用户希望将 45、57.76 和 g 输入到变量中。然而，C 语言将值分配为 4557、0.760000 和 g。在输入的三个值中，只有一个值似乎符合用户的选择。让我们尝试理解这里发生了什么。用户从键盘输入了 4557.76g，且值之间未插入任何分隔符。来自键盘的数据生成了一个字符流。当结果需要打印时，输出函数试图将数据转换为整数。由于流数据 4557 中间没有任何小数点，它被假定为整数。当从流中读取 .（点）时，编译器试图将其映射到下一个变量数据类型；因此，.76 被分配给变量 `d_second`，最后 g 被分配给 `c_choice`。

为了解决这个问题，输出2中的用户使用空格作为分隔符来输入数据。用户在此处输入的条目是 75、65.50 和 t。可以看到前两个变量被分配了适当的值，而最后一个似乎有误。事实上，输出是完全正确的。在这种情况下，数据首先被转换为流。当遇到第一个空格时，值 75 被分配给 `i_first`。然后编译器丢弃空格并将 65.50 分配给 `d_second`。65.50 之后的空格是问题所在，因为空格也被视为 C 语言的有效字母，编译器将空格的值分配给 `c_choice`。由于空格表示不可打印字符，因此在输出中不可见。此时我们可能会疑惑输入时输入的字符 t 去哪了。它仍然在流中；根据新变量的数据类型，它要么被分配给新变量，要么从考虑中丢弃。如果下一个要读取的变量是字符数据类型，t 将被分配给它；在所有其他情况下，它将从流中简单丢弃。

前文提到的 C 语言特性要求程序员在编写程序时要稍加小心。程序员在此处需要做的微小修改是通过指定适当的消息来询问输入。程序2展示了程序1的修改版本：

#### 程序 2

```c
/* 演示 scanf 用法的程序 */
#include <stdio.h>
/* main 函数开始 */
main()
{
/* 声明变量 */
int i_first;
double d_second;
char c_choice;

/* 读取并打印值 */
printf("\nEnter the value of i_first: ");
scanf("%d",&i_first);
printf("\nEnter the value of d_second: ");
scanf("%lf",&d_second);
printf("\nEnter the value of c_choice: ");
scanf("%c",&c_choice);
printf("\nValues of the variables are %d %lf %c\n"
, i_first,d_second,c_choice);
return;
}
/* main 函数结束 */
```

**输出 1：**

```
Enter the value of i_first: 56
Enter the value of d_second: 75.66
Enter the value of c_choice: 
Values of the variables are 56 75.660000
```

在程序2中，通过将一个 `scanf` 语句转换为多个 `scanf` 语句，前两个变量的读取问题很容易得到解决。然而，字符数据的问题仍然存在；在这种情况下，问题是 Enter 键。如果我们先读取字符值，这个问题就不会发生。为了解决这个问题，我们需要使用临时变量，以便 Enter 键的值被分配给该临时变量。我们可以在这里使用非格式化函数。程序3展示了临时变量的用法：

#### 程序 3

```c
/* 演示临时变量用法的程序 */

#include<stdio.h>
/* main 函数开始 */
main()
{
    /* 声明变量 */
    int i_first;
    double d_second;
    char c_choice, c_temp;

    printf("Enter the value of i_first: ");
    scanf("%d", &i_first);
    printf("Enter the value of d_second: ");
    scanf("%lf", &d_second);

    /* 使用临时变量清除流 */
    c_temp=getchar();

    printf("\nEnter the value of c_choice: ");
    scanf("%c", &c_choice);
    printf("\nValues of the variables are %d %lf %c\n",
           i_first, d_second, c_choice);
    return;
}
/* main 函数结束 */
```

**输出 1：**

```
Enter the value of i_first: 45
Enter the value of d_second: 78.25
Enter the value of c_choice: h
Values of the variables are 45 78.250000 h
```

**输出 2：**

```
Enter the value of i_first: r
Enter the value of d_second: 
Enter the value of c_choice: 
Values of the variables are -28851 0.000000
```

**输出 3：**

```
Enter the value of i_first: 56
Enter the value of d_second: h
Enter the value of c_choice: 
Values of the variables are 56 0.000000
```

在程序3中，语句 `c_temp = getchar();` 的使用解决了我们的问题，我们能够看到如输出1所示的预期输出。这里另一个值得注意的有趣之处在于，如果遇到任何无效字符，编译器将终止值的读取。观察到在输出2中，在消息 *Enter the value of i_first* 之后，编译器期望一个整数值，但接收到了一个字符。在这种情况下，编译器终止输入并直接给出输出。这里的输出被视为垃圾数据，因为它没有用处。输出3中发生了类似的情况。

C 允许我们由现有的原始数据类型构建派生数据类型。一种这样的数据类型是数组。C 中的字符数组表示为字符串。让我们现在学习如何在字符串中输入数据。格式代码 `%s` 允许用户从键盘读取字符串。程序4说明了如何在 C 中读取和显示字符串：

