
## 自我复习练习答案

12.1 a) 引用。 b) malloc。 c) 栈。 d) 谓词。 e) FIFO。 f) 链接。 g) free。 h) 队列。 i) 树。 j) LIFO。 k) 二叉。 l) 根。 m) 子节点, 子树。 n) 叶。 o) 中序, 前序, 后序。

12.2 可以在链表的任何位置插入节点并从链表的任何位置删除节点。然而，栈中的节点只能在栈顶插入，只能从栈顶删除。

12.3 队列同时具有指向其头和尾的指针，以便节点可以在尾部插入并从头部删除。栈只有一个指向栈顶的指针，节点的插入和删除都在该位置进行。

```
GradeNodePtr startPtr = NULL;
```

```
GradeNodePtr newPtr;
newPtr = malloc(sizeof(GradeNode));
strcpy(newPtr->lastName, "Jones");
newPtr->grade = 91.5;
newPtr->nextPtr = NULL;
```

插入 "Adams" 时：
previousPtr 为 NULL，currentPtr 指向列表中的第一个元素。
newPtr->nextPtr = currentPtr;
startPtr = newPtr;
插入 "Thompson" 时：
previousPtr 指向列表中的最后一个元素（包含 "Smith"）
currentPtr 为 NULL。
newPtr->nextPtr = currentPtr;
previousPtr->nextPtr = newPtr;
插入 "Pritchard" 时：
previousPtr 指向包含 "Jones" 的节点
currentPtr 指向包含 "Smith" 的节点
newPtr->nextPtr = currentPtr;
previousPtr->nextPtr = newPtr;

```
currentPtr = startPtr;
while (currentPtr != NULL) {
    printf("Lastname = %s\nGrade = %6.2f\n", currentPtr->lastName, currentPtr->grade);
    currentPtr = currentPtr->nextPtr;
}
```

```
currentPtr = startPtr;
while (currentPtr != NULL) {
    tempPtr = currentPtr;
    currentPtr = currentPtr->nextPtr;
    free(tempPtr);
}
startPtr = NULL;
```

12.5 中序遍历为：
11 18 19 28 32 40 44 49 69 71 72 83 92 97 99
前序遍历为：
49 28 18 11 19 40 32 44 83 71 69 72 97 92 99
后序遍历为：

```
    11 19 32 44 40 28 69 72 71 92 99 97 83 49
```

## 练习

- **12.6 (连接列表)** 编写一个程序，将两个字符链表连接起来。程序应包含函数 concatenate，该函数接收指向两个列表的指针作为参数，并将第二个列表连接到第一个列表。

- **12.7 (合并有序列表)** 编写一个程序，将两个整数有序列表合并为一个整数有序列表。函数 merge 应接收要合并的每个列表的第一个节点的指针，并返回合并后列表的第一个节点的指针。

- **12.8 (向有序列表中插入)** 编写一个程序，按顺序将 25 个 0 到 100 的随机整数插入到链表中。程序应计算元素的总和和元素的浮点平均值。

- **12.9 (创建链表然后反转其元素)** 编写一个程序，创建包含 10 个字符的链表，然后创建该列表的反向副本。

- **12.10 (反转句子的单词)** 编写一个程序，输入一行文本并使用栈打印反转后的行。

- **12.11 (回文测试器)** 编写一个程序，使用栈确定一个字符串是否为回文（即字符串正向和反向拼写相同）。程序应忽略空格和标点符号。

- **12.12 (中缀到后缀转换器)** 栈被编译器用于帮助评估表达式和生成机器语言代码的过程。在本练习和下一个练习中，我们研究编译器如何评估仅由常量、运算符和括号组成的算术表达式。

人们通常写表达式如 3 + 4 和 7 / 9，其中运算符（此处为 + 或 /）写在运算对象之间——这称为中缀表示法。计算机“偏好”后缀表示法，其中运算符写在其两个运算对象的右侧。上述中缀表达式在后缀表示法中分别显示为 3 4 + 和 7 9 /。

为了评估复杂的中缀表达式，一些编译器首先将表达式转换为后缀表示法，然后评估后缀版本。每种算法只需要对表达式进行一次从左到右的扫描。每种算法都使用栈来支持其操作，并且在每种算法中栈的使用目的不同。

在本练习中，你将编写一个中缀到后缀转换算法的版本。在下一个练习中，你将编写后缀表达式求值算法的版本。

编写一个程序，将普通的中缀算术表达式（假设输入的是有效表达式）与单数字整数如

```
`(6 + 2) * 5 - 8 / 4`
```

转换为后缀表达式。前述中缀表达式的后缀版本是

```
`6 2 + 5 * 8 4 / -`
```

程序应将表达式读入字符数组 infix 并使用本章中实现的栈函数帮助在字符数组 postfix 中创建后缀表达式。创建后缀表达式的算法如下：

1. 将左括号 '(' 压入栈。
2. 在 infix 末尾追加右括号 ')'。
3) 当栈不为空时，从左到右读取 infix 并执行以下操作：
如果 infix 中的当前字符是数字，将其复制到 postfix 的下一个元素。
如果 infix 中的当前字符是左括号，将其压入栈。
如果 infix 中的当前字符是运算符，
弹出栈顶的运算符（如果有）当它们与当前运算符具有相等或更高的优先级时，并将弹出的运算符插入 postfix。
将 infix 中的当前字符压入栈。
如果 infix 中的当前字符是右括号
从栈顶弹出运算符并将其插入 postfix，直到栈顶为左括号。
弹出（并丢弃）栈中的左括号。

表达式中允许以下算术运算：

- + 加法
- - 减法
- * 乘法
- / 除法
- ^ 指数运算
- % 余数

栈应使用以下声明维护：

```
struct stackNode {
    char data;
    struct stackNode *nextPtr;
};
typedef struct stackNode StackNode;
typedef StackNode *StackNodePtr;
```

程序应由 main 和另外八个函数组成，函数头如下：

```
void convertToPostfix(char infix[], char postfix[])
Convert the infix expression to postfix notation.
int isOperator(char c)
Determine whether c is an operator.
int precedence(char operator1, char operator2)
Determine whether the precedence of operator1 is less than, equal to, or greater than the precedence of operator2. The function returns -1, 0 and 1, respectively.
void push(StackNodePtr *topPtr, char value)
Push a value on the stack.
char pop(StackNodePtr *topPtr)
Pop a value off the stack.
char stackTop(StackNodePtr topPtr)
Return the top value of the stack without popping the stack.
int isEmpty(StackNodePtr topPtr)
Determine whether the stack is empty.
void printStack(StackNodePtr topPtr)
Print the stack.
```

```
int isEmpty(StackNodePtr topPtr)
Determine whether the stack is empty.
```

```
void printStack(StackNodePtr topPtr)
Print the stack.
```

### 12.14 (后缀求值器修改)

修改练习 12.13 的后缀求值器程序，使其能够处理大于 9 的整数操作数。

### 12.15 (超市模拟)

编写一个程序模拟超市收银台。队列是一条队列。顾客以 1 到 4 分钟的随机整数间隔到达。同样，每个顾客的服务时间也是 1 到 4 分钟的随机整数间隔。显然，速率需要平衡。如果平均到达率大于平均服务率，队列将无限增长。即使速率平衡，随机性仍可能导致长时间排队。使用以下算法运行超市模拟 12 小时（720 分钟）：

1) 选择 1 到 4 之间的随机整数以确定第一个顾客到达的分钟。
2) 在第一个顾客到达时间时：
   确定顾客的服务时间（1 到 4 的随机整数）；
   开始为顾客服务；
   安排下一个顾客的到达时间（将当前时间加上 1 到 4 的随机整数）。
3) 对于一天中的每分钟：
   如果下一个顾客到达，
     这样说；
     将顾客入队；
     安排下一个顾客的到达时间。
   如果上一个顾客的服务已完成，
     这样说；
     将下一个要服务的顾客出队；
     确定顾客的服务完成时间（将当前时间加上 1 到 4 的随机整数）。

现在运行你的模拟 720 分钟并回答以下每个问题：

a) 队列中任意时刻顾客的最大数量是多少？
b) 任何一位顾客经历的最长等待时间是多少？
c) 如果到达间隔从 1 到 4 分钟改为 1 到 3 分钟会怎样？

### 12.16 (允许二叉树中存在重复值)

修改图 12.19 的程序以允许二叉树包含重复值。

### 12.17 (字符串二叉搜索树)

编写一个基于图 12.19 程序的程序，输入一行文本，将句子标记化为单独的单词，将单词插入二叉搜索树，并打印树的遍历。

[提示：读取文本行到数组中。使用 strtok 对文本进行标记化。当找到一个标记时，为树创建一个新节点，将 strtok 返回的指针分配给新节点的成员 string，并将节点插入树中。]

### 12.18 (重复消除)

我们已经看到在创建二叉搜索树时重复消除很简单。描述你如何仅使用一维数组执行重复消除。比较基于数组的重复消除与基于二叉搜索树的重复消除的性能。

### 12.19 (二叉树的深度)

编写一个函数 depth，接收一棵二叉树并确定其有多少层。
