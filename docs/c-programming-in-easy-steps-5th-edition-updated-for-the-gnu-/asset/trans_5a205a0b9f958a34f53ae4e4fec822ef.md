
```
return 0 ;
```

保存程序文件，然后编译并执行该程序，以查看搜索子字符串的结果以及三个字符串值的比较结果。

![](img/db19f3858a1e321646bf2590afd29547_169_0.png)

![](img/db19f3858a1e321646bf2590afd29547_169_1.png)

注意，本例中的 \ 字符用于转义双引号字符——以避免输出字符串过早终止。

![](img/db19f3858a1e321646bf2590afd29547_169_2.png)

string.h 头文件还包含两个字符搜索函数：strchr() 查找字符串中某字符的首次出现，strrchr() 查找最后一次出现——如果未找到该字符，两者都返回 NULL。

## 验证字符串

名为 ctype.h 的标准库头文件包含许多用于对字符执行测试的函数。为了使这些函数可用于程序，必须在程序开头添加 #include 指令来包含 ctype.h 头文件。

在 ctype.h 头文件中，isalpha() 函数测试字符是否为字母，而 isdigit() 测试字符是否为数字。类似地，ispunct() 函数测试字符是否为其他可打印符号，而 isspace() 函数测试一个“字符”是否实际上是一个空格。

此外，ctype.h 头文件提供了 isupper() 和 islower() 函数来测试字符大小写，以及 toupper() 和 tolower() 函数来更改字符大小写。

每个测试函数在测试字符符合预期时返回一个非零值（不一定是 1），但如果不符合预期，则始终返回零。

这些测试函数可用于验证用户输入的字符串，方法是循环遍历字符串中的字符，逐一检查。当某个字符不满足所需条件时，可以设置一个“标志”变量，以告知用户输入无效。

- 1 在一个新程序中添加预处理指令，以包含标准输入/输出和字符串函数

```
#include <stdio.h>
#include <string.h>
```

![](img/db19f3858a1e321646bf2590afd29547_170_0.png)

isval.c

- 2 添加一个 main 函数，声明三个变量，并将一个标志变量初始化为数值真值 (1)

```
int main()
{
```

```
char str[7];
int i;
int flag = 1;
}
```

接下来，在 main 函数中，请求用户输入，然后将该输入作为字符串赋给数组变量。

```
puts("Enter six digits without any spaces...");
gets(str);
```

现在，在 main 函数块中，添加一个循环来检查数组变量中的每个字符。

```
for(i = 0 ; i < 6 ; i++) { }
```

在循环块内，如果任何字符不是数字，则将标志变量改为 false (0)。

```
if( !isdigit( str[i] ) )
{
    flag = 0 ;
}
```

接下来，在 if 块中，描述任何非数字字符。

```
if( isalpha( str[i] ) )
{ printf( "Letter %c Found\n" , toupper(str[i]) ); }
else if( ispunct( str[i] ) )
{ printf( "Punctuation Found\n" ); }
else if( isspace( str[i] ) )
{ printf( "Space Found\n" ); }
```

在循环块之后，输出一条描述标志变量状态的消息。

```
( flag ) ? puts("Entry Valid") : puts("Entry Invalid");
```

在 main 函数块末尾，根据函数声明的要求，返回一个零整数值。

```
return 0 ;
```

保存程序文件，然后编译并执行该程序，以查看输入字符串的验证结果。

![](img/db19f3858a1e321646bf2590afd29547_172_0.png)

![](img/db19f3858a1e321646bf2590afd29547_172_1.png)

**isdigit()** 测试也可以这样表示：**isdigit() == 0.**

![](img/db19f3858a1e321646bf2590afd29547_172_2.png)

完整的字符测试函数列表可在此处的参考部分找到。

## 转换字符串

标准 C 库文件 stdlib.h 中包含一个名为 atoi() 的有用函数，可用于将字符串转换为整数。为了使该函数可用于程序，必须在程序开头添加 #include 指令以包含 stdlib.h 文件。

atoi() 函数，即字母转整数，将要转换的字符串作为其唯一参数。如果字符串为空，或者字符串的第一个字符不是数字或减号，则 atoi() 返回零。否则，字符串（或至少字符串开头的数字部分）将被转换为 int 数据类型，直到 atoi() 遇到字符串中的非数字字符为止。当 atoi() 遇到字符串中的非数字字符时，它会将已转换的数字作为 int 数据类型返回。

还有一个 itoa() 函数，即整数转字母，可用于将 int 数据类型值转换为字符串。该函数使用广泛，但不属于标准 ANSI C 规范。itoa() 函数需要三个参数：要转换的数字；转换后的数字要赋给的字符串；最后是转换所用的基数。例如，指定基数为 2 时，会将指定数字参数的二进制等价形式赋给指定的字符串参数。

符合 ANSI 标准的替代 itoa() 的函数是 stdlib.h 头文件中的 sprintf() 函数。它的功能较弱，因为不能指定基数。sprintf() 函数同样接受三个参数——转换后的数字要赋给的字符串、格式说明符和要转换的数字。该函数返回一个整数，表示转换后字符串中的字符数。

- 1. 在一个新程序中添加预处理指令，以包含标准输入/输出和转换函数

```
#include <stdio.h>
#include <stdlib.h>
```

![](img/db19f3858a1e321646bf2590afd29547_173_0.png)

conv.c

- 2 添加一个 main 函数，声明三个整数变量，然后声明并初始化三个字符数组

```c
int main()
{
    int n1, n2, n3 ;
    char s1[10]="12eight", s2[10]="-65.8", s3[10]="x13" ;
}
```

- 3 现在，在 main 函数块中，尝试将每个字符串转换为整数值并输出结果

```c
n1 = atoi( s1 );
printf( "\nString %s converts to Integer: %d\n", s1 , n1 );

n2 = atoi( s2 );
printf( "String %s converts to Integer: %d\n", s2 , n2 );

n3 = atoi( s3 );
printf( "String %s converts to Integer: %d\n\n", s3 , n3 );
```

- 4 接下来，在函数块中，使用非标准函数将第一个整数变量的值转换为包含其二进制等价形式的字符串，并输出结果

```c
itoa( n1, s1, 2 );
printf( "Decimal %d is Binary: %s\n", n1 , s1 );
```

- 5 然后，使用标准库函数将第一个整数变量的值转换为包含其八进制和十六进制等价形式的字符串，并存储它们的字符长度

```c
n2 = sprintf( s3, "%o", n1 );
printf( "Decimal %d is Octal: %s chars: %d\n", n1, s3, n2 );

n3 = sprintf( s3, "%x", n1 );
printf("Decimal %d is Hexadecimal: %s chars: %d\n",n1,s3,n3);
```

- 6 在 main 函数块末尾，根据函数声明的要求，返回一个零整数值

```c
return 0 ;
```

- 7 保存程序文件，然后编译并执行该程序以查看转换结果

```
C:\MyPrograms>gcc conv.c -o conv.exe
C:\MyPrograms>conv
String 12eight converts to Integer: 12
String -65.8 converts to Integer: -65
String x13 converts to Integer: 0
Decimal 12 is Binary: 1100
Decimal 12 is Octal: 14 chars: 2
Decimal 12 is Hexadecimal: c chars: 1
C:\MyPrograms>_
```

![](img/db19f3858a1e321646bf2590afd29547_175_0.png)

itoa() 函数非常有用，但由于它不是 ANSI 标准的一部分，并非所有编译器都支持它——不过，本书介绍的 GNU C 编译器支持它。

![](img/db19f3858a1e321646bf2590afd29547_175_1.png)

与 itoa() 函数不同，sprintf() 不能转换为二进制，因为没有二进制数的格式说明符。

## 总结

- 在 C 语言编程中，字符串是一个字符数组，其最后一个元素是特殊的 \0 空字符。
- 每个字符还有一个数值型的 ASCII 码值。
- 字符数组名称的作用类似于指向整个字符串的指针。
- scanf() 函数在遇到第一个空格字符时停止读取输入，而 gets() 函数接受空格并自动在末尾添加一个 \0 空字符。
- puts() 函数输出其参数指定的字符串，并自动在字符串末尾添加一个换行符。
- 标准 C 库 string.h 头文件提供了特殊的字符串处理函数，例如 strlen() 函数返回指定字符串的长度，或者 strcpy() 和 strncpy() 函数可以复制字符串。
- string.h 头文件还提供了 strcat() 和 strncat() 函数，可用于拼接字符串。
- 此外，string.h 提供了 strstr() 函数，用于在字符串中搜索指定的子字符串，以及 strcmp() 函数，用于比较两个指定的字符串。
- 当 strstr() 未能找到其要查找的子字符串时，该函数返回 NULL 值。
- 标准 C 库 ctype.h 头文件提供了测试字符类型的函数，例如 isalpha()、isdigit() 和 ispunct()。
- ctype.h 头文件还提供了 islower()、isupper() 以及 tolower()、toupper() 函数，用于测试和设置字符大小写。
- 标准库 stdlib.h 头文件提供了 atoi() 函数，可以将字符串转换为整数。
- 标准库 stdlib.h 头文件提供了 sprintf() 函数，可以将整数转换为字符串，其方式与功能更强大的非标准 itoa() 函数非常相似。

