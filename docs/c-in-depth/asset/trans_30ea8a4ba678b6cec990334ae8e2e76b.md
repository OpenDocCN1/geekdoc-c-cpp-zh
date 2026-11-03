

## 第 9 章
字符串

C 语言中没有单独的字符串数据类型。字符串被当作 char 类型的数组处理。如果字符数组以空字符（'\0'）结尾，那么它就是一个字符串。这个空字符是 ASCII 值为 0 的转义序列。字符串通常用于存储和操作文本形式的数据，例如单词或句子。

字符串常量是用双引号括起来的一系列字符。它有时被称为字面量。双引号不是字符串的一部分。字符串常量的一些示例如下——

- "Taj Mahal"
- "2345"
- "Subhash Chandra Bose was a great leader"
- ""（空字符串，仅包含 '\0'）
- "My age is %d and height is %f\n"（printf 中使用的控制字符串）

每当字符串常量在程序中的任何位置被写出时，它都会作为以空字符（'\0'）结尾的字符数组存储在内存中的某个位置。字符串常量本身成为指向该数组中第一个字符的指针。例如，字符串 "Taj Mahal" 在内存中将存储为——

| 1000 | 1001 | 1002 | 1003 | 1004 | 1005 | 1006 | 1007 | 1008 | 1009 |
|------|------|------|------|------|------|------|------|------|------|
| T    | a    | j    |   | M    | a    | h    | a    | l    | \0   |

每个字符占用一个字节，编译器会自动在末尾插入空字符。字符串常量 "Taj Mahal" 实际上是指向字符 'T' 的指针。因此，每当程序中使用字符串常量时，它都会被替换为指向该字符串的指针。

如果我们有一个 char * 类型的指针变量，那么我们可以将这个字符串常量的地址赋给它，如下所示——
char *p = "Taj mahal";

```
char *p = "Taj mahal";
```

类似地，当我们写：
printf("Subhash Chandra Bose\n");
时，实际上传递给 printf() 函数的是一个指向字符的指针（char *）。

如果程序中使用了相同的字符串常量，它们将被分别存储在不同的内存位置。

```
#include<stdio.h>
main()
{
	printf("\n\n","good");
	printf("\n\n","good");
	if("bad" == "bad")
		printf("Same\n\n");
	else
		printf("Not same\n\n");
}
```

输出
174
183
Not same

从上面的输出可以看出，两个字符串 "good" 是相同的，但它们存储在不同的位置。当我们使用相等运算符比较两个相同的字符串时，实际上比较的是地址，而不是字符串。（稍后我们将学习用于比较字符串的库函数 strcmp()。）

你能猜出表达式 "software"[4] 表示什么吗？根据指针与下标记法的等价性，这个表达式等价于 *("software"+4)。我们知道 "software" 表示第一个字符（即 's'）的地址。在这个地址上加 4，就得到字符 'w' 的地址，再对其解引用，就得到字符 "w"。

在某些编译器中，我们还可以通过将字符串常量的地址存储在指针中来修改字符串常量，但这样做并不是好做法，而且此类程序的行为是未定义的。因此，我们绝不应尝试修改字符串常量。

我们已经学过，字符串常量给出其第一个字符的地址，但这条规则有一个例外；当字符串常量用作字符数组的初始化器时，它不表示任何地址，也不会存储在内存中的任何位置。例如——
```
char arr[5] = "Deep";
```
这里，字符串常量 "Deep" 不存储在内存中，因此不表示任何地址。

注意，'b' 和 "b" 是不同的。'b' 是字符常量，表示字符 'b' 的 ASCII 值；而 "b" 是字符串常量，由字符 'b' 和空字符 '\0' 组成。

在字符串常量内部，反斜杠被视为转义字符，因此如果需要在字符串常量中包含反斜杠字符，则它前面应再加一个反斜杠。

例如，考虑下面两个 printf 语句——
printf("good\nbad");
printf("I love \"C\" programming");

这两个语句的输出将是——

Character = a   Address = 1004

| arr[0] | arr[1] | arr[2] | arr[3] | arr[4] | arr[5] |
|---|---|---|---|---|---|
| I | n | d | i | a | \0 |
| 1000 | 1001 | 1002 | 1003 | 1004 | 1005 |

```
/*P9.3 Program to print the address and characters of the string using pointer*/
#include<stdio.h>
main()
{
    char str[] ="India";
    char *p;
    p=str;
    while(*p!='\0')
    {
        printf("Character = %c\t",*p);
        printf("Address=%u\n",p);
        p++;
    }
}
```

该程序的输出与上一个程序相同。

这里，'p' 是一个指针变量，保存数组 str[] 的基地址。将该指针加 1 会得到字符数组 str[] 下一个元素的地址，因此通过递增并解引用该指针，我们可以打印字符串的所有元素。这个过程与其他数组中所用的过程类似，不同之处在于这里的循环在遇到字符 '\0' 时终止，该字符表示字符串的结束。

有一种输入和打印字符串的快捷方式，即在 printf() 和 scanf() 的控制字符串中使用 %s 格式说明。

```
/*P9.4 Program to input and output a string variable using scanf()*/
#include<stdio.h>
main()
{
    char name[20];
    printf("Enter name :");
    scanf("%s",name);
    printf(" %s ",name);
    printf(" %s\n","Srivastava");
}
```

### 第 1 次运行：
Enter a name: Deepali
Deepali Srivastava

### 第 2 次运行：
Enter a name : Suresh Kumar
Suresh Srivastava

printf() 接受字符串的基地址，并继续显示字符，直到遇到字符 '\0'。

当我们使用 %s 输入字符串时，空字符会自动存储在数组末尾。我们在 scanf() 中没有使用 & 符号，因为数组名本身就是数组的地址。在第 2 次运行中，当我们输入带空格的字符串时，无法得到所需结果。这是因为 scanf() 一遇到空白字符就停止读取。因此，要输入带空白的字符串，我们可以使用函数 gets()。它只在遇到换行符时停止读取，并将该换行符替换为空字符。我们还有另一个函数 puts()，它可以输出字符串，并将空字符替换为换行符。

```
/*P9.5 Program to understand the use of gets() and puts()*/
#include<stdio.h>
main()
{
    char name[20];
    printf("Enter name : ");
    gets(name);
    printf("Entered name is : ");
    puts(name);
}
```

```
Output:
    Enter name : Suresh Kumar
    Entered name is : Suresh Kumar
```

## 9.3 字符串库函数

有几个用于操作字符串的库函数。这些函数的原型位于头文件 string.h 中。下面我们将讨论其中一些——

### 9.3.1 strlen( )
此函数返回字符串的长度，即字符串中不包括终止空字符的字符数。它接受一个参数，该参数是指向字符串第一个字符的指针。例如，strlen("suresh") 返回值为 6。类似地，如果 s1 是一个包含名字 "deepali" 的数组，那么 strlen(s1) 返回值为 7。

```
/*P9.6 Program to understand the work of strlen() function*/
#include<stdio.h>
#include<string.h>
main()
{
    char str[20];
    int length;
    printf("Enter the string:\n");
    scanf("%s",str);
    length=strlen(str);
    printf("Length of the string is : %d\n",length);
}
```

输出：
Enter the string : CinDepth
Length of the string is : 8

### 此函数的创建
数组版本——
```
int astrlen(char str[])
{
    int i=0;
    while(str[i]!='\0')
        i++;
    return i;
}
```

指针版本——
```
int pstrlen(char *str)
{
    char *start=str;
    while(*str!='\0')
        str++;
    return (str-start);
}
```

我们也可以将 while 条件写成——
```
while(*str)
```
因为 '\0' 的 ASCII 值为 0，而在 C 中 0 被视为假。

### 9.3.2 strcmp()
此函数用于比较两个字符串。如果两个字符串匹配，strcmp() 返回值 0，否则返回非零值。此函数逐字符比较字符串。当到达字符串末尾，或两个字符串中的对应字符不相同时，比较停止。不匹配时返回的非零值是两个字符串中不匹配字符的 ASCII 值之差——
- 当 s1 < s2 时 < 0
- 当 s1 == s2 时 = 0
- 当 s1 > s2 时 > 0

通常，我们不使用不匹配时返回的确切非零值。我们只需要知道它的符号，以比较两个字符串的字母顺序位置。我们可以使用此函数按字母顺序对字符串排序。

```
/*P9.7 Program to understand the work of strcmp() function*/
#include<stdio.h>
#include<string.h>
main()
{

