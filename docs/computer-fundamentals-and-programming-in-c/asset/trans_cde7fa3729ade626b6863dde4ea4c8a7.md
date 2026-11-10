

## 使用扫描集进行多行输入

可以使用括号字符串读取，`%[ ... ]`，其中方括号 `[]` 用于括起输入中允许的所有字符。如果输入字符串中出现了括号内列出字符之外的任何字符，则进一步读取将终止。反过来，也可以通过方括号指定这些字符，如果输入中出现这些字符，将导致字符串的进一步读取被终止。此类输入终止符必须以脱字符（`^`）开头。例如，如果使用波浪号（`~`）来结束字符串，下面的 `scanf()` 展示了其编码方式。

```c
char string [200];
scanf("%[^~]", string);
```

然后，如果字符串的输入包含嵌入空格，无论如何，这些空格都会被 `scanf()` 全部接受；当输入波浪号（`~`）时，读取将停止。下面的程序及其输出对此进行了说明。

```c
#include <stdio.h>
int main( )
{
    char string [80];

    printf("Enter a string, terminate with a tilde\
          (~)...");
    scanf("%[^~]", string);
    printf("%s", string);
    return 0;
}
```

### 输出

```text
Enter a string, terminate with a tilde (~) ... I am
a string. ~
I am a string. ~
```

虽然终止波浪号本身并不作为所读字符串的元素包含在内，但它会留在“读取缓冲区”——即专用于存储输入的内存区域——并且会被下一次 `scanf()` 调用读取，即使它并不需要。下面的程序及其输出说明了这一点。这里，当下一次 `scanf()` 调用自动执行时，波浪号（`~`）字符被赋给字符变量 `x`。对 `putchar()` 的调用打印出 `x` 的值。

```c
#include <stdio.h>
int main( )
{
    char string [80];
    char x;
    printf("Enter a string, terminate with a tilde\
          (~)...");
    scanf("%[^~]", string);
    scanf("%c", &x);  /* The leftover from the last
                         scanf is read here. This scanf() does not
                         wait for the user to enter another char. */
    printf("%s", string);
    putchar(x);
    return 0;
}
```

### 输出

```text
Enter a string, terminate with a tilde (~) ... I am a
string. ~
I am a string. ~
```

编译并执行该程序。你会发现机器毫不费力地执行了第二个 `scanf()`。此类悬空字符必须通过对 `scanf()` 的后续调用配合 `%c` 或通过 `getchar()` 来“吸收掉”，否则它们可能会以意想不到的方式干扰后续对 `scanf()` 或 `getchar()` 的调用。

## 使用带转换说明符 %c 的 scanf() 进行字符串输入

输入字符串的另一种方法是使用带有 `%c` 转换的 `scanf()`，该转换可以带有计数。此转换不将换行符视为特殊字符。计数指定要读取的字符数。与 `%s` 和 `%[]`（扫描集）转换不同，`%c` 转换不会自动生成字符串终止的 NUL，如果提供的字符数量错误，将会注意到奇怪的效果。下面的程序演示了其用法。

```c
int main()
{
    char str[10];
    int i;
    while(1)
    {
        printf("Enter a string of 9 characters:");
        scanf("%10c",str);
        str[9]='\0';          /* Make it a string */
        printf("String was :%s\n",str);
        if(str[0] == 'z')
            break;
    }
    return 0;
}
```

示例运行的输出如下所示。

- (a) Enter a string of 9 characters: 123456789  
  String was : 123456789
- (b) Enter a string of 9 characters: abcdefghi  
  String was : abcdefghi
- (c) Enter a string of 9 characters: abcdefghijklmnopqr  
  String was : abcdefghi
- (d) Enter a string of 9 characters: 123456789  
  String was : klmnopqr
- (e) Enter a string of 9 characters: ttttttttt  
  String was : 23456789

这里还需要注意其他几点。首先是，与提示相反，实际转换了 10 个字符。这样做是为了让输入行末尾的换行符也被读入；否则它会留在输入缓冲区中，在下一次被当作输入字符之一读取。提供过多输入字符的效果是，'未消费'的输入字符（包括换行符）会留在输入缓冲区中。这些字符将被下一次 `scanf()` 调用'消费'。如果提供的输入字符过少，`scanf()` 会挂起（或阻塞），直到获得足够的输入字符。以上示例中可以看到这两种行为。

使用 `scanf()` 函数的复杂性表明，它并不真正适合可靠、通用的字符串输入。

### 使用 gets()

字符串输入的最佳方法是使用名为 `gets()` 的库函数。该函数将适合保存输入的内存区域的起始地址作为单个参数。完整的输入行被读入并作为以 null 结尾的字符串存储在该内存区域中。其用法如下面的程序所示。

```c
int main()
{
 char str[150];
 printf("Enter a string");
 gets(str);
 printf("The string was :%s\n",str);
 return 0;
}
```

**示例运行：**

- (a) Enter a string manas  
  The string was :manas
- (b) Enter a string manas ghosh  
  The string was :manas ghosh

gets() 可以使用 getchar() 或带 %c 转换说明符的 scanf() 来实现，如下所示：

```c
#include <stdio.h>
int main()
{
 char s[80], ch;
 int i;
 printf("\n Enter the text:");
 for(i=0; i<80 ;i++)
 {
   ch=getchar();
   if(ch=='\n')
     break;
   s[i]=ch;
 }
 s[i]='\0';
 printf("\n Entered text is:");
 puts(s);
 return 0;
}
```

注意不要输入超过所用字符串变量所能存储的字符数，因为 C 语言不检查数组边界。gets() 和 puts() 函数可以嵌套使用。可以在 C 语言中编写以下语句。

```c
printf("%s", gets(s));
puts(gets(s));
```

### sscanf()

有多种处理输入数据的库函数。最有用的包括 sscanf() 和 atoi() 函数。sscanf() 函数将 scanf() 类型的转换应用于保存在程序缓冲区中作为单个字符串的数据，而不是从标准输入读取数据。atoi() 函数将字符串从外部十进制形式转换为内部二进制形式。

sscanf() 与 gets() 结合使用的用法通过以下程序说明。该程序的目的是读取一个整数。与 scanf() 的简单用法不同，输入错误会被检测到，并重复提示直到输入有效的整数。

```c
#include <stdio.h>
int main()
{
 int error;
 char inbuf[256];
 int i;
 char c;
 while(1)
 {
   error = i = 0;
   printf("Enter an integer");
   gets(inbuf);           /* get complete input line */
   while(inbuf[i] == ' ')  /* skip spaces */
     i++;
   if(inbuf[i] == '-' || inbuf[i] == '+')
     i++;
   while((c = inbuf[i++])!='\0')
                       /* while string end with NUL */
   {
     if(c>'9' || c<'0')    /* non-digit ? */
     {
       printf("Non-Numeric Character %c\n",c);
       error = 1;
       break;
     }
   }
   if(!error)            /* was everything OK ? */
   {
```

```c
{
    int i;
    printf("Input an integer:");
    /* read an integer from the standard input stream */
    if(fscanf(stdin,"%d", &i))
        printf("The integer read was: %i\n", i);
    else
    {
        fprintf(stderr,"Error in reading from stdin.\n");
        exit(1);
    }
    return 0;
}
```

**注意**

- 一种特殊情况是，当显式指定数组大小且初始化器的数量完全填满该数组大小时，null 字符不会自动附加到数组。
- 在 `%s` 转换说明符中使用宽度和精度修饰符的 printf() 可用于显示字符串。
- 在 scanf() 中，`%s` 格式在字符串名称前不需要与号。
- 如果提供的输入字符较少，scanf() 会挂起，直到获得足够的输入字符。
- scanf() 仅将空白字符分隔的字符序列识别为外部字符串。
- 使用 scanf() 时，悬空字符必须通过后续使用 %c 的 scanf() 调用或 getchar() 来吸收。

## 11.3.5 字符串中的字符操作

在处理字符串时，需要记住的一个重要点是，它必须以 NUL（'\0'）结尾。下面的程序移除了字符串中的所有空格。

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char a[80],t[80];
    int i,j;
    printf("\n enter the text\n");
    gets(a);
    for(i=0,j=0; a[i]!='\0';++i)
        if(a[i]!=' ')
            t[j++]=a[i];
    t[j]='\0';
    printf("\n the text without blank spaces\n");
    puts(t);
    return 0;
}
```

表 11.2 列出了头文件中的字符处理函数。注意，除了 toupper() 和 tolower() 函数外，所有这些函数都返回表示真或假的值。可以回想一下，在 C 语言中，真是非零数，假是零。在这些函数中，字符似乎是作为整数输入的。这是因为字符函数实际上是在查看字符的 ASCII 值，而 ASCII 值是整数。

### 表 11.2 <ctype.h> 中的字符函数，其中 c 是字符参数

| 函数 | 描述 |
|---|---|
| isalnum(c) | 如果 c 是字母数字则返回非零值 |
| isalpha(c) | 如果 c 是字母则返回非零值 |
| iscntrl(c) | 如果 c 是控制字符则返回非零值 |
| isdigit(c) | 如果 c 是数字 0-9 则返回非零值 |
| isgraph(c) | 如果 c 是非空白的可打印字符则返回非零值 |
| islower(c) | 如果 c 是小写字母字符，即 a-z，则返回非零值 |
| isprint(c) | 如果 c 是可打印字符，包括非空白和空白，则返回非零值 |
| ispunct(c) | 如果 c 是可打印字符但不是字母、数字或空白，则返回非零值 |
| isspace(c) | 对空白及以下转义序列返回非零值：'\f'、'\n'、'\r'、'\t' 和 '\v' |
| isupper(c) | 如果 c 是大写字母，即 A-Z，则返回非零值 |
| isxdigit(c) | 如果 c 是十六进制字符，0-9、a-f 或 A-F，则返回非零值 |
| tolower(c) | 如果 c 是大写字母则返回小写版本；否则返回 c |
| toupper(c) | 如果 c 是小写字符则返回大写版本；否则返回 c |

要查看其中一些字符操作函数的实际效果，请在计算机上编写并运行以下程序。该程序统计字符串中的单词数量。

```c
#include <stdio.h>
#include <ctype.h>
int main()
{
    char s[30];
    int i=0,count=0;
    printf("\n enter the string\n");
    scanf("%[^\n]",s);
    while(s[i]!='\0')
    {
        while(isspace(s[i]))
```

