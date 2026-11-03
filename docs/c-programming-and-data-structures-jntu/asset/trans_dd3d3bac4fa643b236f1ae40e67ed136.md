
如图所示，对队列的操作是FIFO（先进先出）。另外，请注意，当从队列中读取一个项时，该项就被销毁。因此，对队列的读取操作是破坏性的，这与其他数据结构（如链表）的情况不同。如果程序员需要实现队列的非破坏性读取，那么这些值在被读取（并因此自动从队列中移除）时，必须存储在别处以便以后检索。

为了实现队列的写入和读取操作，需要两个指针：start 和 end。一个指针（start）指向队列的当前起始位置（即任意时刻队列中的第一个项）。另一个指针（end）指向队列的当前末尾位置（即队列中可供新项使用的下一个存储位置）。因此，如前所述，对队列的插入和检索将对指针产生如图14.5所示的影响。

![](img/65953ea584e494f3d396b2252cb5ea53_382_0.png)

图14.5 因队列操作引起的指针移动——第I部分

![](img/65953ea584e494f3d396b2252cb5ea53_383_0.png)

图14.5 因队列操作引起的指针移动——第II部分

以下程序说明了队列的工作方式。

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX 1000

/* Global variables */
char *arr[MAX];
int start, end;

/* Function declarations */
char *queue_retrieve (void);
void enter (void);
void queue_store (char *item);
void queue_review (void);
void delete_item (void);
```

图14.6 队列程序——第I部分

```
/* Make an entry into the queue */
void enter (void)
{
    char str[400], *p;

    do
    {
        printf ("Please enter item number : %d", end+1);
        gets (str);

        if(!*str)
            return;
        else
            p = (char *) malloc (strlen (str));
```

```
if (!p)
{
    printf("Insufficient memory\n");
    return;
}

strcpy(p, str);

if (*str)
    queue_store(p);
}
while (*str);
}

/* List queue items */
void queue_review(void)
{
    register int i;

    for (i=start; i<end; i++)
        printf("%d %s", i+1, arr[i]);
}

/* Delete an item from the queue */
void delete_item(void)
{
    char *p;

    p = queue_retrieve();

    if (p == NULL)
        return;

    printf("%s\n", p);
}
```

图14.6 队列程序——第II部分

```
/* store an item */
void queue_store(char *p)
{
    if (end == MAX)
    {
        printf("Queue is full. Cannot add new items.\n");
        return;
    }

    arr[end] = p;
    end++;
}

/* Retrieve an item from the queue */
char* queue_retrieve(void)
{
```

```
if (start == end)
{
    printf ("Queue is empty.\n");
    return NULL;
}

start++;

return arr[start-1];
}
```

图14.6 队列程序——第III部分

## 14.4 循环队列

队列也可以是环形的，在这种情况下，它被称为循环队列。当我们讨论队列时，你可能会认为，随着队列中的项被删除，该项的空间会被回收。然而，事实并非如此。那些队列位置会继续为空。循环队列解决了这个问题。

循环队列不采用线性方法，而是采用环形方法。这就是循环队列没有起点或终点的原因。循环队列的逻辑如图14.7所示。

![](img/65953ea584e494f3d396b2252cb5ea53_385_0.png)

图14.7 循环队列

在循环队列的情况下，函数 queue_store 和 queue_retrieve 将如下改变：

```
void queue_store (char *p)
{
    /* The queue is full if (a) end is one less than start, or (b) end is at the end position of the queue, and start is at the beginning of the queue */

    if ((end+1 == start) || (end+1 == MAX && start == 0))
    {
    printf ("Queue is full. Cannot add new items.\n");
    return;
    }
}
```

### 示例 14.1

中缀表示法的一个示例是 (A/B)+(C-D)*E。

## 前缀表示法

在前缀表示法中，运算符放在数学表达式中的操作数之前。这种表示法也称为波兰表示法。

### 示例 14.2

方程 A/B+C-D*E 的前缀表示法是 +/-AB*-CDE。

## 从中缀表示法转换为前缀表示法

以下算法用于将中缀表达式转换为前缀表达式。

### 算法

- 1. 首先，将栈初始化为空，并反转给定的输入字符串。
- 2. 对于输入字符串中的每个字符
  - 如果输入字符串中的字符是右括号，则将其压入栈中
  - 如果输入字符串中的字符是操作数，则追加到输出。
  - 否则
    - 如果栈为空，或该运算符的优先级高于栈顶运算符，或栈顶是右括号，则
      - 将该运算符压入栈中
    - 否则
      - 从栈中弹出运算符并追加到输出。
- 3. 如果输入字符串中的字符是左括号，则从栈中弹出运算符并将所有运算符追加到输出，直到遇到右括号。从栈中弹出右括号并丢弃它。
- 4. 如果遇到输入字符串的末尾，则迭代循环直到栈不为空
  从栈中弹出内容，并将剩余的输入字符串追加到输出，然后反转输出字符串。

### 示例 14.3

考虑将中缀表达式 A*B/(C-D)+E*(F-G) 转换为其等价的前缀表示法。

首先，要将中缀表达式转换为前缀表示法，请按如下方式反转给定的输入字符串：)G-F(*E+D-C/B*A

| 输入字符串 | 栈操作 | 后缀表示法 |
|---|---|---|
| ) | ) |  |
| G | ) | G |
| - | )- | G |
| F | )- | GF |
| ( | 空 | GF- |
| * | * | GF- |
| E | * | GF-E |
| + | + | GF-E* |
| ) | +) | GF-E* |
| D | +) | GF-E*D |
| - | +)- | GF-E*D |
| C | +)- | GF-E*DC |
| ( | + | GF-E*DC- |
| / | +/ | GF-E*DC- |
| B | +/ | GF-E*DC-B |
| * | +/* | GF-E*DC-BA |
| A | +/* | GF-E*DC-BA |
|  | 空 | GF-E*DC-BA*/+ |

现在，将输出字符串 GF-E*DC-BA*/+ 反转为 +/*AB-CD*E-FG，以获得前缀表示法。因此，给定的中缀表达式被转换为其等价的前缀表示法。中缀表达式到前缀表达式的转换如图14.8所示。

```
#include <stdio.h>
#include <conio.h>
#include <string.h>
#include <ctype.h>
#define MAX 50
char output[MAX];
char stack[MAX];
char input[MAX];
char *s, *t;
int top;
int i ;
/*Initializing Function*/
void Initialize(void);
void SetExpression(char *);
char PopFromStack(void);
void PushOnStack(char);
int priority(char);
void ConvertToPrefix(void);
void main()
{
clrscr();
Initialize();
printf("\nEnter an infix expression: ");
gets(input);
SetExpression(input);
strrev(s);
ConvertToPrefix();
strrev(output);
printf("\nThe Prefix expression is: ");
puts(output);
getch();
}
void Initialize(void)
```

```
{
 top = -1;
 strcpy(output,"");
 strcpy(stack,"");
 i = 0;
}
void SetExpression(char *str)
{
 s = str;
 i = strlen(s);
 *(output + i) = '\0';
 t= output;
}
/*Adding operator to the stack */
void PushOnStack(char c)
{
 if (top == MAX - 1)
 printf("\nStack is full.\n");
 else
 {
 top++;
 stack[top] = c;
 }
}
/*Popping an operator from the stack*/
char PopFromStack(void)
{
 if (top == -1)
 return -1;
 else
 {
 char item = stack[top];
 top--;
 return item;
 }
}
/* Returning the priority of the operator */
int priority(char c)
{
 if (c=='^') return 3;
 if (c=='*' || c=='/' || c=='%')
 return 2;
 else if (c=='+' || c=='-') return 1;
 else return 0;
}

/* Converting the Infix expression to Prefix*/
void ConvertToPrefix(void)
{
 char opr;
 while (*s)
 {
 if (*s=='=' || *s=='^')
 {
 s++;

continue;
}
if (isdigit (*s) || isalpha (*s))
{
while (isdigit (*s) || isalpha (*s))
{
*t = *s;
s++;
t++;
}
}
if (*s == ')')
{
PushOnStack(*s);
s++;
}
if (*s == '=' || *s == '+' || *s == '/' || *s == '%' || *s == '-' || *s == '*')
{
if (top != -1)
{
opr = PopFromStack();
while(priority(opr)>priority(*s))
{
*t = opr;
t++;
opr = PopFromStack();
}
PushOnStack(opr);
PushOnStack(*s);
}
else PushOnStack (*s);
s++;
}
if (*s == ')')
{
opr = PopFromStack();
while (opr != '(')
{
*t = opr;
t++;
opr = PopFromStack();
}
s++;
}
}
while (top != -1)
{
opr = PopFromStack();
*t = opr;
t++;
}
t++;
}
```
