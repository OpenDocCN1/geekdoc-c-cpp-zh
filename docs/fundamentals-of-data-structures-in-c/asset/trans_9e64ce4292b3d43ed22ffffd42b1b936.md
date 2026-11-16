

- 将转换为后缀表达式的部分视为单个操作数 = Z-E [Z=(+YX)]
- 从左到右对具有最高优先级的运算符的子表达式加括号 = (Z-E)
- 将括号内的操作数移到操作数左侧 = (-ZE)
- 替换 z 的值 = (-(+YX) E)
- 替换 Y 的值 = (- (+(*AB) X) E)
- 替换 X 的值 = (- (+(*AB) (/CD) ) E)
- 删除所有括号 = -*+AB/CDE
- 所需的前缀形式是 -*+AB/CDE。

## 3.8.2 将中缀表达式转换为后缀形式

使用计算机对表达式求值可以采用多种方式。有些程序员可能会尝试解析表达式并找出优先级最高的运算符，先计算它们，然后再使用优先级较低的运算符来求值表达式。但如果向表达式中添加了括号和函数，计算将很快变得非常复杂。一种更简单的计算方法是将表达式从中缀表示法转换为后缀表示法。乍一看这可能很奇怪，但在计算机上进行计算时，这种方法要容易得多。

### 将中缀表达式转换为后缀表达式时采用以下过程

- 读取中缀字符串。
- 从左到右遍历表达式。
- 如果遇到操作数，则将其添加到后缀字符串中。
- 如果遇到运算符，则将其压入栈中，只要满足以下任一条件。
  - 栈为空。
  - 栈顶运算符的优先级低于正在处理的运算符的优先级。
- 如果上述所有条件都不满足，则将正在处理的运算符弹出到后缀字符串中。
- 当中缀字符串为空时，将栈中的元素弹出到后缀字符串中以获得结果。

### 中缀转后缀算法

IN_TO_POST(INSTR : STRING, POSTSTR : STRING)
其中 INSTR 包含中缀表达式，POSTSTR 存储结果表达式

步骤 1：初始化栈

步骤 2：While (INSTR != NULL)

步骤 3：CH = 从 INSTR 获取字符

步骤 4：If (CH == 操作数) Then
         将 CH 追加到 POSTSTR
         Else If (CH == '(') Then
         将 CH 压入栈中
         Else If (CH == ')') Then
         从栈中弹出数据并将其追加到 POSTSTR，直到
         从栈中获取 '('
         Else
         While (precedence(栈顶) >= precedence(CH))
         从栈中弹出数据并将其追加到 POSTSTR
         [While 结构结束]
         [步骤 4 If 结构结束]

步骤 5：将 CH 压入栈中。

步骤 6：[步骤 2 While 结构结束]

步骤 7：将栈中的所有数据弹出并追加到 POSTSTR，直到
         栈为空

END_IN_TO_POST()

### 程序 3.5

```c
/* Program to convert infix expression to postfix notation. */
/* in_post.c */
/* */
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#define MAX 9
typedef struct node
{
 char data;
 struct node *next;
}stack;
int push(char);
int pop(char *);
stack *getNode();
void releaseNode(stack *);
void inToPost(char [], char []);
int indexPriority(char P[][2], char data);
stack *topStk = NULL;
```

```c
char ip[MAX][2] = {
    {'(', MAX}, {')', 0 }, {'\0', 0}, {'+', 1},
    {'-', 1}, {'*', 2}, {'/', 2}, {'%', 2},
    {'\0', 3}
};
```

```c
char sp[MAX][2] = {
    {'(', 0}, {')', -1}, {'\0', 0}, {'+', 1},
    {'-', 1}, {'*', 2}, {'/', 2}, {'%', 2},
    {'\0', 3}
};
```

```c
void main()
{
    char inStr[20], postStr[20];
    printf("Enter the infix expression : ");
    scanf("%s", inStr);
    inToPost(inStr, postStr);
    printf("The postfix expression is : %s", postStr);
}
```

```c
int push(char value)
{
    extern stack *topStk;
    stack *newptr;
    newptr = getNode();
    if(newptr == NULL)
    return -1;
    newptr -> data = value;
    newptr -> next = topStk;
    topStk = newptr;
    return 0;
}
```

```c
int pop(char *value)
{
    extern stack *topStk;
    stack *temp;
    if(topStk == NULL)
    return -1;
    temp = topStk;
    topStk = topStk -> next;
    *value = temp -> data;
    releaseNode(temp);
    return 0;
}
```

```c
stack *getNode()
{
    return ((stack *)malloc(sizeof(stack)));
}

void releaseNode(stack *newnode)
{
    free(newnode);
}

void inToPost(char inStr[], char postStr[])
{
    char ch, item;
    int i = 0, st = 0, spr, ipr;
    push('\0');
    while((ch = inStr[st++]) != NULL)
    {
        if(tolower(ch) >= 'a' && tolower(ch) <= 'z')
            postStr[i++] = ch;
        else if(ch == '(')
            push(ch);
        else if(ch == ')')
        {
            pop(&item);
            while(item != '(')
            {
                postStr[i++] = item;
                pop(&item);
            }
        }
        else
        {
            pop(&item);
            spr = indexPriority(sp, item);
            ipr = indexPriority(ip, ch);
            while(sp[spr][1] >= ip[ipr][1])
            {
                postStr[i++] = item;
                pop(&item);
                spr = indexPriority(sp, item);
            }
        }
        push(item);
        push(ch);
    }
    while(!pop(&item))
    postStr[i++] = item;
}
```

```c
int indexPriority(char P[][2], char data)
{
    int ind;
    for(ind = 0; ind < MAX; ind++)
    if(P[ind][0] == data)
    return ind;
}
```

程序显示以下输出

RUN1 输入中缀表达式：a-b*c+d/g
后缀表达式为：abc-*dg/+

RUN2 输入中缀表达式：(A+B)*(C-D)%G
后缀表达式为：AB+CD--G/

## 3.8.3 对后缀表示法中的表达式求值

如果使用栈，对后缀表示法中的表达式求值非常简单。要对后缀表达式进行求值，需从左到右扫描该表达式。变量或常量被压入栈中。当遇到运算符时，使用栈顶两个元素执行指示的操作，并用结果替换栈上的操作数。

### 使用栈对后缀表达式求值时需注意的步骤

- 从左到右遍历表达式。
- 如果遇到操作数，则将其压入栈中。
- 如果看到二元运算符，则从栈中弹出两个元素，使用该运算符对这些操作数求值，并将结果压回栈中。
- 如果看到一元运算符，则从栈中弹出一个元素，使用该运算符对这些操作数求值，并将结果压回栈中。
- 当整个表达式求值结束后，栈上应仅剩下最终结果。如果栈上剩下零个或多于一个操作数，则说明程序不一致，或者表达式无效。

### 对后缀表达式求值的算法

- EVALPOST(POSTEXP : STRING)
- 其中 POSTEXP 包含后缀表达式
- 步骤 1：初始化栈。
- 步骤 2：While (POSTEXP != NULL)
- 步骤 3：ch = 从 POSTEXP 获取字符
- 步骤 4：If (ch == 操作数) Then
  - 读取 CH 的值并将 CH 压入栈中
  - Else If (ch == 运算符) Then
    - 从栈中弹出两个操作数，并使用运算符执行算术运算
      将结果值压入栈中
    - [步骤 4 if 结构结束]
- 步骤 5：[步骤 2 While 结构结束]
- 步骤 6：从栈中弹出数据并返回弹出的数据
- END EVALPOST()

### 程序 3.6

```c
/* Program to evaluate postfix expression using stacks. */
/* evalpost.c */
#include<stdio.h>
#include<ctype.h>
#include<stdlib.h>
typedef struct node
{
    int data;
    struct node *next;
}stack;
stack *topStk = NULL;
int push(int);
int pop(int );
stack *getNode();
int evalPost(char []);
int calc(int, int, char);
void printError();
void main()
{
    char postStr[20];
    printf("\nEnter the postfix string : ");
    gets(postStr);
    printf("\nThe evaluated value of %s is %d",postStr, evalPost( postStr) );
}
```

