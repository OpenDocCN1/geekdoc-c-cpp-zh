
## 数据结构

数据结构是计算机存储、组织数据的方式。数据结构是指相互之间存在一种或多种特定关系的数据元素的集合。

### 常见的数据结构

- 数组
- 链表
- 栈
- 队列
- 树
- 图

### 数组

数组是一种线性表数据结构。它用一组连续的内存空间，来存储一组具有相同类型的数据。

**代码清单 1.12 提到了使用 if-else 语句时发生的编译错误。**

**代码清单 1.12：if-else 语句中的错误**

```c
#include<stdio.h>

int main()
{
    if(1)
    {
        printf("\n IN IF ");
    }
    printf("\n IN Between ");
    else
    {
        printf("\n IN ELSE ");
    }
    getch();
}
```

代码清单 1.12 将给出如下编译错误：

```text
syntax error before "else"
```

在处理 if 和 else 语句时，应牢记：if 块与 else 块之间不应出现任何语句。

### 嵌套 if-else 语句

可以将多个 if-else 语句相互嵌套。当存在复杂的决策问题，并且一个分支中可能有多个分支或子分支时，就需要这种结构。

考虑一个场景：我们需要根据学生在考试中获得的百分比来给他们评定等级。评分标准如下：

- 91% 及以上 – A 等级
- 75% - 90% - B 等级
- 50% - 74% - C 等级
- 35% - 49% - 仅及格
- 低于 35% - 不及格

代码清单 1.13 展示了 if-else 语句的嵌套：

**代码清单 1.13：if-else 语句的嵌套**

```c
#include<stdio.h>

int main()
{
    int marks_obtained;
    float percentage;

    printf("\n Enter marks obtained by candidate out of 500 ");
    scanf("%d",&marks_obtained);

    percentage = marks_obtained/5;

    if(percentage > 90)
    {
        printf("\n Grade Obtained is A");
    }
    else
    {
        if(percentage > 74)
        {
            printf("\n Grade Obtained is B");
        }
        else
        {
            if(percentage > 50)
            {
                printf("\n Grade obtained is C");
            }
            else
            {
                if(percentage > 39)
                {
                    printf("\n Grade obtained is Just Passed");
                }
                else
                {
                    printf("\n Candidate Failed");
                }
            }
        }
    }
    getch();
}
```

代码清单 1.13 的输出如下：

```text
Enter marks obtained by candidate out of 500 490

Grade Obtained is A

Enter marks obtained by candidate out of 500 100

Candidate Failed
```

在代码清单 1.13 中，第二个 if-else 结构嵌套在第一个 if-else 结构的 else 块中。其思路是，如果第一个 if 语句失败，控制流就会转移到相应 else 块内的语句，然后执行第一个 else 块中的 if-else 块。嵌套并不一定总要发生在 else 块内部；它也可以发生在 if 块内部。然而，代码必须正确缩进，这一点极其重要；否则可能会出现 if-else 块位置错误。此外，将单条语句和多条语句都放在花括号内是一种良好的编程实践，因为这会提高代码的可读性。

嵌套有不同的类型。其中一些如下所述：

- 1. `if(expression)`
  `statement;`
- 2. `if(expression)`
  ```c
  {
      statements;
  }
  ```

## 第1章

### 代码清单 1.15：OR 运算符的用法

```c
#include<stdio.h>

int main()
{
    int sex,exp;

    printf("\n Enter type of candidate (1 for MALE 2 for FEMALE) ");
    scanf("%d",&sex);
    printf("\n Enter Years of Experience ");
    scanf("%d",&exp);

    if(((sex == 1) && (exp >= 3)) || ((sex == 2) && (exp >=2)))
        printf("\n Candidate Accepted");
    else
        printf("\n Candidate Rejected");
    getch();
}
```

代码清单 1.15 的输出如下：

```text
Enter type of candidate (1 for MALE 2 for FEMALE) 1

Enter Years of Experience 4

Candidate Accepted
```

在代码清单 1.15 中，如果任意一个表达式变为真，OR 运算符就会帮助执行这组语句。该代码还表明，我们也可以一起使用多个逻辑运算符。NOT 运算符有自己不同的解释。顾名思义，NOT 运算符表示对表达式取反。考虑以下代码片段：

```c
if(!expression)
```

在这种情况下，如果表达式返回假，那么 NOT 运算符会反转结果并将其变为真，因此 if 块内的语句会被执行。

代码清单 1.16 展示了 NOT 运算符在 C 中的实现。

### 代码清单 1.16：NOT 运算符在 C 中的实现

```c
#include<stdio.h>

int main()
{
    int variable=0;
    if(!variable)
        printf("\n variable is zero");
    else
        printf("\n variable is non-zero");

    getch();
}
```

代码清单 1.16 中提到的代码片段将执行 if 块内的语句；NOT 运算符是下面所述条件语句的另一种写法

```c
if(variable == 0)
```

而是写成

```c
if(!variable)
```

我们将在本章末尾找到这些运算符的更多示例。

### else-if 语句

else-if 语句是编写决策程序的另一种方式。

代码清单 1.17 展示了一个使用 else-if 块编写的程序：

**代码清单 1.17：在 C 中编写 else-if 语句**

```c
#include<stdio.h>

int main()
{
    int marks_obtained;
    float percentage;

    printf("\n Enter marks obtained by candidate out of 500 ");
    scanf("%d",&marks_obtained);

    percentage = marks_obtained/5;

    if(percentage > 90)
    {
        printf("\n Grade Obtained is A");
    }
    else if(percentage > 74)
    {
        printf("\n Grade Obtained is B");
    }
    else if(percentage > 49)
    {
        printf("\n Grade Obtained is C");
    }
    else if(percentage > 34)
    {
        printf("\n Grade Obtained is Just Passed");
    }
    else
        printf("\n Candidate Failed");

    getch();
}
```

代码清单 1.17 的输出如下：

```text
Enter marks obtained by candidate out of 500 490

Grade Obtained is A
```

else-if 语句是编写 if-else 语句的另一种方式。

以下代码片段展示了一个通用 if-else 语句的示例：

```c
if(expression)
{
    statements;
}
else
{
    if(expression)
        statement;
}
```

前面的代码可以使用 else-if 结构重排为：

```c
if(expression)
{
    statements;
}
else if(expression)
    statement;
```

### 条件运算符

决策所需的另一组相关运算符是 ? 和 :。这些运算符通常被称为三元运算符，因为它们接受三个参数。组合在一起，它们构成 if-else 语句的简化版本。

```text
expression ? statement 1 : statement2
```

上面显示的表达式意味着，如果表达式为真，则执行语句 1；否则执行语句 2。代码清单 1.18 展示了如何在 C 中编写条件运算符：

**代码清单 1.18：在 C 中编写条件运算符**

```c
#include<stdio.h>

int main()
{
    int varA=10;

    (varA < 5 ? printf("\n Less than 5"):printf("\n Greater than 5"));

    getch();
}
```

代码清单 1.18 的输出如下：

```text
Greater than 5
```

代码清单 1.19 展示了条件运算符在 C 中的使用：

**代码清单 1.19：C 中的条件运算符**

```c
#include<stdio.h>

int main()
{
    int gender,age;

    printf("\n Enter your Gender (1. MALE/ 2. FEMALE)");
    scanf("%d",&gender);
    printf("\n Enter age ");
    scanf("%d",&age);

    ((gender == 1) ?
        ((age > 18) ? printf("\n Qualified"):printf("\n Disqualified"))
        :
        ((age > 24) ? printf("\n Qualified"):printf("\n Disqualified"))
    );
    getch();
}
```

使用条件运算符的主要缺点之一是，在条件语句的真块和假块中只能有一条语句。因此，这种结构并不经常使用。

