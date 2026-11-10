
字符串以 `\0` 字符终止。C 语言允许另一种表示法

```c
char msg[] = "Hello";
```

这种写法在实践中经常使用。编写字符串常量的规则与本书前面在介绍 `printf()` 用法时所讨论的规则完全相同。应当注意，聚合体 'msg' 的大小为六个字节：五个字节用于字母，一个字节用于终止 NUL。

有一种特殊情况，空字符不会自动追加到数组末尾。这种情况是：显式指定了数组大小，并且初始化项的数量恰好填满数组大小。例如，

```c
char c[4] = "abcd";
```

这里，数组 `c` 只保存指定的四个字符 a、b、c 和 d。没有空字符终止该数组。

### 注意

- 由字符组成的数组在 C 中就是字符串。
- 字符串的结尾用空字符标记。
- 当显式指定字符数组大小，并且初始化项的数量恰好填满数组大小时，空字符不会自动追加到数组末尾。

## 11.3.3 打印字符串

转换类型 's' 可用于通过 `printf()` 输出字符串。宽度和精度说明可与 `%s` 转换说明符一起使用。宽度指定最小输出字段宽度；如果字符串较短，则会生成空格填充。精度指定要显示的最大字符数。如果字符串太长，则会被截断。负宽度意味着短字符串左对齐，而不是默认的右对齐。例如，

```c
printf("%7.3s", name)
```

这指定只打印前三个字符，总字段宽度为七个字符，并且默认在分配的宽度内右对齐。我们可以包含减号使其左对齐（`%-7.3s`）。应注意以下几点。

- 当字段宽度小于字符串长度时，会打印整个字符串。
- 小数点右侧的整数值指定要打印的字符数。
- 当要打印的字符数指定为零时，不打印任何内容。
- 说明中的减号使字符串按左对齐方式打印。

以下程序演示了 `%s` 转换说明符的用法。

```c
#include <stdio.h>
int main()
{
    char s[]="Hello, World";
    printf(">>%s<<\n",s);
    printf(">>%20s<<\n",s);
    printf(">>%-20s<<\n",s);
    printf(">>%-4.4s<<\n",s);
    printf(">>%-20.4s<<\n",s);
    printf(">>%20.4s<<\n",s);
    return 0;
}
```

该程序产生如下输出

```text
>>Hello, World<<
>>        Hello, World<<
>>Hello, World        <<
>>Hell<<
>>Hell                <<
>>        Hell<<
```

程序中包含 `>>` 和 `<<` 符号，以便在输出中清楚看到输出字段的边界。

还有另一种打印字符串的方法。库函数 `puts()` 将一行输出写入标准输出。它用换行符 `\n` 终止该行。如果发生错误，则返回 EOF。成功时返回正数。`puts()` 的用法如下：

```c
#include <stdio.h>
int main()
{
    char s[]="Hello, World";
    puts(s);
    return 0;
}
```

库函数 `sprintf()` 与 `printf()` 类似。唯一的区别是格式化输出被写入内存区域，而不是直接写入标准输出。当需要在内存中构造格式化字符串以便随后通过通信通道传输或发送到特殊设备时，它特别有用。它与 `printf()` 的关系类似于 `sscanf()` 与 `scanf()` 的关系。库函数 `puts()` 可用于将字符串复制到标准输出，其唯一参数是字符串的起始地址。`puts()` 在写完字符串后向标准输出写入一个换行字符。

以下是使用 `sprintf()` 和 `puts()` 的简单示例。

```c
#include <stdio.h>
int main()
{
    char buf[128];
    double x = 1.23456;
    int i = 0;
    sprintf(buf,"x = %7.5lf",x);
    while(i<10)
        puts(buf+i++);
    return 0;
}
```

产生的输出如下：

```text
x = 1.23456
 = 1.23456
= 1.23456
 1.23456
1.23456
.23456
23456
3456
456
56
```

如果 '\n' 被包含在 sprintf() 的格式字符串中，输出将会变成双倍行距，因为该函数会在生成的字符串中放入换行字符，而 puts() 随后还会再生成一个换行。

## 11.3.4 字符串输入

以下各节将描述从用户处获取输入的方法。

### 使用 %s 控制字符串配合 scanf()

可以使用 scanf() 函数的 %s 转换来读取字符串，但有一些限制。首先，scanf() 只把由空白字符分隔的字符序列识别为外部字符串。其次，程序员有责任确保有足够空间接收并存储传入的字符串，以及由 scanf() 作为 %s 转换的一部分自动生成并存储的终止空字符。值列表中关联的参数必须是为存储传入字符串而预留的内存区域中第一个位置的地址。

当然，可以指定字段宽度，这是读取的最大字符数，但请记住，任何多余字符都会留在输入缓冲区中未被消耗。以下程序说明了 scanf() 与 %s 转换的简单用法。

```c
int main()
{
    char str[50];
    printf("Enter a string");
    scanf("%s",str);
    printf("The string was :%s\n",str);
    return 0;
}
```

示例运行的输出：

```text
(a) Enter a string   manas
    The string was  :manas
(b) Enter a string   manas ghost
    The string was  :manas
(c) Enter a string   "manas and ghost"
    The string was  : "manas"
```

与整数、浮点数和字符不同，%s 格式不需要在变量 str 前加 & 符号。

还可以观察到，尝试用引号括起包含内部空格的字符串，或对内部空格进行转义（这两种做法在 UNIX 命令环境中通常有效），都没有奏效。C 支持可变字段宽度或精度，例如，

```c
printf("%*.*s",w,d,str);
```

在宽度为 w 的字段中打印字符串的前 d 个字符。例如，

```c
int main()
{
    char str[50];
    printf("\n Enter a string:");
    scanf("%s",str);
    printf("\n %*.*s\n",2,3,str);
    return 0;
}
```

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_276_0.png)

示例运行：

```text
Enter a string:Manas
Man
```

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_276_1.png)

作为示例，以下程序将十进制数转换为其十六进制等价值。

```c
#include <stdio.h>
int main(void)
{
    int n, r, i, a[50];
    char hexdigit[]="0123456789ABCDEF";
    printf("\n Enter the decimal number: ....\t");
    scanf("%d", &n);
    i=0;
    while(n>0)
    {
        r=n%16;
        a[i]=r;
        i++;
        n=n/16;
    }
    printf("\n Hexadecimal equivalent is....\t");
    for(--i;i>=0;--i)
        printf("%c", hexdigit[a[i]]);
    return 0;
}
```

这里，在每次迭代中，n 除以 16 的整数除法的余数被存储为数组变量 'a' 的一个元素。这一过程持续到数字 'n' 变为 0。将余数存储为数组 'a' 的元素后，需要按逆序打印这些元素。当控制流离开 while 循环时，'i' 的值会被递增。因此需要将 i 减 1，然后在 for 循环的初始化部分执行这一操作。表达式 hexdigit[a[i]] 会在每次迭代时打印对应的十六进制数字。如果 a[i] 中存储的值为 5，那么 printf("%x", hexdigit[5]) 将打印 5。如果 a[i] 中存储的值为 13，那么 printf("%x", hexdigit[13]) 将打印 D。上述程序的跟踪如下。

```text
n= 28
n=28 i=0 r=12 a[0]=12
n=1 i=1 r=1 a[1]=1
n=0 i=2
```

当控制流位于 while 循环之外时，i 的值为 2。在初始化步骤中，'i' 变为 1。在第一次迭代中，将打印 hexdigit[1]，即 '1'，因为 a[1] 中存储的值为 1。在第二次迭代中，将打印 hexdigit[0]，即 'C'，因为 a[0] 中存储的值为 12。

上述程序可以改写为将余数存储在字符串 hexdigit 中。

```c
#include <stdio.h>
#include <string.h>
int main(void)
{
    int n, r, i;
    char hexdigit[50];
    printf("\n Enter the decimal number: ....\t");
    scanf("%d", &n);
    i=0;
    while(n>0)
    {
        r=n%16;
        if(r<10)
            hexdigit[i]=r+48;
        else
            hexdigit[i]=r%10+65;
        i++;
        n=n/16;
    }
    hexdigit[i]='\0';
    printf("\n Hexadecimal equivalent is....\t");
    for(i=strlen(hexdigit)-1;i>=0;--i)
        printf("%c", hexdigit[i]);
    return 0;
}
```

### 使用扫描集

scanf() 提供的扫描集转换功能是一种有用的字符串输入方法。这种转换功能允许程序员指定作为字符串一部分可接受（或不可接受）的字符集。扫描集转换由方括号内的一列可接受字符组成。可以使用 'a-z' 这样的表示法指定字符范围，表示该范围内的所有字符。在此上下文中，范围的实际解释取决于具体实现，即它取决于宿主计算机上使用的特定字符集。如果扫描集中需要实际的 '-'，它必须是集合中的第一个或最后一个字符。如果 '[' 后的第一个字符是 '^' 字符，则扫描集的其余部分指定的是不可接受字符，而不是可接受字符。

以下程序展示了扫描集的用法。

```c
int main()
{
    char str[50];
    printf("Enter a string in lower case:");
    scanf("%[a-z]",str);
    printf("The string was : %s\n",str);
    return 0;
}
```

下面给出三个示例运行。

- (a) 输入一个小写字符串：hello world  
  该字符串为：hello world

- (b) 输入一个小写字符串：hello, world  
  该字符串为：hello

- (c) 输入一个小写字符串：abcd1234  
  该字符串为：abcd

在第二种情况下，字符 ','（逗号）不在指定范围内。请注意，在所有情况下，转换都会因输入非小写字母的内容而终止。

### 使用带 ^ 的 scanf 进行单行输入

脱字符（`^`）在获取输入时起着重要作用。对于单行文本输入，用户按下 <Return> 或 <Enter> 键来终止字符串。用户可输入的最大字符数可能是 80，因为屏幕一行最多可打印 80 个字符。除 '\n' 外，所有字符都允许作为输入键入。在下面的示例中，计算机把此处的 (\n) 作为字符串已结束的线索。

```c
#include <stdio.h>
int main()
{
    char str[80];
    printf("Enter a string in lower case");
    scanf("%[^\n]",str);
    printf("The string was : %s\n", str);
    return 0;
}
```
