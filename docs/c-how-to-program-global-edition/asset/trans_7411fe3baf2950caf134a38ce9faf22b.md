
```
28     printf("\'%c\' was not found in \"%s\".\n", 
29             character2, string);
30     }
31 }
```

'a' 在 "This is a test" 中被找到。
'z' 在 "This is a test" 中未被找到。

图 8.20 | 使用函数 strchr。 (Part 2 of 2.)

## 8.8.2 函数 strcspn

函数 strcspn (图 8.21) 确定其第一个参数中字符串的初始部分的长度，该部分不包含第二个参数中字符串的任何字符。函数返回该段的长度。

```
1  // Fig. 8.21: fig08_21.c
2  // Using function strcspn
3  #include <stdio.h>
4  #include <string.h>
5
6  int main(void)
7  {
8      // initialize two char pointers
9      const char *string1 = "The value is 3.14159";
10     const char *string2 = "1234567890";
11
12     printf("\n%s\n%s\n\n%s\n%s\n%s\n", string1, string2,
13            "The length of the initial segment of string1",
14            "containing no characters from string2 = ",
15            strcspn(string1, string2) );
16 }
```

string1 = The value is 3.14159
string2 = 1234567890

string1 的初始段的长度
不包含来自 string2 的字符 = 13

图 8.21 | 使用函数 strcspn。

## 8.8.3 函数 strpbrk

函数 strpbrk 在其第一个字符串参数中搜索第二个字符串参数中任何字符的首次出现。如果找到第二个参数中的字符，strpbrk 会返回指向第一个参数中该字符的指针；否则，strpbrk 返回 NULL。图 8.22 显示了一个程序，该程序定位 string1 中来自 string2 的任何字符的首次出现。

// Fig. 8.22: fig08_22.c
// Using function strpbrk
#include <stdio.h>
#include <string.h>

int main(void)
{
    const char *string1 = "This is a test"; // initialize char pointer
    const char *string2 = "beware"; // initialize char pointer

    printf("%s\n%s\n%c%s\n%s\n",
           "Of the characters in ",
           string2,
           *strpbrk(string1, string2),
           " appears earliest in ", string1);
}

"beware" 中的字符中
'a' 最早出现在
"This is a test" 中

图 8.22 | 使用函数 strpbrk。

## 8.8.4 函数 strrchr

函数 strrchr 在字符串中搜索指定字符的最后一次出现。如果找到该字符，strrchr 会返回指向字符串中该字符的指针；否则，strrchr 返回 NULL。图 8.23 显示了一个程序，该程序在字符串 "A zoo has many animals including zebras" 中搜索字符 'z' 的最后一次出现。

// Fig. 8.23: fig08_23.c
// Using function strrchr
#include <stdio.h>
#include <string.h>

int main(void)
{
    // initialize char pointer
    const char *string1 = "A zoo has many animals including zebras";

    int c = 'z'; // character to search for
    printf("%s\n%s%c%s\n",
           "The remainder of string1 beginning with the",
           "last occurrence of character ", c,
           " is: ", strrchr(string1, c));
}

从字符 'z' 的最后一次出现开始的 string1 的剩余部分是："zebras"

图 8.23 | 使用函数 strrchr。

## 8.8.5 函数 strspn

函数 strspn (图 8.24) 确定其第一个参数中字符串的初始部分的长度，该部分仅包含第二个参数中字符串的字符。函数返回该段的长度。

// Fig. 8.24: fig08_24.c
// Using function strspn
#include <stdio.h>
#include <string.h>

int main(void)
{
    // initialize two char pointers
    const char *string1 = "The value is 3.14159";
    const char *string2 = "aehi 1sTuv";

    printf("%s\n%s\n%s\n%s\n",
    "string1 = ", string1, "string2 = ", string2,
    "The length of the initial segment of string1",
    "containing only characters from string2 = ",
    strspn(string1, string2));
}

string1 = The value is 3.14159
string2 = aehi 1sTuv
string1 的初始段的长度
仅包含来自 string2 的字符 = 13

图 8.24 | 使用函数 strspn。

## 8.8.6 函数 strstr

函数 strstr 在其第一个字符串参数中搜索第二个字符串参数的首次出现。如果在第一个字符串中找到第二个字符串，则返回指向第一个参数中该字符串位置的指针。图 8.25 使用 strstr 在字符串 "abcdefabcdef" 中查找字符串 "def"。

// Fig. 8.25: fig08_25.c
// Using function strstr
#include <stdio.h>
#include <string.h>

int main(void)
{
    const char *string1 = "abcdefabcdef"; // string to search
    const char *string2 = "def"; // string to search for

图 8.25 | 使用函数 strstr。 (Part 1 of 2.)

```
    11        printf("%s%s\n%s\n%s\n%s\n%s\n",
    12            "string1 = ", string1, "string2 = ", string2,
    13            "The remainder of string1 beginning with the",
    14            "first occurrence of string2 is: ",
    15            strstr(string1, string2) );
    16    }
```

```
    string1 = abcdefabcdef
    string2 = def

    The remainder of string1 beginning with the
    first occurrence of string2 is: defabcdef
```

图 8.25 | 使用函数 strstr。 (Part 2 of 2.)

## 8.8.7 函数 strtok

函数 strtok (图 8.26) 用于将字符串分解为一系列标记。标记是由定界符分隔的字符序列（通常是 *空格或标点符号*，但定界符可以是 *任何字符*）。例如，在一行文本中，每个单词可以被视为一个标记，而分隔单词的空格和标点可以被视为定界符。

```
    1    // Fig. 8.26: fig08_26.c
    2    // Using function strtok
    3    #include <stdio.h>
    4    #include <string.h>
    5
    6    int main(void)
    7    {
    8        // initialize array string
    9        char string[] = "This is a sentence with 7 tokens";
    10
    11       printf("%s\n%s\n%s\n%s\n",
    12           "The string to be tokenized is:", string,
    13           "The tokens are:");
    14
    15       char *tokenPtr = strtok(string, " "); // begin tokenizing sentence
    16
    17       // continue tokenizing sentence until tokenPtr becomes NULL
    18       while (tokenPtr != NULL) {
    19           printf("%s\n", tokenPtr);
    20           tokenPtr = strtok(NULL, " "); // get next token
    21       }
    22   }
```

```
    The string to be tokenized is:
    This is a sentence with 7 tokens
```

图 8.26 | 使用函数 strtok。 (Part 1 of 2.)

![](img/bf54db922e6fa8319cba11069e785521_385_0.png)

图 8.26 | 使用函数 strtok。 (Part 2 of 2.)

对字符串进行标记化（即将其分解为标记，假设字符串包含多个标记）需要多次调用 strtok。第一次调用 strtok（第 15 行）包含两个参数：要标记化的字符串，以及包含分隔标记的字符的字符串。在第 15 行，语句

```
char * tokenPtr = strtok(string, " "); // begin tokenizing sentence
```

将 tokenPtr 分配为指向 string 中第一个标记的指针。第二个参数 " " 表示标记由空格分隔。函数 strtok 在 string 中搜索第一个不是定界字符（空格）的字符。这开始了第一个标记。然后函数在字符串中找到下一个定界字符，并将其替换为 null ('\0') 字符以终止当前标记。函数 strtok 保存指向 string 中标记后下一个字符的指针并返回指向当前标记的指针。

第 20 行中的后续 strtok 调用继续对 string 进行标记化。这些调用的第一个参数为 NULL。NULL 参数表示应从上一次 strtok 调用保存的 string 中的位置继续标记化。如果调用 strtok 时没有剩余标记，strtok 将返回 NULL。您可以在每次新的 strtok 调用中更改定界符字符串。图 8.26 使用 strtok 对字符串 "This is a sentence with 7 tokens" 进行标记化。每个标记分别打印。函数 strtok 通过在每个标记末尾放置 '\0' 来修改输入字符串；因此，如果在调用 strtok 之后仍需使用该字符串，则应制作字符串的副本。[注意：另请参阅 CERT 建议 STR06-C，其中讨论了假设 strtok 不修改其第一个参数中字符串的问题。]

## 8.9 字符串处理库的内存函数

本节介绍的字符串处理库函数操作、比较和搜索内存块。这些函数将内存块视为字符数组，可以操作任何数据块。图 8.27 总结了字符串处理库的内存函数。[注意：这些函数中的每个函数都有在 C11 标准的可选附录 K 中描述的更安全的版本。我们在本章的 Secure C Programming 部分中提到这些。]

指针参数声明为 void *，因此它们可用于操作任何数据类型中的内存。回顾第 7 章，任何指针都可以直接分配给类型为 void * 的指针，而类型为 void * 的指针可以直接分配给任何其他类型的指针。由于 void * 指针不能被解引用，每个函数都会接收一个 size 参数，该参数指定函数将处理的字节数。对于
