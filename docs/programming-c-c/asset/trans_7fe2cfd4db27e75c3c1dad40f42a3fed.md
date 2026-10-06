

# 示例 4：字符串与指针：

```c
#include<stdio.h>

int main(void) {
    char name[] = "Harry Potter";

    printf("%c",
```

C 语言支持广泛处理空终止字符串的函数：

```c
void main() {
    char str1[12]="Hello";
    char str2[12]="World";
    char str3[12];
    int len;

    /*拷贝 str1*/ strcpy(str3,str1);
    printf("strcpy(str3,str1): %s\n",str3,str3);

    /*拼接 str1 和 str2*/ strcat(str1,str2);
    printf("strcat(str1,str2): %s\n",str1,str1);
}
```

当上述代码被编译并执行时，会产生以下结果：

```
strcpy(str3,str1): Hello
strcat(str1,str2);
HelloWorld
strlen(str1)
```

# 字符串库函数

有几个用于处理字符串的库函数，这些函数的原型位于头文件 "string.h" 中。一些字符串函数包括：

- * string.h 头文件支持 C 语言中所有的字符串函数。所有的字符串函数列如下。
- 点击下方每个字符串函数的名称查看详细说明和示例程序。

# C 语言标准字符串函数

| | 描述 |
|---|---|
| strcat() | 将 str2 拼接到 str1 的末尾 |
| strcat() | 将字符串的一部分附加到另一个字符串 |
| strcpy() | 将 str2 复制到 str1 |
| strncpy() | 将一个字符串的指定数量字符复制到另一个字符串 |
| strlen() | 得 str1 的长度 |
| strcmp() | 如果 str1 与 str2 相同则返回 0。如果 str1< str2 则返回 <0。如果 str1 > str2 则返回 >0 |
| strcmp() | 与 strcmp() 相同。但此函数会忽略大小写。"A" 和 "a" 被视为相同。 |
| strchr() | 返回字符在 str1 中第一次出现位置的指针 |
| strr() | 找到字符串中指定字符最后出现的位置 |

# 字符串函数

# 函数、数组与字符串

| | |
|---|---|
| strchr( ) | 返回 str2 在 str1 中第一次出现位置的指针 |
| strr( ) | 返回 str2 在 str1 中最后出现位置的指针 |
| strdup( ) | 复制字符串 |
| strlw( | 将字符串转换为小写 |
| strupr( ) | 将字符串转换为大写 |
| strrev( ) | 反转给定的字符串 |
| strset( ) | 将字符串中的所有字符设置为给定字符 |
| strtok( ) | 使用分隔符对给定字符串进行分词 |

部分函数定义如下：

strlen()

此函数返回字符串的长度，即字符串中不包括终止 NULL字符的字符数。

它接受一个参数，即指向字符串第一个字符的指针。

例如：strlen("uresh")

它返回值 6。

数组版本的长度计算方法：

```c
int strlen(char str[])
{
    int i=0;
    while(str[i]='\0')
    {
        i++;
    }
    return i;
}
```

示例：
#include<stdio.h>
#include<string.h>
void main()
{
    char str[50];
    printf("Enter a string:");
    gets(str);
    printf("Length of the string is %d\n",strlen(str));
}
```

**输出：**
nEnter a string: C in Depth
Length of the string is 8

strcmp() 此函数用于比较两个字符串。如果两个字符串匹配，strcmp()
返回值 0，否则它返回一个非零值。它逐字符地比较字符串，当到达字符串末尾或两个字符串中的对应字符不同时，比较停止。

strcmp(s1,s2)
返回值：
<0 当 s1<s2
=0 当 s1=s2
>0 当 s1>s2

在字符串不同时返回的确切值未定义。我们只知道如果 s1<s2，将返回一个负值；如果 s1>s2，则将返回一个正值。

**示例：**

```c
/*字符串比较................*/
#include <stdio.h>
#include <string.h>
void main()
{
char str1[10],str2[10];
printf("Enter two strings: ");

gets(str1);
gets(str2);
if(strcmp(str1,str2)==0)
{
    printf("String are same\n");
}
else
{
    printf("String are not same\n");
}
```

# strcpy()

此函数用于将一个字符串复制到另一个字符串。strcpy(str1,str2) 将 str2 复制到 str1，包括 NULL字符。这里，str2 是源字符串，str1 是目标字符串。

目标字符串 str1 的旧内容将丢失。该函数返回指向目标字符串 str1 的指针。

示例：

```c
#include <stdio.h>
#include <string.h>
void main()
{
    char str1[50], str2[50];
    printf("Enter a string:");
    gets(str2);
    strcpy(str1,str2);
    printf("strcpy(str1,str2): %s\n",str1);
}
```

# strcat()

此函数用于将一个字符串附加到另一个字符串的末尾。strcat(str1,str2) 将 str2 附加到 str1 的末尾，包括 NULL字符。这里，str1 是目标字符串，str2 是源字符串。

**示例：**

```c
#include <stdio.h>
#include <string.h>
void main()
{
    char str1[50], str2[50];
    printf("Enter first string:");
    gets(str1);
    printf("Enter second string:");
    gets(str2);
    strcat(str1,str2);
    printf("strcat(str1,str2): %s\n",str1);
}
```

