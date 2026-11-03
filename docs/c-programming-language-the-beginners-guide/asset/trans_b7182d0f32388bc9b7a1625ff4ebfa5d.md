
这里，两个条件都为真。因此，*if* 语句会被执行。在下面的例子中，其中一个条件为假。因此，*if* 语句会被跳过。

```
a = 7;
if( a > 0 && a < 5)
```

```
TRUE && FALSE == FALSE
```

在逻辑或运算符中，只需要其中一个条件为真即可。下面，*if* 语句将被执行。

```
a = 50;
if( a < 10 || a > 25) FALSE || TRUE == TRUE
```

当两个条件都为假时，*if* 语句将不会被执行。a = 50;

```
if( a < 10 || a > 75 )
```

```
FALSE || FALSE == FALSE
```

而对于 NOT 运算符，它会对条件取反。这里，两个条件都为假。a = 50:

```
if( !(a!=50)) TRUE
```

变量 *a* 等于 50。然而，NOT 运算符将其反转，使其为真。最后，在 C 语言中，所有值都被视为真，除了零被视为假。通常情况下，使用值 1 表示真。但它也可以是 -1 或任何非零值。作为构建你自己的字符测试的一个例子，请看下面的代码：

![](img/7d7500a0ed1507e3351945dfe5a0440d_160_0.png)

```
1  #include 2
3  int iscaps(int ch); 4
5  int main()
```

在第 22 行进行了一次逻辑比较。要理解其工作原理，请阅读条件：如果变量 *ch* 的值小于 A，或变量 *ch* 的值大于 Z。当这两个条件中的任何一个为假（即该字符不是大写字母）时，函数返回假。否则，函数返回真。

假设你想将 *iscaps* 函数改为 *isLowerCase*，并让它基于该条件返回真或假。你会怎么做呢？首先，你需要将函数名改为更贴切的名字。

```
#include

int isLowerCase(int ch);

int main()
{
    int c;

do
{
c = getchar();
if(isLowerCase(c))
putchar(c);
}
while (c != '\n');

return(0);
}

int isLowerCase(int ch)
21 {
22 if( ch < 'a' || ch > 'z')
23 return(0);
```

在适当修改函数调用之后，还要将‘A’改为‘a’，将‘Z’改为‘z’。保存、构建并运行代码。从输出中可以看到，只会出现小写字母。通过使用逻辑运算符，你可以创建几乎任何字符测试。在本书后续章节中，你还会看到更多使用逻辑运算符的例子。

## 第9章：字符串处理

字符串是一种有趣的东西。它并不是真正的 C 语言变量，但却被当作变量来使用。在代码中处理字符串时，由于其不寻常的特性，你必须格外小心。本节将讨论如何处理字符串。

我们将向你展示如何获取字符串信息、拼接字符串、比较字符串，以及在一个字符串中查找另一个字符串。这些任务代表了 C 语言中更常用的字符串处理函数。请看下面的代码：

```
#include
#include 3
4 int main()
5 {
char string[] = "Just how long am I?";
int len;
8
len = strlen(string);
printf("The following string:\n");
puts(string);
printf("is %d characters long.\n",len); 13
14 return(0);
15 }
16
17
```

### Strlen

第 6 行声明了一个字符串。它是一个字符数组，因此指定了 *char* 变量类型。变量名后面是空方括号。字符串长度函数 *strlen* 出现在第 9 行。它返回字符串中的字符数，该值存储在 *len* 变量中。构建并运行代码。

这个字符串长度为 19 个字符。你也可以在源代码中数一数字符，但你并不总能知道确切的字符数。例如，如果用户输入一个字符串呢。请看下面的代码：

```
#include
#include

3
4 int main()
5 {

char input[64]; /* 63 characters plus null */
int len;

8

printf("Instructions: ");
fgets(input,64,stdin);
len = strlen(input);
printf("You typed %d characters of instructions.\n",len); 13
14 return(0);
15 }
```

输入通过 *fgets* 函数获取，然后存储到输入缓冲区中。之后，*strlen* 函数获取字符串的长度。下一条语句显示结果。构建并运行代码。

请记住，C 语言中的字符串以空字符结尾。必须为这个额外的字符分配存储空间。程序会生成该字符，但你必须在输入缓冲区中为其预留空间。*strlen* 函数在测量字符串长度时不会计算这个空字符。现在请看下面的代码示例：

```
1 #include 2
3 int main()
4 {
char first[] = "I would like to go ";
char second[] = "from here to there\n"; 7
8 return(0);
9 }
10
```

### Strcat / 字符串拼接

这只是部分代码。我们将研究如何将这两个字符串粘合在一起，形成一个新的字符串。在许多编程语言中，加法运算符就能实现这个功能。例如，某些编程语言可能会这样编写代码，将两个字符串连接起来形成一个新的字符串：

```
#include

int main()
{
    char first[] = "I would like to go ";
    char second[] = "from here to there\n";
    printf("%s\n", first+second);
    return(0);
}
```

然而，在 C 编程语言中，这种做法行不通。你可以将两个字符串连续显示出来，但这不是我们想要的解决方案。你需要做的是将字符串粘合在一起。与其说“把字符串粘在一起”，C 程序员更常说“拼接（concatenate）”，这个词源自拉丁语，意思是把两个字符串粘在一起。

但在那之前，先修正代码。首先，为产生的两个字符串创建一个存储位置，即缓冲区。

```
#include
```

此外，你需要为 strcpy 函数创建原型。所有字符串函数都声明在 string.h 头文件中。

```
#include
#include 3
4 int main()
5 {
char first[] = "I would like to go ";
char second[] = "from here to there\n";
char storage[64]; 9
10 strcpy(storage,first); 11
12 return(0);
13 }
14
```

接下来，你需要将字符串‘second’粘到存储缓冲区的末尾。strcat 语句，也就是字符串拼接语句，会将字符串‘second’附加到存储缓冲区中已有内容的末尾——这就是拼接。最后，显示结果。

```
#include
#include 3
4 int main()
5 {
char first[] = "I would like to go ";
char second[] = "from here to there\n";

char storage[64];

strcpy(storage,first);
strcat(storage,second);

printf("Here is your string:\n%s",storage);

return(0);

14  }
15
```

保存、构建并运行代码。从输出中可以看到，它成功了。

### Strcmp / 字符串比较

另一个常用的字符串函数是比较两个字符串。下面的代码使用 *strcmp*（字符串比较函数）来比较两个字符串：

```
#include
#include 3
4 int main()
5 {
char password[9];
int compare;
8
printf("Enter your password: ");
scanf("%s",password);
compare = strcmp(password,"secret");
if( compare == 0 )
puts("You have been granted access!");
else
puts("Intruder alert!");
return(0);
}
```

当两个字符串相同时，返回值为零。这是零实际上表示“真”的那些奇怪情况之一。小于或大于零的值表示匹配不正确。你还会注意到，*scanf* 函数将输入限制为最多八个字符。输入符合缓冲区的八个字符限制。缓冲区为九个字符，是为了容纳字符串末尾的空字符。构建并运行代码。

现在，在尝试真正的密码 `secret` 之前，先试几个密码。另外，这段代码并不需要 compare 变量。你可以删除它。在代码中删除它（共两处），并直接用函数替换。将 strcmp 函数放到 if 语句中，如下所示：

```
#include
#include
int main()
{
{
{
```

