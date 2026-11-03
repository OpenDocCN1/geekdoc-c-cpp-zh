

```c
14
15 return(0);
16 }
17
```

当基于 if 条件执行多条语句时，实际上需要这种格式。例如，我们将代码的第 9 行下移到第 12 行。保存、构建并运行代码。

```c
1 #include 2
3 int main();
4 {
5 int a;
6

7 printf("Type an integer: ");
8 scanf("%d",&a);
9 if(a > 10)
10) 10) 10)
10) 10) 10) 10) 10)
15 return(0);
16 }
17
```

例如，输入数字 25。现在，由于该数字大于 10，两行内容都会显示出来。看看下面的代码：

```c
1 #include 2

3 int main();
```

```c
4 {
5 int a;
6

7 printf("Type an integer: ");
8 scanf("%d",&a);
9 printf("You typed %d.\n",a);
10 if(a > 10)
11 {
12  printf("%d is greater than 10.\n",a); 13 }
14 if(a < 10)
15 {
16  printf("%d is less than 10.\n",a); 17 }
18

19 return(0);
20 }
```

这段代码连续展示了两个 *if* 比较。每个比较都有自己的花括号组。会评估两个条件：第 10 行的“大于”和第 14 行的“小于”。构建并运行代码。

运行代码后可以看到，对于你输入的、小于或大于 10 的值，都会显示相应的输出。不过请注意，当你输入 10 本身时，看不到相应的输出。

编辑第 14 行，将运算符改为“小于或等于”。编辑第 16 行以体现相同的结果，如下所示：

```c
1 #include <stdio.h>
2

3 int main();
```

```c
4 {
4 { 4 {
4 { 4 { 4 { 4 {
4 {
4 { 4 { 4 {
4 { 4 { 4 {
4 {

4 { 4 { 4 { 4 {
4 {
4 { 4 { 4 {
4 {

4 { 4 { 4 { 4 { 4 { 4 {
4 {
4 {
```

---

保存、构建并运行代码。

## Else 语句

处理二选一决策的另一种方法是使用关键字 *else*。看看下面的代码：

````c
1 #include <stdio.h>
3 int main()
4 {
5 int a;
6

7 printf("Type an integer: ");
8 scanf("%d", &a);
9 printf("You typed %d.\n",a);
10 if(a > 10)
11 {
12  printf("%d is greater than 10.\n",a); 13 }
14 else
15 {
16  printf("%d is less than or equal to 10.\n",a); 17 }
18

19 return(0);
20 }
21

````

这段代码是对前面代码的重写，但它使用了 *else* 关键字。第 10 行的 *if* 条件会进行一次判断。当该条件为真时，其语句会被执行。如果条件为假，则改为执行属于 *else* 的语句。构建并运行这段代码。

注意，else 没有分号。相反，它带有花括号。所有这些语句都可以不写花括号，因为它后面只跟一条语句。

## Else if 语句

当存在三个或更多条件时，可以使用 *else if* 结构来评估它们。看看下面的代码：

```c
#include <stdio.h>
int main()
{
    int a;

    printf("Type an integer: ");
    scanf("%d", &a);
    printf("You typed %d.\n", a);
    if(a > 10)
    {
        printf("%d is greater than 10.\n", a);
    }
    else if(a < 10)
    {
        printf("%d is less than or equal to 10.\n", a);
    }
    else
    {
        printf("%d is 10.\n", a);
    }
    return(0);
}
```

该结构从第 10 行的 *if* 语句开始。当该条件为真时，属于该条件的语句会被执行，其余部分则被跳过。否则，会在第 14 行检查第二个条件。如果该条件为真，则执行其语句，并跳过其余部分。结构的末尾是一个单独的 *else*。当前面的条件都不满足时，会执行它的语句。构建并运行这段代码。

结果与前面的示例类似。只不过这一次，当输入值为 10 时，会执行 *else* 语句下的 *printf* 语句。你可以按需堆叠任意多个 *else if* 语句，这有助于评估复杂情况。

提醒一下：*else* 和 *else* 关键字后面通常不会紧跟分号。在 C 语言中，分号本身就是一个语句。当分号留在 *if* 判断之后时，编译器会认为该分号就是语句，后面不再有任何内容。这是新手程序员常犯的错误。看看下面的代码：

```
1 #include 2
3 int main()
4 {
5 int a = -5;
6

7 if(a > 0);
8 printf("%d is a positive number.\n",a); 9
10 return(0);
```

## Switch/Else 语句

C 语言允许你通过堆叠一系列 *if/else* 条件来处理复杂决策。有时，这种结构会变得有些丑陋。作为替代方案，你可以使用 *switch/case* 结构，这是 C 语言中的另一种决策工具。

在本节中，我们将讨论这种结构。你将看到它是如何构造的、如何应对多个决策，此外我们还会讨论一些技巧。看看下面的代码：

```c
#include <stdio.h>

int main()
{
    char a;

    printf("Your choice (1,2,3): ");
    scanf("%c", &a);

    switch(a)
    {
        case '1':
            puts("Excellent choice!");
            break;
        case '2':
```

```
• puts("This is the most common choice: ");
• break;
• case '3':

• puts("I question your judgement.");
• break;
• default:

• puts("That's not a valid choice."); 23 }
24

25 return(0);
26 }
27

28
```

这段代码的主体是一个结构。它从第 10 行的 *switch* 开始。后面跟着一系列 *case* 语句，每个 *case* 都有自己的语句。最后一部分是 default。它后面也跟有自己的语句，然后是一个右花括号。这些就是该结构的要素。

该结构还使用了 *break* 关键字。总而言之，这个结构包含四个 C 语言关键字：…… 构建并运行上面的代码，看看它的作用。多运行几次，尝试各种选项。该代码接受字符输入，不过它本来也很容易改为接受整数。

它的工作方式如下：Switch 处理的是单个值，而不是比较。它可以是一个数学表达式，但结果必须是单个值。该值由……指定，随后会与每个 *case* 语句的值进行比较。如果比较结果为真，则执行被标记为真的 *case* 语句所属的语句。否则，它们会被跳过。

在第 12 行，如果输入字符 1，则执行第 13 行的 *puts* 语句。第 14 行的 *break* 会结束 switch case 的评估，将控制权返回到 switch 结构最终右花括号之后的那一行，即第 23 行。否则，如果没有匹配项，执行会落到下一个 *case* 语句，然后再下一个，依此类推。

最后，当没有任何 *case* 条件匹配时，会执行 *default* 条件。它不需要 *break* 语句，因为它位于结构的末尾。通过注释掉所有 *break* 语句来修改代码。在第 14、17 和 20 行插入双斜杠。

~~~
1 #include <stdio.h>
3 int main()
4 {
5 char a;
6

7 printf("Your choice (1,2,3): ");
8 scanf("%c", &a);
9

10 switch(a)
11 {
~~~

+   - case '1':
+   - puts("Excellent choice!");

~~~
14// break;
~~~

+   - puts("B – Hotel");
+   - puts("C – Rental Car");

```
11  scanf("%c", &a);
12

13  switch(a)
14  {

- case 'A':
- puts("You have selected the airfare");
- break;
- case 'B':
- puts("You have selected Hotel");
- break;
- case 'C':
- puts("You have selected Rental Car");
- break;
- default:

- puts("That is an invalid choice"); 26 }
27

28  return(0);
29

30  }
31

32
```

下面是另一个结构，它将输入作为菜单系统来评估。构建并运行代码。这些选项的问题在于，你可能输入了小写 ‘a’ 而不是大写 ‘A’。在这种情况下，程序似乎不能正确运行。通过调整 case 语句以同时兼顾大小写输入来解决该问题。

编辑源代码，为小写字母添加重复的 *case* 语句，如下所示：

```c
1 #include 2
3 int main()
4 {
5 char a;
6

• puts("Vacation options: ");
• puts("A — Airfare");
• puts("B — Hotel");
• puts("C — Rental Car");

11 scanf("%c", &a);
12

13 switch(a)
14 {

• case 'A':
• puts("You have selected the airfare");
• break;
```

