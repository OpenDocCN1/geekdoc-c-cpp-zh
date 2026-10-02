
## 作用：`strcpy` 函数

`strcpy` 函数将一个字符串与另一个字符串拼接。它将源字符串附加到另一个字符串之后。

**输入：** 要附加的源字符串以及要附加到的目标字符串。函数 `strcpy` 的第一个参数可以是字符数组或字符指针，但不应该是字符串字面量常量。

**输出：** `strcpy` 将源字符串附加到目标字符串，并返回指向目标字符串的指针。

## 7.10 数组、指针和字符串

用法：程序 7-9 中的代码段说明了 `strcat` 函数的使用以及 `strcat` 功能的实现。

| 行 | Prog 7-9a. 使用库函数 | Prog 7-9b. 使用用户定义函数 | 输出窗口 |
|---|---|---|---|
| 1 | //Concatenating a string with another | //Concatenating a string with another | 字符串为: |
| 2 | #include<stdio.h> | #include<stdio.h> | Hello |
| 3 | #include<string.h> | char* mystrcat(char* dest, const char* src); | Readers!! |
| 4 | main() | main() | 拼接后: |
| 5 | { | { | Hello!! |
| 6 | char dest[50]="Hello"; | char dest[50]="Hello"; | 备注: |
| 7 | char src[50]="Readers"; | char src[50]="Readers"; | • 拼接后的目标字符串长度 |
| 8 | puts("The strings are:"); | puts("The strings are:"); | 等于拼接前字符串的长度 |
| 9 | puts(dest); | puts(dest); | 加上源字符串的长度 |
| 10 | puts(src); | puts(src); | |
| 11 | strcat(dest,src); | mystrcat(dest,src); | • 目标空间足够大 |
| 12 | puts("After concatenation:"); | puts("After concatenation:"); | 即可容纳目标字符串 |
| 13 | puts(dest); | } | 加上源字符串 |
| 14 | } | char* mystrcat(char* dest, const char* src); | 如果空间不足， |
| 15 | | { | 结果字符串的字符将放在 |
| 16 | | int i=0, j=0; | 未预留的内存中 |
| 17 | | while(dest[j]!='\0') | 并可能导致 |
| 18 | | j++; | 内存违规。 |
| 19 | | while(src[i]!='\0') | 因此可能会发生 |
| 20 | | dest[j]=src[i]; | 异常 |
| 21 | | i++;j++; | |
| 22 | | } | |
| 23 | | dest[j]='\0'; | |
| 24 | | return dest; | |
| 25 | | } | |

**程序 7-9** 一个拼接字符串的程序，(a) 使用库函数，(b) 使用用户定义函数。

## 7.5.4 strcmp 函数

**作用：** `strcmp` 函数比较两个字符串。

**输入：** 待比较的字符串 `str1` 和 `str2`，形式可以是字面量、字符数组或指向 `str1` 和 `str2` 存储位置的指针。

**输出：** `strcmp` 函数逐字符比较 `str1` 和 `str2`，从字符串的第一个字符开始，直到字符不同或字符串结束。它返回第一个不同字符的 ASCII 值；如果对应字符相同则返回 0。

## 7.11 字符串和字符数组

用法：程序 7-10 中的代码段说明了 `strcmp` 函数的使用和 `strcmp` 功能的实现。

| 行 | Prog 7-10a.c 使用库函数 | Prog 7-10b.c 使用用户定义函数 | 输出窗口 |
|---|---|---|---|
| 1 | //Comparing two strings | //Comparing two strings | 输入字符串: |
| 2 | #include<stdio.h> | #include<stdio.h> | Hello |
| 3 | #include<string.h> | int mystrcmp(const char *s1, const char *s2); | 输入字符串: |
| 4 | main() | main() | Hi |
| 5 | { | { | 字符串不相等 |
| 6 | char str1[50], str2[50]; | int res; | 输出窗口 (第二次执行) |
| 7 | puts("Enter string:"); | puts("Enter string:"); | 输入字符串: |
| 8 | gets(str1); | gets(str1); | Hello |
| 9 | puts("Enter string 2:"); | puts("Enter string 2:"); | 输入字符串: |
| 10 | gets(str2); | gets(str2); | Hello |
| 11 | res=strcmp(str1,str2); | if(res==0) puts("Strings are equal") | 字符串相等 |
| 12 | if(res==0) | res=strcmp(str1,str2); | 输出窗口 (三次执行) |
| 13 | puts("Strings are equal"); | if(res==0) | 输入字符串: |
| 14 | else | puts("Strings are not equal"); | hello |
| 15 | puts("Strings are not equal"); | else | 输入字符串 2: |
| 16 | } | puts("Strings are not equal"); | HELLO |
| 17 | | int mystrcmp(const char *s1, const char *s2); | 字符串不相等 |
| 18 | | { | 备注: |
| 19 | | int i=0; | - strcmp(str1,str2) 返回一个值: |
| 20 | | while(s1[i]!='\0' && s2[i]!='\0') | - 如果 str1 和 str2 相等， |
| 21 | | if(s1[i]!=s2[i]) | - >0 如果 str1 大于 str2，即在字典序中在 str2 之后， |
| 22 | | return(s1[i]-s2[i]); | - <0 如果 str1 小于 str2，即在字典序中在 str2 之前， |
| 23 | | i++; | |
| 24 | | return 0; | |
| 25 | | } | |

**程序 7-10** 一个比较两个字符串的程序，(a) 使用库函数，(b) 使用用户定义函数。

## 7.5.5 strcmp 函数

**作用：** `strcmp` 函数不区分大小写地比较两个字符串。`strcmp` 中的后缀 'i' 代表忽略大小（ignore case）。

## 7.12 数组、指针和字符串

**输入：** 待比较的两个字符串 `str1` 和 `str2`，形式可以是字面量或指向 `str1` 和 `str2` 存储位置的数组指针。

**输出：** `strcmp` 函数不区分大小写地比较字符串 `str1` 和 `str2`。它返回第一个不同字符的 ASCII 差；如果两个字符串中的对应字符均相同，则返回 0。

**用法：** 程序 7-11 中的代码段说明了 `strcmp` 函数的使用和 `strcmp` 函数的实现。

| 行 | Prog 7-11a.c | Prog 7-11b.c | 输出窗口 |
|---|---|---|---|
| 1 | //Comparing two strings without | //Comparing two strings without | 输入字符串: |
| 2 | // case sensitivity | // case sensitivity | HELLO |
| 3 | #include<stdio.h> | #include<stdio.h> | hello |
| 4 | #include<string.h> | int mystrcmp(const char* s1, const char* s2); | 字符串相等 |
| 5 | main() | main() | |
| 6 | { | { | |
| 7 | char str1[20],str2[20]; | char str1[20],str2[20]; | 输出窗口 (第二次执行) |
| 8 | int res; | int res; | 输入字符串: |
| 9 | puts("Enter string 1:"); | puts("Enter string 1:"); | Hello |
| 10 | gets(str1); | gets(str1); | 输入字符串 2: |
| 11 | puts("Enter string 2:"); | puts("Enter string 2:"); | Hello |
| 12 | gets(str2); | gets(str2); | 字符串相等 |
| 13 | res=strcmp(str1,str2); | res=mystrcmp(str1,str2); | 输出窗口 (三次执行) |
| 14 | if(res==0) | if(res==0) | 输入字符串: |
| 15 | puts("Strings are equal"); | puts("Strings are equal"); | hello |
| 16 | else | else | 输入字符串 2: |
| 17 | puts("Strings are not equal"); | puts("Strings are not equal"); | HELLO |
| 18 | } | } | 字符串不相等 |
| 19 | | int mystrcmp(const char* s1, const char* s2) | |
| 20 | | { | |
| 21 | | int i=0; | |
| 22 | | while(s1[i]!='\0' && s2[i]!='\0') { | |
| 23 | | if((s1[i]==s2[i])||(s1[i]-s2[i])==32 || (s1[i]-s2[i])==-32) { | |
| 24 | | i++; | |
| 25 | | else { | |
| 26 | | return(s1[i]-s2[i]); | |
| 27 | | } | |
| 28 | | return 0; | |
| 29 | | } | |

**程序 7-11** 一个不区分大小写比较两个字符串的程序，(a) 使用库函数，(b) 使用用户定义函数。

## 7.5.6 strrev 函数

**角色：** `strrev` 函数反转字符串中除终止空字符以外的所有字符。

**输入：** 字符数组、字符指针或字符串字面量常量形式的字符串。

**输出：** `strrev` 函数反转字符串并指向反转后字符串的指针。程序 7-12 中的代码段说明了 `strrev` 函数的使用以及 `strrev` 函数的实现。

**用法：**

| 行号 | 程序 7-12a.c 使用库函数 | 程序 7-12b.c 使用用户定义函数 | 输出窗口 |
|---|---|---|---|
| 1 | //反转字符串的内容 | //反转字符串的内容 | 输入一个字符串: |
| 2 | #include<stdio.h> | #include<stdio.h> | Hello |
| 3 | #include<string.h> | char* mystrev(char* s); | 反转后，字符串是: |
| 4 | main() | main() | alleH |
| 5 | { | { | |
| 6 | char str[20]; | char str[20]; | 输出窗口 |
| 7 | puts("Enter a string:"); | puts("Enter a string:"); | (第二次执行) |
| 8 | gets(str); | mystrev(str); | 输入一个字符串: |
| 9 | strrev(str); | puts("After reversal, the string is:"); | Hello Readers |
| 10 | puts("After reversal, the string is:"); | puts(str); | 反转后，字符串是: |
| 11 | puts(str); | char* mystrev(char* s) | sredaeR alleH |
| 12 | } | { | 备注: |
| 13 | | int i=0, j; | • strrev 函数也可以应用于 |
| 14 | | char temp; | 字符串字面量 |
| 15 | | while(s[i]!='\0') | 字面量，例如，strrev("Hello")="alleH" |
| 16 | | i++; | • strrev(strrev("String"))="String" |
| 17 | | i--; | • 字符串的反反转 |
| 18 | | j=0; | 是字符串本身 |
| 19 | | while(j < i) | |
| 20 | | { | |
| 21 | | temp=s[i]; | |
| 22 | | s[i]=s[j]; | |
| 23 | | s[j]=temp; | |
| 24 | | j++;i--; | |
| 25 | | } | |
| 26 | | return s; | |
| 27 | | } | |

**程序 7-12** 使用库函数 (a) 和使用用户定义函数 (b) 反转字符串内容的程序。

## 7.5.7 strlwr 函数

**角色：** `strlwr` 函数将字符串中的所有字母转换为小写。

**输入：** 字符数组、字符指针或字符串字面量常量形式的字符串。

## 7.14 数组、指针和字符串

**输出：** 它返回指向转换后字符串的指针。

**用法：** 程序 7-13 中的代码段说明了 `strlwr` 函数的使用以及 `strlwr` 功能的实现。

| 行号 | 程序 7-13a.c | 程序 7-13b.c | 输出窗口 |
|---|---|---|---|
| | 使用库函数 | 使用用户定义函数 | |
| 1 | //将字符串的所有字符 | //将字符串的所有字符 | 输入一个字符串: HELLO |
| 2 | //字符串转换为小写 | //字符串转换为小写 | 小写字符串: hello |
| 3 | #include<stdio.h> | #include<stdio.h> | |
| 4 | #include<string.h> | char* mystrlwr(char* s); | 输出窗口（第二次执行） |
| 5 | main() | main() | |
| 6 | { | { | |
| 7 | char str[20]; | char str[20]; | 输入一个字符串: HELLO READERS!! |
| 8 | puts("Enter string:"); | puts("Enter string:"); | 小写字符串是: hello readers!! |
| 9 | gets(str); | gets(str); | |
| 10 | strlwr(str); | mystrlwr(str); | 备注: |
| 11 | puts("Lowercase string is:"); | puts("Lowercase string is:"); | - 字符串中的数字、特殊字符和空白字符保持不变 |
| 12 | puts(str); | puts(str); | |
| 13 | } | } | |
| 14 | | char* mystrlwr(char* s) | |
| 15 | | { | |
| 16 | | int i=0; | |
| 17 | | while(s[i]!='\0') | |
| 18 | | { | |
| 19 | | if(s[i]>=65 && s[i]<=90) | |
| 20 | | s[i]+=32; | |
| 21 | | i++; | |
| 22 | | } | |
| 23 | | return s; | |
| 24 | | } | |

**程序 7-13** 使用库函数 (a) 和使用用户定义函数 (b) 将字符串的所有字符转换为小写的程序。

## 7.5.8 strupr 函数

**角色：** `strupr` 函数将字符串中的所有字母转换为大写。

**输入：** 字符数组、字符指针或字符串字面量常量。

**输出：** 它返回转换后字符串的指针。

**用法：** 程序 7-14 中的代码段说明了 `strupr` 函数的使用。

## 字符串和字符数组

| 行号 | 程序 7-14a.c | 程序 7-14b.c | 输出窗口 |
|---|---|---|---|
| | 使用库函数 | 使用用户定义函数 | |
| 1 | //将字符串的所有字符 | //将字符串的所有字符 | 输入一个字符串: |
| 2 | //字符串转换为大写 | //字符串转换为大写 | hello |
