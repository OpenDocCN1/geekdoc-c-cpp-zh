
```c
// fig08_18.c
// Using function strspn
#include <stdio.h>
#include <string.h>

int main(void) {
   const char *string1 = "The value is 3.14159";
   const char *string2 = "aehil 1sTuv";

   printf("string1 = %s\nstring2 = %s\n\n%s\n%s\n", string1, string2,
      "The length of the initial segment of string1"
      "containing only characters from string2 = ",
      strspn(string1, string2));
}
```

```text
string1 = The value is 3.14159
string2 = aehil 1sTuv

The length of the initial segment of string1
containing only characters from string2 = 13
```

**图 8.18** | 使用函数 strspn。

### 8.8.6 函数 strstr

函数 strstr 在其第一个字符串参数中搜索其第二个字符串参数首次出现的位置。如果在第一个字符串中找到第二个字符串，strstr 返回指向第二个字符串在第一个字符串中位置的指针。图 8.19 使用 strstr 在字符串 "abcdefabcdef" 中查找字符串 "def"。

```c
// fig08_19.c
// Using function strstr
#include <stdio.h>
#include <string.h>

int main(void) {
   const char *string1 = "abcdefabcdef";
   const char *string2 = "def"; // string to search for

   printf("string1 = %s\nstring2 = %s\n\n%s\n%s\n", string1, string2,
      "The remainder of string1 beginning with the"
      "first occurrence of string2 is: ", strstr(string1, string2));
}
```

```text
string1 = abcdefabcdef
string2 = def

The remainder of string1 beginning with the
first occurrence of string2 is: defabcdef
```

**图 8.19** | 使用函数 strstr。

### 8.8.7 函数 strtok

函数 *strtok*（图 8.20）将字符串分解为一系列标记——这也称为对字符串进行标记化。标记是由分隔符（例如*空格*或*标点符号*）分隔的字符序列。分隔符可以是任意字符。例如，在一行文本中，每个单词都是一个标记，而分隔单词的空格和标点符号则是分隔符。你可以在每次 *strtok* 调用中更改分隔符字符串。图 8.20 对字符串 "This is a sentence with 7 tokens" 进行标记化并打印这些标记。函数 *strtok 会修改输入字符串*，方法是在每个标记末尾放置 '\0'，因此如果你打算在调用 *strtok* 之后继续使用该字符串，请先复制它。关于假设 *strtok* 不会修改其第一个参数中的字符串所导致的问题，请参见 CERT 建议 STR06-C。

```c
1  // Fig08_20.c
2  // Using function strtok
3  #include <stdio.h>
4  #include <string.h>
5
6  int main(void) {
7     char string[] = "This is a sentence with 7 tokens";
8
9     printf("The string to be tokenized is:\n%s\n\n", string);
10    puts("The tokens are:");
11
12    char *tokenPtr = strtok(string, " "); // begin tokenizing sentence
13
14    // continue tokenizing sentence until tokenPtr becomes NULL
15    while (tokenPtr != NULL) {
16        printf("%s\n", tokenPtr);
17        tokenPtr = strtok(NULL, " "); // get next token
18    }
19 }
```

```text
The string to be tokenized is:
This is a sentence with 7 tokens

The tokens are:
This
is
a
sentence
with
7
tokens
```

**图 8.20** | 使用函数 strtok。

### 第一次调用 strtok

假设一个字符串包含多个标记，则需要对 *strtok* 进行多次调用才能对该字符串进行标记化。第一次调用 *strtok*（第 12 行）接收两个参数：要标记化的字符串，以及包含分隔标记字符的字符串。以下语句

```c
char *tokenPtr = strtok(string, " "); // begin tokenizing sentence
```

将 tokenPtr 赋值为指向 string 中第一个标记的指针。第二个参数 " " 表示标记由空格分隔。函数 strtok 在 string 中搜索第一个不是分隔符（空格）的字符。这标志着第一个标记的开始。然后，该函数在 string 中找到下一个分隔符，并用空字符（'\0'）替换它，以终止当前标记。函数 strtok 保存指向 string 中该标记之后字符的指针，并返回指向当前标记的指针。

### 后续调用 strtok

第 17 行中后续的 strtok 调用继续对 string 进行标记化。这些调用将 NULL 作为第一个参数，以表明它们应从上次调用所保存的 string 中的位置继续标记化。如果没有剩余标记，strtok 返回 NULL。

### 自测

1（选择题）以下哪项描述的是“在字符串 s1 中定位字符串 s2 的首次出现——如果找到该字符串，函数返回指向 s1 中该字符串的指针；否则返回 NULL”？

+   - a) strpbrk。
+   - b) strstr。
+   - c) strspn。
+   - d) strcspn。

答案：b. strstr。

2（填空题）在函数 strtok 的语境中，______ 是由分隔符分隔的字符序列。

答案：标记。

## 8.9 字符串处理库的内存函数

本节中的字符串处理库函数用于操作、比较和搜索内存块。这些函数将内存视为字符数组，并且可以操作任意数据块。下表总结了字符串处理库的内存函数。在函数讨论中，“对象”指的是一个数据块。

| 函数原型 | 函数描述 |
|---|---|
| `void *memcpy(void *s1, const void *s2, size_t n);` | 从 s2 所指向的对象复制 n 个字节到 s1 所指向的对象，然后返回指向结果对象的指针。 |
| `void *memmove(void *s1, const void *s2, size_t n);` | 从 s2 所指向的对象复制 n 个字节到 s1 所指向的对象。复制过程就好像先将字节从 s2 所指向的对象复制到临时数组，再从临时数组复制到 s1 所指向的对象。返回指向结果对象的指针。 |
| `int memcmp(const void *s1, const void *s2, size_t n);` | 比较 s1 和 s2 所指向对象的前 n 个字节。如果 s1 等于、小于或大于 s2，函数分别返回 0、小于 0 或大于 0。 |
| `void *memchr(const void *s, int c, size_t n);` | 在 s 所指向对象的前 n 个字节中定位 c（转换为 unsigned char）首次出现的位置。如果找到 c，memchr 返回指向对象中 c 的指针；否则返回 NULL。 |
| `void *memset(void *s, int c, size_t n);` | 将 c（转换为 unsigned char）复制到 s 所指向对象的前 n 个字节中，然后返回指向结果的指针。 |

这些指针参数声明为 `void *`，因此可用于操作任意数据类型的内存。回顾第 7 章可知，任何指针都可以直接赋值给 `void *` 指针，而 `void *` 指针也可以直接赋值给任何其他类型的指针。由于不能解引用 `void *` 指针，每个函数都接收一个大小参数，用于指定该函数将处理的字节数。为简单起见，本节中的示例操作字符数组（字符块）。上表中的函数*不*检查终止空字符，因为它们操作的内存块不一定是字符串。

### 8.9.1 函数 memcpy

函数 `memcpy` 从其第二个参数所指向的对象复制指定数量的字节到其第一个参数所指向的对象。该函数可以接收指向任意类型对象的指针。如果两个对象在内存中重叠——也就是说，它们是同一对象的一部分——则其结果是*未定义*的。在这种情况下，请改用 `memmove`。图 8.21 使用 `memcpy` 将数组 `s2` 中的字符串复制到数组 `s1`。当你已知要复制的字符串大小时，函数 `memcpy` 比 `strcpy` 更高效。

```c
1    // fig08_21.c
2    // Using function memcpy
3    #include <stdio.h>
4    #include <string.h>
5
6    int main(void) {
7        char s1[17] = "";
8        char s2[] = "Copy this string";
9
10       memcpy(s1, s2, 17); // 17 so we copy s2's terminating \0
11       puts("After s2 is copied into s1 with memcpy, s1 contains:");
12       puts(s1);
13   }
```

**图 8.21** | 使用函数 memcpy。（第 1 部分，共 2 部分。）
