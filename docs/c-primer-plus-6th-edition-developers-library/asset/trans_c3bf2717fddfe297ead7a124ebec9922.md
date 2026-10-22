
那么break语句呢？它使程序跳出switch，并跳转到switch之后的下一语句（见图7.4）。如果没有break语句，从匹配的标签到switch末尾的所有语句都将被执行。例如，如果从程序中删除所有break语句，然后使用字母d运行该程序，你将得到如下交互：

```
Give me a letter of the alphabet, and I will give an animal name
beginning with that letter.
Please type in a letter; type # to end my act.
d [enter]
desman, aquatic, molelike critter
echidna, the spiny anteater
fisher, a brownish marten
That's a stumper!
Please type another letter or a #.
# [enter]
Bye!
```

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_310_0.png)

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_310_1.png)

图7.4 有break和无break时switch中的程序流程。

从`case 'd' :`到switch末尾的所有语句都被执行了。

顺便提一下，break语句可用于循环和switch，而continue只能用于循环。不过，如果switch语句位于循环内，continue也可以作为switch的一部分使用。在这种情况下，与其他循环一样，continue会使程序跳过循环的其余部分，包括switch的其他部分。

如果你熟悉Pascal，你会看出switch语句与Pascal的case语句类似。最重要的区别是，如果只想处理标签对应的那条语句，switch语句需要使用break。此外，不能用范围作为C的case标签。

switch测试表达式位于括号内，其值应为整数（包括char类型）。case标签必须是整数类型（包括char）的常量或整数常量表达式（只包含整数常量的表达式）。case标签不能使用变量。那么，switch的结构如下：

```
switch (integer expression)
{
    case constant1:
        statements      <--optional
    case constant2:
        statements      <--optional
    default :           <--optional
        statements      <--optional
}
```

## 只读取一行中的第一个字符

animals.c中另一个新特性是它如何读取输入。你可能已经注意到，在示例运行中，当输入dab时，只有第一个字符被处理。这种丢弃行中其余字符的行为，在需要单字符响应的交互式程序中通常很理想。下面的代码实现了这一行为：

```
while (getchar() != '\n')
    continue;      /* skip rest of input line */
```

这个循环从输入中读取字符，直到（并包括）Enter键产生的换行符。注意，函数返回值没有赋给ch，因此这些字符只是被读取并丢弃。因为最后丢弃的字符是换行符，所以下一个要读取的字符是下一行的第一个字符。它由getchar()读取，并赋给外层while循环中的ch。

假设用户一开始就按下Enter，那么遇到的第一个字符就是换行符。下面的代码处理了这种情况：

```
if (ch == '\n')
    continue;
```

## 多个标签

对于同一条语句，可以使用多个case标签，如程序清单7.12所示。

### 程序清单7.12 vowels.c程序

```
// vowels.c -- uses multiple labels
#include <stdio.h>
int main(void)
{
    char ch;
    int a_ct, e_ct, i_ct, o_ct, u_ct;

    a_ct = e_ct = i_ct = o_ct = u_ct = 0;

    printf("Enter some text; enter # to quit.\n");
    while ((ch = getchar()) != '#')
    {
        switch (ch)
        {
            case 'a':
            case 'A':   a_ct++;
                        break;

            case 'e':
            case 'E':   e_ct++;
                        break;

            case 'i':
            case 'I':   i_ct++;
                        break;

            case 'o':
            case 'O':   o_ct++;
                        break;

            case 'u':
            case 'U':   u_ct++;
                        break;

            default:    break;
        }                   // end of switch
    }                       // while loop end
    printf("number of vowels:   A    E    I    O    U\n");
    printf("                    %4d %4d %4d %4d %4d\n",
           a_ct, e_ct, i_ct, o_ct, u_ct);

    return 0;
}
```

例如，如果ch是字母i，switch语句将转到标有`case 'i':`的位置。因为该标签没有关联break，程序流程会继续执行下一条语句，即`i_ct++;`。如果ch是I，程序流程将直接转到该语句。实际上，两个标签指向同一条语句。

严格来说，`case 'U':`的break语句并非必需，因为如果没有它，程序流程会转到switch中的下一条语句，即default情况的break。所以`case 'U'`的break可以省略，从而缩短代码。另一方面，如果以后可能会添加其他情况（例如你可能想把字母y视为有时是元音），那么提前放好break可以防止你忘记添加一个。

下面是一个示例运行：

```
Enter some text; enter # to quit.
I see under the overseer.#
number of vowels:    A    E    I    O    U
                     0    7    1    1    1
```

在这种特定情况下，你可以使用ctype.h函数族中的toupper()函数（参见表7.2）在测试前将所有字母转换为大写，从而避免多个标签：

```
while ((ch = getchar()) != '#')
{
    ch = toupper(ch);
    switch (ch)
    {
        case 'A' :  a_ct++;
                    break;
        case 'E' :  e_ct++;
                    break;
        case 'I' :  i_ct++;
                    break;
        case 'O' :  o_ct++;
                    break;
        case 'U' :  u_ct++;
                    break;
        default :   break;
    }                         // end of switch
}                             // while loop end
```

或者，如果你愿意，可以让ch保持不变，并使用toupper(ch)作为测试条件：

```
switch(toupper(ch))
```

## 总结：使用switch进行多项选择

### 关键字：

```
switch
```

### 一般说明：

程序控制跳转到与表达式值对应的case标签。然后程序流继续执行所有剩余的语句，除非再次使用break语句改变流向。表达式和case标签都必须有整数值（包括char类型），并且标签必须是常量或仅由常量组成的表达式。如果没有case标签与表达式值匹配，则控制转到标记为default的语句（如果存在）。否则，控制传递到switch语句之后的下一条语句。

### 格式：

```
switch (expression)
{
    case label1 : statement1 // use break to skip to end
    case label2 : statement2
    default     : statement3
}
```

标签语句可以多于两个，default情况是可选的。

### 示例：

```
switch (choice)
{
    case 1 :
    case 2 : printf("Darn tootin!\n"); break;
    case 3 : printf("Quite right!\n");
    case 4 : printf("Good show!\n"); break;
    default : printf("Have a nice day.\n");
}
```

如果choice的整数值为1或2，则打印第一条消息。如果为3，则打印第二条和第三条消息。（流程会继续执行下一条语句，因为case 3之后没有break语句。）如果为4，则打印第三条消息。其他值只打印最后一条消息。

## switch与if else

什么时候应该使用switch，什么时候应该使用if else结构？通常你没有选择余地。如果你的选择基于对浮点变量或表达式的求值，就不能使用switch。如果变量必须落在某个范围内，使用switch也不方便。但下面这样写很简单：

```
if (integer < 1000 && integer > 2)
```
