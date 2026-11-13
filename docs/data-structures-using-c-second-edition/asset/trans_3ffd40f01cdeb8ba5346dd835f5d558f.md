

下面给出的算法将中缀表达式转换为后缀表达式，如图 7.22 所示。该算法接受可能包含运算符、操作数和括号的中缀表达式。为简化起见，我们假设中缀运算仅包含取模（%）、乘法（*）、除法（/）、加法（+）和减法（-）运算符，并且优先级相同的运算符从左到右执行。

该算法使用栈来暂时保存运算符。后缀表达式是从左到右使用中缀表达式中的操作数和从栈中移除的运算符获得的。该算法的第一步是将左括号压入栈，并在中缀表达式末尾添加相应的右括号。该算法重复执行，直到栈为空。

- 步骤 1：将 ")" 添加到中缀表达式的末尾
- 步骤 2：将 "(" 压入栈中
- 步骤 3：重复扫描中缀表示法中的每个字符，直到扫描完毕
  - 如果遇到 "("，则将其压入栈中
  - 如果遇到操作数（无论是数字还是字符），则将其添加到后缀表达式中
  - 如果遇到 ")"，则
    - a. 反复从栈中弹出并将其添加到后缀表达式中，直到遇到 "("。
    - b. 丢弃 ")”。也就是说，从栈中移除 "(" 且不将其添加到后缀表达式中
  - 如果遇到运算符 O，则
    - a. 反复从栈中弹出并将每个运算符（从栈中弹出的运算符）添加到后缀表达式中，其优先级与 O 相同或高于 O
    - b. 将运算符 O 压入栈中。
    - [END OF IF]
- 步骤 4：反复从栈中弹出并将其添加到后缀表达式中，直到栈为空
- 步骤 5：退出

图 7.22 将中缀表示法转换为后缀表示法的算法

| 扫描的中缀字符 | 栈 | 后缀表达式 |
|---|---|---|
| A | ( | A |
| - | ( - | A |
| ( | ( - ( | A |
| B | ( - ( / | A B |
| / | ( - ( / | A B |
| C | ( - ( / | A B C |
| ) | ( - ( | A B C / |
| + | ( - + | A B C / |
| * | ( - + * | A B C / |
| D | ( - + * ( | A B C / D |
| % | ( - + * ( % | A B C / D |
| E | ( - + * ( % | A B C / D E |
| * | ( - + * ( % * | A B C / D E |
| F | ( - + * ( % * | A B C / D E F |
| ) | ( - + * | A B C / D E F * % |
| / | ( - + * / | A B C / D E F * % / |
| G | ( - + * / | A B C / D E F * % / G |
| ) | ( - + | A B C / D E F * % / G + |
| * | ( - * | A B C / D E F * % / G + * |
| H | ( - * | A B C / D E F * % / G + * H |
| ) | ( | A B C / D E F * % / G + * H - |

### 示例 7.3 使用图 7.22 给出的算法将以下中缀表达式转换为后缀表达式。
(a) A – ( B / C + ( D % E * F ) / G) * H
(b) A – (B / C + (D % E * F) / G) * H

### 编程示例
6. 编写一个程序，将中缀表达式转换为其等效的后缀表示法。

```c
#include <stdio.h>
#include <conio.h>
#include <ctype.h>
#include <string.h>
#define MAX 100
char st[MAX];
int top=-1;
void push(char st[], char);
char pop(char st[]);
void InfixtoPostfix(char source[], char target[]);
int getPriority(char);
int main()
{
    char infix[100], postfix[100];
    clrscr();
    printf("\n Enter any infix expression : ");
    gets(infix);
    strcpy(postfix, "");
    InfixtoPostfix(infix, postfix);
    printf("\n The corresponding postfix expression is : ");
    puts(postfix);
    getch();
    return 0;
}
void InfixtoPostfix(char source[], char target[])
{
    int i=0, j=0;
    char temp;
    strcpy(target,"");
    while(source[i]!='\0')
    {
        if(source[i]=='(')
        {
            push(st, source[i]);
            i++;
        }
        else if(source[i] == ')')
        {
            while((top!=-1) && (st[top]!='('))
            {
                target[j] = pop(st);
                j++;
            }
            if(top==-1)
            {
                printf("\n INCORRECT EXPRESSION");
                exit(1);
            }
            temp = pop(st); //remove left parenthesis
            i++;
        }
        else if(isdigit(source[i]) || isalpha(source[i]))
        {
            target[j] = source[i];
            j++;
            i++;
        }
        else if (source[i] == '*' || source[i] == '-' || source[i] == '+' ||
                 source[i] == '/' || source[i] == '%')
        {
            while (top!=-1 && (st[top]!= '(') && (getPriority(st[top]) > getPriority(source[i])))
            {
                target[j] = pop(st);
                j++;
            }
            push(st, source[i]);
            i++;
        }
        else
        {
            printf("\n INCORRECT ELEMENT IN EXPRESSION");
            exit(1);
        }
        while((top!=-1) && (st[top]!='('))
        {
            target[j] = pop(st);
            j++;
        }
        target[j]='\0';
    }
}
int getPriority(char op)
{
    if(op=='/' || op == '*' || op=='%')
        return 1;
    else if(op=='+' || op=='-')
        return 0;
}
void push(char st[], char val)
{
    if(top==MAX-1)
        printf("\n STACK OVERFLOW");
    else
    {
        top++;
        st[top]=val;
    }
}
char pop(char st[])
{
    char val=' ';
    if(top==-1)
        printf("\n STACK UNDERFLOW");
    else
    {
        val=st[top];
        top--;
    }
    return val;
}
```

**输出**
Enter any infix expression : A+B*C+D
The corresponding postfix expression is : AB+CD*=

## 后缀表达式的求值

求值的简便性促使计算机将中缀表示法转换为后缀表示法。也就是说，给定一个用中缀表示法编写的代数表达式，计算机首先将该表达式转换为等效的后缀表示法，然后对后缀表达式求值。

这两项任务——将中缀表示法转换为后缀表示法以及对后缀表达式求值——都广泛使用栈作为主要工具。

使用栈，任何后缀表达式都可以非常容易地求值。后缀表达式的每个字符都从左到右扫描。如果遇到的字符是操作数，则将其压入栈中。但是，如果遇到运算符，则从栈中弹出顶部的两个值，并将运算符应用于这些值。然后将结果压入栈中。

让我们来看图 7.23，它展示了求值后缀表达式的算法。

- 步骤 1：在后缀表达式末尾添加一个 ")"
- 步骤 2：扫描后缀表达式的每个字符，并重复步骤 3 和 4，直到遇到 ")"
- 步骤 3：如果遇到操作数，则将其压入栈中。如果遇到运算符 *，则
  - a. 从栈中弹出顶部的两个元素作为 A 和 B，并且
  - b. 计算 B O A，其中 A 是栈顶元素，B 是 A 下方的元素。
  - c. 将求值结果压入栈中
  - [END OF IF]
- 步骤 4：将 RESULT 设置为栈顶元素
- 步骤 5：退出

| 扫描的字符 | 栈 |
|---|---|
| 9 | 9 |
| 3 | 9, 3 |
| 4 | 9, 3, 4 |
| * | 9, 12 |
| 8 | 9, 12, 8 |
| + | 9, 20 |
| 4 | 9, 20, 4 |
| / | 9, 5 |
| - | 4 |

图 7.23 求值后缀表达式的算法

现在让我们举一个使用此算法的示例。考虑给定的中缀表达式 9 – ((3 * 4) + 8) / 4。求值该表达式。

中缀表达式 9 – ((3 * 4) + 8) / 4 可以使用后缀表示法写成 9 3 4 * 8 + 4 / –。请参阅表 7.1，它展示了该过程。

## 编程示例

- 7. 编写一个程序来求值后缀表达式。

```c
#include <stdio.h>
#include <conio.h>
#include <ctype.h>
#define MAX 20
float st[MAX];
int top=-1;
void push(float st[], float val);
float pop(float st[]);
float evaluatePostfixExp(char exp[]);
int main()
{
    float val;
    char exp[100];
    clrscr();
    printf("\n Enter any postfix expression : ");
    gets(exp);
    val = evaluatePostfixExp(exp);
    printf("\n Value of the postfix expression = %.2f", val);
    getch();
    return 0;
}
float evaluatePostfixExp(char exp[])
{
    int i=0;
    float op1, op2, value;
    while(exp[i] != '\0')
    {
        if(isdigit(exp[i]))
```

