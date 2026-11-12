

## 双向选择

- 逻辑表达式的求值结果为真或假。
- 如果结果逻辑值为真，我们有一条路径可走；但如果结果为假，我们将执行第二条路径下的替代（且唯一）语句。
- 在 C 语言编程中，双向选择有两种选择结构可用：if/else 和条件表达式。

### if / else

- if/else 结构（或非常相似的变体）几乎存在于所有编程语言中。其思想是：对逻辑表达式求值，当逻辑表达式为真时执行一组语句，当其为假时执行另一组替代语句。

```
if(logical expression)
{
//TRUE ACTIONS TO EXECUTE
}
else
{
//FALSE ACTIONS TO EXECUTE
}
```

- 如果列出的第一个条件（逻辑表达式）求值为真，则执行 if 主体中的语句，否则执行 else 主体中的语句。

### 双向逻辑图：

### 示例：函数接收一个非负整数，当为偶数时加 1 并返回，当为奇数时减 1 并返回。

```
int changeNumber(int n)
{
    if(n % 2 == 0)
    {
        n++;
    }
    else
    {
        n--;
    }
    return(n);
}
```

### 示例 #2：修改前一个函数，仅在奇数时更改值（减 1）。

| int changeNumber(int n) | int changeNumber(int n) |
|---|---|
| { | { |
| if (n % 2 == 1) | if (n % 2 == 0) |
| { | { |
| n--; | //永远不要让主体为空 |
| } | } |
| else | else |
| { | { |
| ////永远不要让主体为空 | n--; |
| } | } |
| return(n); | return(n); |
| } | } |

### 修改问题的最佳解决方案（else 为可选）：

```
int changeNumber(int n)
{
if (n % 2 == 1)
{
n--;
}
return(n);
}
```

## 嵌套选择

if/else 可以包含任何可执行语句，包括另一个 if/else 结构。当这种情况发生时，我们称之为嵌套选择。通常，嵌套选择涉及对两个或多个不同变量的比较。

### 嵌套选择的逻辑流程：

![](img/50641bd70680c74d7c49fe705f0d8389_86_0.png)

### 嵌套选择的代码示例：

```
int calcStatus(float gpa, int credit_hrs)
{
 int status;
 if(credit_hrs > 120)
 {
 if(gpa >= 3.50)
 {
 status = HONORS;
 }
 else
 {
 status = CANDIDATE;
 }
 }
 else
 {
 status = NONCANDIDATE;
 }
 return(status);
}
```

### 悬空 else 逻辑错误和嵌套 if/else

- 调试注意事项：请注意，本文和许多其他资料并不总是对仅包含单条语句主体的 if/else 语句使用 { }。然而，这可能导致一个称为“悬空 else”的难以调试的逻辑问题。
- 由于此问题可能非常难以调试，我们将要求所有 if/else 语句都使用 { }，即使主体仅包含单条可执行语句。

| Example of dangling else logical error: | Output Generated: |
|---|---|
| `int x = 3;`<br>`int y = 2;`<br>`int z = 0;`<br>`if(x == 3)`<br>`    if(y != 2)`<br>`        z++;`<br>`else`<br>`    z--;`<br>`printf("z = %d\n", z);` | warning: suggest explicit braces to avoid ambiguous 'else' |

对上述代码的逻辑解释：

## 条件表达式

条件表达式有三个操作数和两个运算符。每个操作数本身也是一个表达式。

- 第一个运算符是问号，用于分隔前两个表达式。
- 第二个运算符是冒号，用于分隔最后两个表达式。

求值条件表达式时，首先必须求值最左侧的表达式。当该表达式为真时，则求值第二个表达式（? 后的第一个表达式）的值。然而，如果逻辑表达式（? 之前）为假，则求值第三个表达式。

下面，当两个变量之和大于零时，变量 a 自增。当和小于或等于零时，变量 b 自增。

```
a + b > 0 ? a++ : b++;
```

### 更多条件表达式示例：

| Code | Output Generated: |
|---|---|
| int a = 1;<br>int b = -1;<br>int c;<br><br>a + b > 0 ? a++ : b++;<br><br>c = a > b ? 5 : 3;<br><br>printf("c = %d\n", c);<br><br>a == b ? printf("a == b\n") : printf("a != b\n"); | |

第二个和第三个表达式都必须存在吗？

- 是。
- error: expected expression before ';' token

每个选项（真和假）是否可以包含多个表达式？

- 不可以。

## 多向选择

需要从多个独特代码段中进行选择（超过两个）是一个常见问题。这就是多向选择的概念。

- 在 C 语言中，有两种不同的结构可用于实现多向选择。第一种是使用 if/else if/else，第二种是 switch 结构。switch 结构比 if/else if/else 结构有更多限制，但在某些情况下，使用 switch 可能优于替代方案。

### 多向选择 if/else if/else

- 示例：编写一个程序，接受分数作为输入，并根据分数回复用户他们可以期望获得的字母等级。

```
#define MINA 90
#define MINB 80
#define MINC 70
#define MIND 60

int getScore(void);
char determineGrade(int);
void displayResults(char, int);

int main(void)
{
    int score; //SCORE OF STUDENT
    char grade; //CALCULATED GRADE BASED ON SCORE

    score = getScore();
    grade = determineGrade(score);

    displayResults(grade, score);

    return(0);
}

void displayResults(char grade, int score)
{
    printf("Based on your score of %d, you will receive the grade of %c in this course.\n", score, grade);
}

int getScore(void)
{
    int score; //SCORE TO BE ENTERED BY THE USER

    printf("Enter the score for the course: ");
    scanf("%d", &score);

    return(score);
}

char determineGrade(int score)
{
   char grade;

   if(score >= MINA)
   {
      grade = 'A';
   }
   else if(score >= MINB)
   {
      grade = 'B';
   }
   else if(score >= MINC)
   {
      grade = 'C';
   }
   else if(score >= MIND)
   {
      grade = 'D';
   }
   else
   {
      grade = 'F';
   }

   return(grade);
}
```

第 261 页的图 5-24 是该选择结构的一个良好流程图示例。

> 注意：在此示例中，一旦某个条件为真，该特定条件主体中的语句将被执行，然后退出 if/else if/else 结构。

### 下面的结构中是否有任何一个与上一页的结构在逻辑上等价？

```
if(score >= MINA)
{
    grade = 'A';
}
else if(score >= MINB && score < MINA)
{
    grade = 'B';
}
else if(score >= MINC && score < MINB)
{
    grade = 'C';
}
else if(score >= MIND && score < MINC)
{
    grade = 'D';
}
else
{
    grade = 'F';
}

if(score >= MINA)
{
    grade = 'A';
}
if(score >= MINB && score < MINA)
{
    grade = 'B';
}
if(score >= MINC && score < MINB)
{
    grade = 'C';
}
if(score >= MIND && score < MINC)
{
    grade = 'D';
}
else
{
    grade = 'F';
}
```

### 多向选择 switch

switch 结构用于在可能的整数值替代项中进行选择。当可能的整数值已知且数量较少时，可能会优先使用 switch。

关键字 switch 后面的控制表达式将被求值，然后与一系列 case 进行相等性比较。每个 case 代表控制表达式的一个预期值。

- 每个 case 关联一个或多个可执行语句。
- 应该存在一个或多个可能的 case。当 case 数量较多或表示一系列值时，应考虑使用 if/else if。
- default case 是一个选项，用于覆盖其他单独 case 未表示的所有值。

> 注意：每个 case 都与控制表达式的值进行相等性比较。

```
void displayResults(char grade, int score)
{
    printf("Given score of %d, you will earn a grade of %c in this course.\n", score, grade);
    switch(grade)
    {
        case 'A': printf("Great job!\n");
            break;
        case 'B': printf("Well done!\n");
            break;
        case 'C': printf("Mission Accomplished.\n");
            break;
        case 'D': printf("Perhaps you need to consider repeating?\n");
            break;
        default: printf("See you next semester?\n");
    }
}

