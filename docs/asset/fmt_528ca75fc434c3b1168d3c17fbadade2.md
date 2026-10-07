
```c
// fig08_12.c
// 使用函数 strcat 和 strcpy
#include <stdio.h>
#include <string.h>

int main(void) {
    char s1[20] = "Happy"; // 初始化数组 s1
    char s2[] = "New Year"; // 初始化数组 s2
    char s3[40] = ""; // 初始化数组 s3 为空

    printf("%s%s\n", s1, s2);

    // 将 s2 追加到 s1
    printf("%s%s\n", strcat(s1, s2));

    // 将 s1 追加到 s3
    printf("%s%s\n", strncat(s3, s1, 6), s3);

    // 将 s2 追加到 s3
    printf("%s%s\n", strcat(s3, s3));
}
```

```
s1 = Happy
s2 = New Year
strcat(s1, s2) = Happy New Year
strncat(s3, s1, 6) = Happy
strcat(s3, s3) = Happy New Year
```

图 8.12 | 使用函数 `strcat` 和 `strncat`。

## 自测

- （多选题）关于函数 `strcat` 和 `strncat` 的哪个描述是错误的？

a) 函数 `strcat` 将其第二个参数字符串追加到第一个参数 `char` 数组中。

b) `strcat` 第二个参数的第一个字符紧跟在终止第一个字符串的空（`'\0'`）字符之后。

c) 你必须确保存储第一个字符串的数组足够大，能够存储第一个字符串、第二个字符串以及从第二个字符串复制的终止空字符。

d) 函数 `strcat` 将第二个字符串中指定数量的字符追加到第一个字符串中，并添加一个终止的 `'\0'`。

- （填空题）你必须确保存储第一个字符串的数组足够大，能够存储第一个字符串、第二个字符串以及从第二个字符串复制的终止空字符。

- （填空题）只有在拷贝指定数量的字符时，`strncpy` 等于 `strcpy`。

- （填空题）如果第三个参数小于或等于第二个参数的长度，而你没有为 `strncpy` 的第一个参数追加终止空字符，则是一个逻辑错误。

## 8.8 字符串处理库的搜索函数

### 函数原型与描述

```
size_t strcspn(const char *s1, const char *s2);
```

确定并返回字符串 `s1` 前部内容的长度，该片段仅由字符串 `s2` 中包含的字符组成。

```
char *strchr(const char *s1, const char *s2);
```

在字符串 `s1` 中定位 `s2` 中任意字符的首次出现位置。如果找到了 `s2` 中的字符，`strchr` 返回指向 `s1` 中该字符的指针；否则，返回 `NULL`。

```
char *strrchr(const char *s, int c);
```

在字符串 `s` 中定位 `c` 的最后一次出现位置。如果找到了 `c`，`strrchr` 返回指向字符串中 `c` 的指针；否则，返回 `NULL`。

```
char *strtok(const char *s1, const char *s2);
```

在 `s1` 中定位字符串 `s2` 的首次出现位置。如果找到了该字符串，`strstr` 返回指向 `s1` 中该字符串的指针。

多次调用 `strtok` 将 `s1` 拆分为由 `s2` 中包含的字符分隔的标记（tokens）。标记是逻辑片段，就像一行文本一样。第一次调用使用 `s1` 作为第一个参数。后续对字符串进行分词的调用需要将第一个参数为 `NULL`。每次调用返回指向当前标记的指针。如果没有更多标记，`strtok` 返回 `NULL`。

#### 8.8.1 函数 strchr

函数 `strchr` 在字符串中搜索某个字符的首次出现位置。如果找到了该字符，`strchr` 返回指向字符串中该字符的指针；否则，`strchr` 返回 `NULL`。8.14 显示在 "This is a test" 中搜索 'a' 和 'z' 的首次出现位置。

```
1 // fig08_c.c
2 // 使用函数 strchr
3 #include <stdio.h>
4 #include <string.h>
5
6 int main(void) {
7 const char *string = "This is a test"; // 初始化字符指针
8 char character1 = 'a';
9 char character2 = 'z';
10
11 // 如果在 string 中找到了 character1
12 if (strchr(string,character1) != NULL) { // 可以移除 "!= NULL"
13 printf("%c' found in "%s".\n", character1, string);
14 }
15 else // 如果没有找到 character1
16 printf("%c' not found in "%s".\n", character1, string);
17 }
```

图 8.14 | 使用函数 `strchr`。（2 部分中的第一部分）。

```
18  // 如果在 string 中找到了 character2 // 可以移除 "!= NULL"
19  if (strchr(string, character2) != NULL) { // 可以移除
20      printf("%c' was found in %s.\n", character2, string);
21  }
22  else { // 如果没有找到 character2
23      printf("%c' was not found in %s.\n", character2, string);
24  }
25 }
```

在 "This is a test" 中找到了 'a'。

在 "This is a test" 中没有找到 'z'。

图 8.14 使用 `strchr`。（2 部分中的第二部分。）

#### 8.8.2 函数 strcspn

函数 `strcspn`（图 8.15）确定其第一个参数起始部分的长度，该部分不包含第二个参数中的任何字符。该函数返回该片段的长度。

`string1` = The value is 3.14159

`string2` = 1234567890

`string1` 中不包含 `string2` 字符的起始片段长度 = 13

图 8.15 使用函数 `strcspn`。

#### 8.8.3 函数 strpbrk

函数 `strpbrk` 在其第一个参数中搜索其第二个参数中任意字符的首次出现位置。如果找到了第二个参数中的字符，`strpbrk` 返回指向第一个参数中该字符的指针；否则，返回 `NULL`。图 8.16 定位 `string1` 中来自 `string2` 的任意字符的首次出现位置。

```
 // fig08_16.c
// 使用函数 strpbrk
#include <stdio.h>
#include <string.h>

int main() {
    const char *string1 = "This is a test";
    const char *string2 = "beware";

    printf("%s%s\n", string2, strpbrk(string1, string2));
    printf("Of the characters in %s, appears earliest in %s\n", string2, string1);
}
```

"beware" 中的字符中

'a' 在 "This is a test" 中出现的最早

图 8.16 使用函数 `strpbrk`。

#### 8.8.4 函数 strrchr

函数 `strrchr` 在字符串中搜索指定字符的最后一次出现位置。如果找到了该字符，`strrchr` 返回指向字符串中字符的指针；否则，返回 `NULL`。图 8.17 在 "A zoo has animals" 中搜索 'z' 的最后一次出现位置。

```
// fig08_17.c
// 使用函数 strrchr
#include <stdio.h>
#include <string.h>

int main(){
    const char *string1 = "A zoo has animals";
    char c = 'z'; // 搜索字符

    if (strrchr(string1, c) != NULL) {
        printf("Last occurrence of %c found in %s.\n", c, string1);
    }
    else {
        printf("Last occurrence of %c not found in %s.\n", c, string1);
    }
}
```

在 "A zoo has animals" 中找到了 'z'。

图 8.17 使用函数 `strrchr`。

#### 8.8.5 函数 strspn

函数 `strspn`（图 8.18）确定其第一个参数起始部分的长度，该部分包含第二个参数中的任何字符。该函数返回该片段的长度。

```
// fig08_18.c
// 使用函数 strspn
#include <stdio.h>
#include <string.h>

int main(void) {
    const char *string1 = "The value is 3.14159";
    const char *string2 = "1234567890";

    printf("Length of initial segment of string1 containing no characters from string2 = %zu\n", strspn(string1, string2));
}
```

图 8.18 使用函数 `strspn`。

#### 8.8.6 函数 strstr

函数 `strstr` 在字符串中搜索其第二个参数的首次出现位置。如果在字符串中找到了该字符串，`strstr` 返回指向第一个字符串中该字符串的指针。图 8.19 在 "abcdef" 中查找字符串 "def"。

```
// fig08_19.c
// 使用函数 strstr
#include <stdio.h>
#include <string.h>

int main(void) {
    const char *string1 = "abcdef";
    const char *string2 = "def"; // 查找字符串

    if (strstr(string1, string2) != NULL) {
        printf("First occurrence of %s found in %s.\n", string2, string1);
    }
}
```

在 "abcdef" 中找到了 "def" 的首次出现位置。

图 8.19 使用 `strstr`。

#### 8.8.7 函数 strtok

函数 `strtok`（图 8.20）将字符串拆分为一系列由分隔符分隔的标记（tokens）。标记是由于分隔符分隔的字符序列。分隔符可以是任何字符。例如，在一行文本中，每个单词都是一个标记，分隔它们的空格就是分隔符。你可以在每次 `strtok` 调用中更改分隔符。图 8.20 对 "a sentence with 7 tokens" 进行分词并打印这些标记。`strtok` 通过在每个标记末尾替换 `'\0'` 来修改输入字符串，因此如果你打算使用字符串，请复制字符串。请参考 CERT 建议 STR06-C 关于使用 `strtok` 时不修改字符串的问题。

```
// fig08_20.c
// 使用函数 strtok
#include <stdio.h>
#include <string.h>

int main(void) {
    char string[] = "This is a sentence with 7 tokens";

    printf("The string to be tokenized is:\n%s\n\n", string);
    puts("the tokens are:");

    char *tokenPtr = strtok(string, " "); // 开始分词

    // 继续分词直到 tokenPtr 变为 NULL
    while (tokenPtr != NULL) {
        printf("%s\n", tokenPtr);
        tokenPtr = strtok(NULL, " "); // 获取下一个标记
    }
}
```

| 要拆分的字符串是: |

This is a sentence with 7 tokens |

标记是: |

This

is

a

sentence

with

7

tokens |

图 8.20 使用 `strtok`。

# 第一次 strtok 调用

需要多次调用 `strtok` 来拆分字符串，假设它包含多个标记。第一次调用 `strtok`（第 12 行）接收的参数是待拆分的字符串和包含分隔标记字符的字符串。该语句

```
char *tokenPtr = strtok(string, " "); // 开始分词
```

# 第 8 章 字符与字符串

`assigns` 将 `tokenPtr` 设置指向字符串中第一个 token 的指针。第二个参数 " " 表示 token 是由空格分隔的。函数 `strtok` 寻找字符串中第一个不是分隔符（空格）的字符。这标记了第一个 token 的开始。该函数在字符串中寻找下一个分隔符，并将其替换为空字符（空字符，`'\0'`）以结束当前 token。函数 `strtok` 寻找一个指向字符串中该 token 之后字符的指针，并返回指向当前 token 的指针。

# 后续的 strtok 调用

第 17 行中的后续 `strtok` 调用将继续进行分标记。这些调用接收 `NULL` 作为其第一个参数，表示它们应该从上一次调用保存的位置继续分标记。如果没有剩余的 token，`strtok` 将返回 `NULL`。

## 自测

- 1 (单选题) 哪一个函数的描述是“在 s1 中查找字符串 s2 的第一次出现处——如果找到该字符串，函数返回指向 s1 中字符串的指针；否则，返回 NULL”？

  - a) strprbk

  - b) strstr

  - c) strcspn

  - d) strcspn

  答案：b. `strstr`。

- 2 (填空题) 在 `strtok` 函数的上下文中，______ 是一个由分隔符分隔的字符序列。

  答案：token。

## 8.9 字符串处理库的内存函数

本节中的字符串处理库函数用于操作、比较和搜索内存块。这些函数将内存视为字符数组并可以操作任何数据块。下表总结了字符串处理库的内存函数。在接后的讨论中，“对象”指的是一个数据块。

| 函数原型 | 函数描述 |

| --- | -- |

| `void *memcpy(void *s1, const void *s2, size_t n);` | 将字节从 `s2` 指向的对象拷贝到 `s1` 指向的对象中，然后返回指向该对象的指针。 |

| `void *memmove(void *s1, const void *s2, size_t n);` | 将字节从 `s2` 指向的对象拷贝到 `s1` 指向的对象中。如果字节先被拷贝到指向 `s2` 的对象的临时数组中，然后再从临时数组拷贝到 `s1` 指向的对象中，则执行拷贝。返回指向结果对象的指针。 |

| `int memcmp(const void *s1, const void *s2, size_t n)` | 比较 `s1` 和 `s2` 指向对象的 `n` 个字节。如果 `s1` 等于、小于或大于 `s2`，函数分别返回 0、小于 0 或大于 0。 |

| `void *memchr(const void *s, int c, size_t n)` | 在 `s` 指向的对象的前 `n` 个字节中定位 `c`（转换为无符号字符）的首次出现处。如果找到 `c`，`memchr` 返回指向对象中 `c` 的指针；否则，返回 `NULL`。 |

| `void *memset(void *s, int c, size_t n)` | 在 `s` 指向的对象的前 `n` 个字节中拷贝 `c`（转换为无符号字符），然后返回指向结果的指针。 |

这些指针参数被声明为 `void *`，因此它们可以被用于操作任何数据类型的内存。回想第 7 章，任何指针都可以直接赋值给一个 `void *` 指针，而 `void *` 可以赋值给任何其他类型的指针。由于 `void *` 指针无法被解引用，每个函数都接收一个大小参数，指定函数将处理的字节数。为了简单起见，本节中的示例操作的是字符数组（字符块）。前面的函数不检查终止字符，因为它们操作的内存块不一定是字符串。

### 8.9.1 函数 memcpy

`memcpy` 函数从其第二个参数指向的对象拷贝指定数量的字节到其第一个参数中。该函数可以接收指向任何类型对象的指针。如果两个对象的内存重叠——也就是说，它们是同一个对象的部分——则其结果是未定义的。在这种情况下，请使用 `memmove` 代替之。图 8.21 使用 `memcpy` 将 `s2` 中的字符串拷贝到 `s1`。当你知道要拷贝的字符串大大运行时，`memcpy` 比 `strcpy` 更高效。

```c
// fig08_21.c
// 使用函数 memcpy
#include <stdio.h>
#include <string.h>

int main(void) {
    char s1[17] = "";
    char s2[17] = "this string";

    memcpy(s1, s2, 17); // 拷贝 s2 的终止 \0
    puts("After s2 is copied into s1, s1 contains: ");
    puts(s1);
}
```
