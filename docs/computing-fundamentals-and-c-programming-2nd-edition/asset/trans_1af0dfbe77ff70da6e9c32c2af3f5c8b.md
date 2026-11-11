

## 10.6 字符串的连接

LO 10.4

正如我们不能直接将一个字符串赋值给另一个字符串一样，我们也不能通过简单的算术加法将两个字符串连接在一起。也就是说，如下语句：

```
string3 = string1 + string2;
string2 = string1 + "hello";
```

是无效的。来自 **string1** 和 **string2** 的字符应该一个接一个地复制到 **string3** 中。数组 **string3** 的大小应足够大，以容纳所有字符。

将两个字符串组合在一起的过程称为*连接*。程序 10.9 演示了三个字符串的连接。

### 习题 10.8

某组织员工的姓名存储在三个数组中，分别称为 **first_name**、**second_name** 和 **last_name**。编写一个程序，将这三部分连接成一个名为 **name** 的字符串。

程序如图 10.9 所示。使用了三个 *for* 循环来复制这三个字符串。在第一个循环中，**first_name** 中包含的字符被复制到变量 **name** 中，直到遇到*空字符*。*空字符*不会被复制；相反，它被赋值语句：

```
name[i] = ' ' ;
```

替换为一个*空格*。

类似地，**second_name** 从上述语句产生的空格之后的列开始复制到 **name** 中。这是通过赋值语句：

```
name[i+j+1] = second_name[j];
```

实现的。

如果 **first_name** 包含 4 个字符，那么此时 *i* 的值将为 4，因此 **second_name** 的第一个字符将被放置在 **name** 的*第五个单元*中。注意，我们在*第四个单元*中存储了一个空格。

同样，语句：

```
name[i+j+k+2] = last_name[k];
```

用于将 **last_name** 中的字符复制到 **name** 的适当位置。

最后，我们放置一个空字符来结束连接后的字符串 **name**。在本例中，注意 **i+j+1** 和 **i+j+k+2** 这两个表达式的使用非常重要。

```
程序

main()
{
    int i, j, k ;
    char first_name[10] = {"VISWANATH"} ;
    char second_name[10] = {"PRATAP"} ;
    char last_name[10] = {"SINGH"} ;
    char name[30] ;
    /* 将 first name 复制到 name */
    for( i = 0 ; first_name[i] != '\0' ; i++ )
        name[i] = first_name[i] ;
    /* 用空格结束 first_name */
    name[i] = ' ' ;
    /* 将 second_name 复制到 name */
    for( j = 0 ; second_name[j] != '\0' ; j++ )
        name[i+j+1] = second_name[j] ;
    /* 用空格结束 second_name */
    name[i+j+1] = ' ' ;
    /* 将 last_name 复制到 name */
    for( k = 0 ; last_name[k] != '\0'; k++ )
        name[i+j+k+2] = last_name[k] ;
    /* 用空字符结束 name */
    name[i+j+k+2] = '\0' ;
    printf("\n\n") ;
    printf("%s\n", name) ;
}
```

输出

VISWANATH PRATAP SINGH

图 10.9 *字符串的连接*

## 10.7 两个字符串的比较

同样，C 语言不允许直接比较两个字符串。也就是说，如下语句：

```
if(name1 == name2)
if(name == "ABC")
```

是不允许的。因此，有必要逐字符比较待测试的两个字符串。比较一直进行到出现不匹配，或者其中一个字符串遇到空字符结束为止，以先发生者为准。下面的程序片段说明了这一点。

```
i=0;
while(str1[i] == str2[i] && str1[i] != '\0'
      && str2[i] != '\0')
    i = i+1;
if (str1[i] == '\0' && str2[i] == '\0')
    printf("strings are equal\n");
else
    printf("strings are not equal\n");
```

## 10.8 字符串处理函数

幸运的是，C 库支持大量的字符串处理函数，可用于执行到目前为止讨论的许多字符串操作。以下是最常用的字符串处理函数：

| 函数 | 作用 |
| --- | --- |
| strcat() | 连接两个字符串 |
| strcmp() | 比较两个字符串 |
| strcpy() | 将一个字符串复制到另一个字符串 |
| strlen() | 求字符串的长度 |

我们将简要讨论这些函数中的每一个如何用于字符串处理。

### strcat() 函数

**strcat** 函数将两个字符串连接在一起。其形式如下：

```
strcat(string1, string2);
```

**string1** 和 **string2** 是字符数组。当执行 **strcat** 函数时，**string2** 被追加到 **string1** 之后。它通过移除 **string1** 末尾的空字符并从该处放置 **string2** 来实现这一点。**string2** 中的字符串保持不变。例如，考虑以下三个字符串：

![](img/11b034a94fc590add0a7808250a38792_368_0.png)

执行语句：

```
strcat(part1, part2);
```

将得到：

![](img/11b034a94fc590add0a7808250a38792_368_1.png)

而语句：

![](img/11b034a94fc590add0a7808250a38792_368_2.png)

将得到：

![](img/11b034a94fc590add0a7808250a38792_368_2.png)

我们必须确保 string1（即被追加 string2 的字符串）的大小足够大，能够容纳最终得到的字符串。

strcat 函数也可以将字符串常量追加到字符串变量。以下用法是有效的：

```
strcat(part1, "6000");
```

C 语言允许 strcat 函数嵌套使用。例如，语句：

```
strcat(strcat(string1,string2), string3);
```

是允许的，它将三个字符串连接在一起。结果字符串存储在 string1 中。

### strcmp() 函数

strcmp 函数比较由参数指定的两个字符串，如果它们相等，则值为 0。如果不等，则值为字符串中第一个不匹配字符之间的数值差。其形式为：

```
strcmp(string1, string2);
```

string1 和 string2 可以是字符串变量或字符串常量。例如：

```
strcmp(name1, name2);
strcmp(name1, "John");
strcmp("Ram", "Ram");
```

我们主要关心的是确定字符串是否相等；如果不相等，哪一个在字母顺序上更靠前。不匹配的值通常并不重要。例如，语句：

```
strcmp("their", "there");
```

将返回 -9，这是 ASCII 码中 "i" 和 "r" 的数值差。也就是说，在 ASCII 码中 "i" 减去 "r" 等于 -9。如果值为负，则 string1 在字母顺序上位于 string2 之前。

### strcpy() 函数

strcpy 函数的功能几乎类似于字符串赋值运算符。其形式如下：

```
strcpy(string1, string2);
```

它将 string2 的内容赋给 string1。string2 可以是字符数组变量或字符串常量。例如，语句：

```
strcpy(city, "DELHI");
```

将字符串 "DELHI" 赋给字符串变量 city。类似地，语句：

```
strcpy(city1, city2);
```

将字符串变量 city2 的内容赋给字符串变量 city1。数组 city1 的大小应足够大，以容纳 city2 的内容。

### strlen() 函数

该函数统计并返回字符串中字符的个数。其形式为：

```
n = strlen(string);
```

其中 n 是一个整型变量，它接收字符串长度的值。参数可以是字符串常量。计数在第一个空字符处结束。

### 习题 10.9

s1、s2 和 s3 是三个字符串变量。编写一个程序，将两个字符串常量读入 s1 和 s2，并比较它们是否相等。如果不相等，则将它们连接起来。然后将 s1 的内容复制到变量 s3 中。最后，程序应打印所有三个变量的内容及其长度。

程序如图 10.10 所示。在第一次运行中，输入的字符串是 "New" 和 "York"。这些字符串通过语句：

```
x = strcmp(s1, s2);
```

进行比较。由于它们不相等，因此使用语句：

```
strcpy(s3, s1);
```

将它们连接起来并复制到 s3 中。

程序输出所有三个字符串及其长度。

在第二次运行中，两个字符串 s1 和 s2 相等，因此它们不会被连接。在这种情况下，三个字符串都包含相同的字符串常量 "London"。

程序

```
#include <string.h>

main()
{ char s1[20], s2[20], s3[20];
  int x, l1, l2, l3;
  printf("\n\nEnter two string constants \n");
  printf("?");
  scanf("%s %s", s1, s2);
  /* 比较 s1 和 s2 */
  x = strcmp(s1, s2);
  if(x != 0)
  { printf("\n\nStrings are not equal \n");
    strcat(s1, s2); /* 连接 s1 和 s2 */
  }
  else
    printf("\n\nStrings are equal \n");
  /* 将 s1 复制到 s3 */
  strcpy(s3, s1);
  /* 求字符串长度 */
  l1 = strlen(s1);
  l2 = strlen(s2);
  l3 = strlen(s3);
  /* 输出 */
  printf("\ns1 = %s\t length = %d characters\n", s1, l1);
  printf("s2 = %s\t length = %d characters\n", s2, l2);
  printf("s3 = %s\t length = %d characters\n", s3, l3);
}
```

输出

Enter two string constants

