
```c
printf("%15.6s \n", country);
printf("%15.0s \n", country);
printf("%.3s \n", country);
printf("%s \n", country);
printf("____________________ \n");
}
```

**输出**

```text
United Kingdom
United Kingdom   United
United
Uni
United Kingdom
```

**图 9.4** 使用 %s 格式写入字符串

### 示例 9.5

使用 for 循环编写程序打印以下输出。

```text
C
CP
CPr
CPro
....
....
CProgramming

CProgramming
....
....
CPro
CPr
CP
C
```

**程序**

```c
/* ************************************************************ */
/*               PRINTING SEQUENCES OF CHARACTERS               */
/* ************************************************************ */

main()
{
    int c, d;
    static char string[] = "CProgramming";
    printf("\n\n");
    printf("____________________ \n");
    for(c = 0; c <= 11 ; c++)
    {
        d = c + 1;
        printf("%-12.*s\n", d, string);
    }
    printf("|___________|\n");
    for(c = 11 ; c >= 0; c--)
    {
        d = c + 1;
        printf("|%-12.*s|\n", d, string);
    }
    printf("|___________|\n");
}
```

*输出*

![](img/65953ea584e494f3d396b2252cb5ea53_235_0.png)

**图 9.5** 可变字段说明的示意图

图 9.5 中程序的输出，对于可变说明 %12.*s、%.*s 和 %*.*s 显示在图 9.6 中，该图进一步说明了可变字段宽度和精度说明。

![](img/65953ea584e494f3d396b2252cb5ea53_236_0.png)

**图 9.6** 可变说明的进一步示意图

## 9.5 字符上的算术运算

C 允许我们像处理数字一样处理字符。每当字符常量或字符变量在表达式中使用时，系统会自动将其转换为整数值。整数值取决于系统的本地字符集。

要以整数形式表示字符，我们可以将其写成整数。例如，如果机器使用 ASCII 表示，则，

```c
x = 'a';
printf("%d\n", x);
```

将在屏幕上显示数字 97。

也可以对字符常量和变量执行算术运算。例如，

```c
x = 'z' - 1;
```

是一个有效的语句。在 ASCII 中，'z' 的值为 122，因此该语句将把值 121 分配给变量 x。

我们也可以在关系表达式中使用字符常量。例如，表达式

```c
ch >= 'A' && ch <= 'Z'
```

将测试变量 ch 中包含的字符是否为大写字母。

我们可以使用以下关系将字符数字转换为其等效整数值：

```c
x = character - '0';
```

其中 x 被定义为整数变量，character 包含字符数字。例如，假设 character 包含数字 '7'。那么，

x = '7' 的 ASCII 值 - '0' 的 ASCII 值  
= 55 - 48  
= 7

C 库支持一个将数字字符串转换为其整数值的函数。该函数的形式为

```c
x = atoi(string)
```

x 是整数变量，string 是包含数字字符串的字符数组。考虑以下程序段：

```c
number = "1988";
year = atoi(number);
```

number 是一个字符串变量，被赋值为字符串常量 "1988"。函数 atoi 将字符串 "1988"（包含在 number 中）转换为其数值等价物 1988 并将其分配给整数变量 year。

### 示例 9.6

编写一个程序，打印字母集 a 到 z 和 A 到 Z 的十进制和字符形式。

程序显示在图 9.7 中。在 ASCII 字符集中，十进制数字 65 到 90 表示大写字母，97 到 122 表示小写字母。值 91 到 96 使用 for 循环中的 if 语句排除。

**程序**

```c
/* ************************************************************/
/* PRINTING ALPHABET SET IN DECIMAL AND CHARACTER FORM */
/* ************************************************************/
main()
{
 char c;
 printf("\n\n");
 for(c = 65; c <= 122; c = c + 1)
 {
 if(c > 90 && c < 97)
 continue;
 printf("%5d - %c", c, c);
 }
 printf("\n");
}
```

**输出**

```text
65 - A 66 - B 67 - C 68 - D 69 - E 70 - F
71 - G 72 - H 73 - I 74 - J 75 - K 76 - L
77 - M 78 - N 79 - O 80 - P 81 - Q 82 - R
83 - S 84 - T 85 - U 86 - V 87 - W 88 - X
89 - Y 90 - Z 97 - a 98 - b 99 - c 100 - d
101 - e 102 - f 103 - g 104 - h 105 - i 106 - j
107 - k 108 - l 109 - m 110 - n 111 - o 112 - p
113 - q 114 - r 115 - s 116 - t 117 - u 118 - v
119 - w 120 - x 121 - y 122 - z
```

**图 9.7** 以十进制和字符形式打印字母集

## 9.6 合并字符串

正如我们不能直接将一个字符串赋给另一个字符串一样，我们也不能通过简单的算术加法将两个字符串连接起来。也就是说，像这样的语句

```c
string3 = string1 + string2;
string2 = string1 + "hello";
```

是无效的。string1 和 string2 中的字符应一个接一个地复制到 string3 中。数组 string3 的大小应足够大以容纳所有字符。

将两个字符串组合在一起的过程称为连接。示例 9.7 说明了三个字符串的连接。

### 示例 9.7

组织员工的姓名存储在三个数组中，即 first_name、second_name 和 last_name。编写一个程序将这三个部分连接成一个名为 name 的字符串。

程序在图 9.8 中给出。使用三个 for 循环复制三个字符串。在第一个循环中，first_name 中包含的字符被复制到变量 name 中，直到遇到空字符。空字符不被复制，而是被赋值语句 name[i] = ' '; 用空格替换；

同样，second_name 被复制到 name 中，从上述语句创建的空格之后的列开始。这是通过赋值语句 name[i+j+1] = second_name[j]; 实现的；

如果 first_name 包含 4 个字符，则此时 i 的值为 4，因此 second_name 的第一个字符将被放置在 name 的第五个单元中。请注意，我们已在第四个单元中存储了一个空格。

同样，语句 name[i+j+k+2] = last_name[k]; 用于将 last_name 中的字符复制到 name 的正确位置。

最后，我们放置一个空字符来终止连接后的字符串 name。在本例中，需要注意表达式 i+j+1 和 i+j+k+2 的使用。

**程序**

```c
/***************************************************************/
/*                     CONCATENATION OF STRINGS                */
/***************************************************************/
main()
{
    int i, j, k;
    static char first_name[10] = {"VISWANATH"};
    static char second_name[10] = {"PRATAP"};
    static char last_name[10] = {"SINGH"};
    char name[30];

    /* Copy first_name into name */
    for(i = 0; first_name[i] != '\0'; i++)
        name[i] = first_name[i];
    /* End first name with a space */
    name[i] = ' ';
    /* Copy second_name into name */
    for (j = 0; second_name[j] != '\0'; j++)
        name[i + j + 1] = second_name[j];
    /* End second name with a space */
    name[i + j + 1] = ' ';
    /* Copy last_name into name */
    for (k = 0; last_name[k] != '\0'; k++)
        name[i + j + k + 2] = last_name[k];
    /* End name with a null character */
    name[i+j+k+2] = '\0';
    printf("\n\n");
    printf("%s\n", name);
}
```

**输出**

```text
VISWANATH PRATAP SINGH
```

**图 9.8** 字符串的连接

## 9.7 比较两个字符串

再一次，C 不允许直接比较两个字符串。也就是说，像这样的语句

```c
if(name1 == name2)
if(name == "ABC")
```

是不允许的。因此有必要逐字符比较要测试的两个字符串。比较一直进行到出现不匹配或其中一个字符串以空字符终止，以先发生者为准。以下程序段说明了这一点。

```c
i=0;
while(str1[i] == str2[i] && str1[i] != '\0'
      && str2[i] != '\0')
    i = i+1;
if (str1[i] == '\0' && str2[i] == '\0')
    printf("strings are equal\n");
else
    printf("strings are not equal\n");
```
