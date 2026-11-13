

当 A 调用 B 时，B 被压入系统栈顶。当 B 的执行完成后，系统控制将从栈中移除 B 并继续执行。

当 B 调用 C 时，C 被压入系统栈顶。当 C 的执行完成后，系统控制将从栈中移除 C 并继续执行。

当 C 调用 D 时，D 被压入系统栈顶。当 D 的执行完成后，系统控制将从栈中移除 D 并继续执行。

当 D 调用 E 时，E 被压入系统栈顶。当 E 的执行完成后，系统控制将从栈中移除 D 并继续执行。

图 7.2 函数调用时的系统栈

为了跟踪每个活动函数的返回点，会使用一种称为系统栈或调用栈的特殊栈。每当一个函数调用另一个函数时，调用函数会被压入栈顶。这是因为在被调用函数执行完毕后，控制权会返回给调用函数。请看图 7.2，它展示了这一概念。

现在当函数 E 执行时，函数 D 将从栈顶移除并执行。一旦函数 D 完全执行完毕，函数 C 将从栈中移除以供执行。整个过程将重复，直到所有函数都执行完毕。让我们来看看每个函数执行后的栈。如图 7.3 所示。

系统栈确保函数的正确执行顺序。因此，在处理顺序非常重要的情况下，栈被频繁使用，尤其是在处理需要推迟到其他条件满足后再进行的情况。

栈可以使用数组或链表实现。在以下章节中，我们将讨论基于数组和链表的栈实现。

当 E 执行完毕后，D 将被移除以供执行。

当 C 执行完毕后，B 将被移除以供执行。

当 D 执行完毕后，C 将被移除以供执行。

当 B 执行完毕后，A 将被移除以供执行。

图 7.3 被调用函数返回到调用函数时的系统栈

## 7.2 栈的数组表示

在计算机内存中，栈可以表示为线性数组。每个栈都有一个名为 top 的相关变量，用于存储栈顶元素的地址。元素将在此位置添加或删除。还有一个名为 max 的变量，用于存储栈可容纳的最大元素数量。

如果 top = NULL，则表示栈为空；如果 top = max-1，则表示栈已满。（你一定在想为什么我们写的是 max-1。这是因为数组索引从 0 开始。）请看图 7.4。

| A | AB | ABC | ABCD | ABCDE | | | | | |
|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | TOP = 4 | 5 | 6 | 7 | 8 | 9 |

图 7.4 栈

图 7.4 中的栈显示 top = 4，因此插入和删除将在此位置进行。在上述栈中，仍可存储五个更多元素。

## 7.3 栈上的操作

栈支持三种基本操作：push、pop 和 peek。push 操作将元素添加到栈顶，pop 操作从栈顶移除元素。peek 操作返回栈顶元素的值。

### 7.3.1 Push 操作

push 操作用于向栈中插入元素。新元素将添加到栈的最顶端位置。但是，在插入值之前，我们必须先检查 top=MAX-1 是否成立，因为如果是这种情况，则栈已满，无法再进行插入。如果尝试向已满的栈中插入值，将打印溢出消息。请考虑图 7.5 中的栈。

![](img/be6359df08208122bec6fad1103de211_234_0.png)

图 7.5 栈

要插入值为 6 的元素，我们首先检查 top=MAX-1。如果条件为假，则递增 top 的值，并在 stack[top] 指示的位置存储新元素。因此，更新后的栈如图 7.6 所示。

![](img/be6359df08208122bec6fad1103de211_234_1.png)

图 7.6 插入后的栈

```
Step 1: IF TOP = MAX-1
    PRINT "OVERFLOW"
    GOTO Step 4
    [END OF IF]
Step 2: SET TOP = TOP + 1
Step 3: SET STACK[TOP] = VALUE
Step 4: END
```

图 7.7 向栈中插入元素的算法

图 7.7 显示了向栈中插入元素的算法。在第 1 步中，我们首先检查溢出条件。在第 2 步中，top 递增，以便它指向数组中的下一个位置。在第 3 步中，值被存储在 top 指向的栈位置中。

### 7.3.2 Pop 操作

pop 操作用于从栈中删除最顶端元素。但是，在删除值之前，我们必须先检查 top=NULL 是否成立，因为如果是这种情况，则表示栈为空。如果尝试从已空的栈中删除值，将打印下溢消息。请考虑图 7.8 中的栈。

![](img/be6359df08208122bec6fad1103de211_234_2.png)

图 7.8 栈

要删除最顶端元素，我们首先检查 top=NULL。如果条件为假，则递减 top 指向的值。因此，更新后的栈如图 7.9 所示。

![](img/be6359df08208122bec6fad1103de211_234_3.png)

图 7.9 删除后的栈

```
Step 1: IF TOP = NULL
    PRINT "UNDERFLOW"
    Goto Step 4
    [END OF IF]
Step 2: SET VAL = STACK[TOP]
Step 3: SET TOP = TOP - 1
Step 4: END
```

图 7.10 从栈中删除元素的算法

图 7.10 显示了从栈中删除元素的算法。在第 1 步中，我们首先检查下溢条件。在第 2 步中，top 指向的栈位置的值存储在 val 中。在第 3 步中，top 递减。

### 7.3.3 Peek 操作

Peek 是一种操作，它返回栈顶元素的值，而不将其从栈中删除。peek 操作的算法如图 7.11 所示。

但是，Peek 操作首先检查栈是否为空，即如果 TOP = NULL，则打印适当消息，否则返回值。请考虑图 7.12 中的栈。

```
Step 1: IF TOP = NULL
    PRINT "STACK IS EMPTY"
    Goto Step 3
    [END OF IF]
Step 2: RETURN STACK[TOP]
Step 3: END
```

图 7.11 Peek 操作算法

![](img/be6359df08208122bec6fad1103de211_235_0.png)

图 7.12 栈

在这里，Peek 操作将返回 5，因为它是栈顶元素的值。

## 编程示例

- 1. 编写一个程序，在栈上执行 Push、Pop 和 Peek 操作。

```
#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#define MAX 3 // Altering this value changes size of stack created
int st[MAX], top=-1;
void push(int st[], int val);
int pop(int st[]);
int peek(int st[]);
void display(int st[]);
int main(int argc, char *argv[]) {
int val, option;
do
{
printf("\n\n *****MAIN MENU*****");
printf("\n 1. PUSH");
printf("\n 2. POP");
printf("\n 3. PEEK");
printf("\n 4. DISPLAY");
printf("\n 5. EXIT");
printf("\n Enter your option: ");
scanf("%d", &option);
switch(option)
{
case 1:
printf("\n Enter the number to be pushed on stack: ");
scanf("%d", &val);
push(st, val);
break;
case 2:
val = pop(st);
if(val != -1)
printf("\n The value deleted from stack is: %d", val);
break;
case 3:
val = peek(st);
if(val != -1)
printf("\n The value stored at top of stack is: %d", val);
break;
case 4:
    display(st);
    break;
}while(option != 5);
return 0;
}
void push(int st[], int val)
{
    if(top == MAX-1)
    {
        printf("\n STACK OVERFLOW");
    }
    else
    {
        top++;
        st[top] = val;
    }
}
int pop(int st[])
{
    int val;
    if(top == -1)
    {
        printf("\n STACK UNDERFLOW");
        return -1;
    }
    else
    {
        val = st[top];
        top--;
        return val;
    }
}
void display(int st[])
{
    int i;
    if(top == -1)
    printf("\n STACK IS EMPTY");
    else
    {
        for(i=top;i>=0;i--)
        printf("\n %d",st[i]);
        printf("\n"); // Added for formatting purposes
    }
}
int peek(int st[])
{
    if(top == -1)
    {
        printf("\n STACK IS EMPTY");
        return -1;
    }
    else
    return (st[top]);
}
```

