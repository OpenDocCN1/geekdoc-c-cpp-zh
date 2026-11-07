

| 函数原型 | 函数描述 |
|---|---|
| `int strncmp( const char *s1, const char *s2, size_t n );` | 将字符串 s1 的前 n 个字符与字符串 s2 进行比较。如果 s1 的 n 个字符部分分别等于、小于或大于 s2 对应的 n 个字符部分，则函数返回零、小于零或大于零。 |
| `char *strtok( char *s1, const char *s2 );` | 对 `strtok` 的一系列调用将字符串 s1 分割成多个标记——即逻辑片段，例如一行文本中的单词。分割过程基于字符串 s2 中包含的字符。例如，如果我们要基于字符 ':' 将字符串 "this:is:a:string" 分割成标记，则得到的标记将是 "this"、"is"、"a" 和 "string"。函数 `strtok` 一次只返回一个标记——第一次调用以 s1 作为第一个参数，而后续继续对同一字符串进行标记化的调用则以 NULL 作为第一个参数。每次调用返回指向当前标记的指针。如果调用该函数时已没有更多标记，则返回 NULL。 |
| `size_t strlen( const char *s );` | 确定字符串 s 的长度。返回终止空字符之前的字符数。 |

**图 22.21** | 字符串处理库的字符串操作函数。（第 2 部分，共 2 部分。）

图 22.21 中的几个函数包含数据类型为 `size_t` 的参数。该类型在头文件 `<cstring>` 中定义为无符号整型，例如 `unsigned int` 或 `unsigned long`。

![](img/b42ba5cd262b1358d16610173f975e4d_939_0.png)

### 常见编程错误 22.7

使用字符串处理库中的函数时，忘记包含 `<cstring>` 头文件会导致编译错误。

## 使用 strcpy 和 strncpy 复制字符串

函数 `strcpy` 将其第二个参数（一个字符串）复制到其第一个参数（一个字符数组）中，该数组必须足够大以存储该字符串及其终止空字符（终止空字符也会被复制）。函数 `strncpy` 与 `strcpy` 非常相似，只不过 `strncpy` 指定了要从字符串复制到数组的字符数。函数 `strncpy` 不一定会复制其第二个参数的终止空字符——只有当要复制的字符数至少比字符串长度多 1 时，才会写入终止空字符。例如，如果第二个参数是 "test"，那么只有当 `strncpy` 的第三个参数至少为 5（"test" 中的 4 个字符加上 1 个终止空字符）时，才会写入终止空字符。如果第三个参数大于 5，则会在数组后追加空字符，直到写入第三个参数指定的总字符数为止。

![](img/b42ba5cd262b1358d16610173f975e4d_940_0.png)

### 常见编程错误 22.8

使用 `strncpy` 时，如果 `strncpy` 第三个参数指定的字符数不大于第二个参数的长度，则第二个参数（一个 `char *` 字符串）的终止空字符将不会被复制。在这种情况下，如果您不手动用空字符终止生成的 `char *` 字符串，则可能发生致命错误。

图 22.22 使用 `strcpy`（第 13 行）将数组 x 中的整个字符串复制到数组 y 中，并使用 `strncpy`（第 19 行）将数组 x 的前 14 个字符复制到数组 z 中。第 20 行向数组 z 追加一个空字符（`'\0'`），因为程序中 `strncpy` 的调用没有写入终止空字符。（第三个参数小于第二个参数的字符串长度加 1。）

```cpp
// Fig. 22.22: fig22_22.cpp
// Using strcpy and strncpy.
#include <iostream>
#include <cstring> // prototypes for strcpy and strncpy
using namespace std;

int main()
{
   char x[] = "Happy Birthday to You"; // string length 21
   char y[25];
   char z[15];

   strcpy(y, x); // copy contents of x into y

   cout << "The string in array x is: " << x
        << "\nThe string in array y is: " << y << '\n';

   // copy first 14 characters of x into z
   strncpy(z, x, 14); // does not copy null character
   z[14] = '\0'; // append '\0' to z's contents

   cout << "The string in array z is: " << z << endl;
} // end main
```

```text
The string in array x is: Happy Birthday to You
The string in array y is: Happy Birthday to You
The string in array z is: Happy Birthday
```

**图 22.22** | `strcpy` 和 `strncpy`。

## 使用 strcat 和 strncat 拼接字符串

函数 `strcat` 将其第二个参数（一个字符串）追加到其第一个参数（一个包含字符串的字符数组）的末尾。第二个参数的第一个字符会替换第一个参数中终止字符串的空字符（`'\0'`）。您必须确保用于存储第一个字符串的数组足够大，能够存储第一个字符串、第二个字符串以及终止空字符（从第二个字符串中复制）的拼接结果。函数 `strncat` 将第二个字符串中指定数量的字符追加到第一个字符串的末尾，并在结果末尾追加一个终止空字符。图 22.23 中的程序演示了函数 `strcat`（第 15 行和第 25 行）和函数 `strncat`（第 20 行）。

```cpp
// Fig. 22.23: fig22_23.cpp
// Using strcat and strncat.
#include <iostream>
#include <cstring> // prototypes for strcat and strncat
using namespace std;

int main()
{
   char s1[20] = "Happy"; // length 6
   char s2[] = "New Year"; // length 9
   char s3[40] = "";

   cout << "s1 = " << s1 << "\ns2 = " << s2;

   strcat(s1, s2); // concatenate s2 to s1 (length 15)

   cout << "\n\nAfter strcat(s1, s2):\ns1 = " << s1 << "\ns2 = " << s2;

   // concatenate first 6 characters of s1 to s3
   strncat(s3, s1, 6); // places '\0' after last character

   cout << "\n\nAfter strncat(s3, s1, 6):\ns1 = " << s1
        << "\ns3 = " << s3;

   strcat(s3, s1); // concatenate s1 to s3
   cout << "\n\nAfter strcat(s3, s1):\ns1 = " << s1
        << "\ns3 = " << s3 << endl;
} // end main
```

```text
s1 = Happy
s2 = New Year

After strcat(s1, s2):
s1 = Happy New Year
s2 = New Year

After strncat(s3, s1, 6):
s1 = Happy New Year
s3 = Happy

After strcat(s3, s1):
s1 = Happy New Year
s3 = Happy Happy New Year
```

**图 22.23** | `strcat` 和 `strncat`。

## 使用 strcmp 和 strncmp 比较字符串

图 22.24 使用 `strcmp`（第 15–17 行）和 `strncmp`（第 20–22 行）比较三个字符串。函数 `strcmp` 将第一个字符串参数与第二个字符串参数逐字符进行比较。如果两个字符串相等，函数返回零；如果第一个字符串小于第二个字符串，返回负值；如果第一个字符串大于第二个字符串，返回正值。函数 `strncmp` 与 `strcmp` 等价，只是 `strncmp` 最多比较指定数量的字符。函数 `strncmp` 在达到指定字符数后停止比较字符。

计算机如何知道一个字母“排在”另一个字母“之前”呢？所有字符在计算机内部都表示为数字代码；当计算机比较两个字符串时，它实际上是比较字符串中字符的数字代码。

> [注意：对于某些编译器，函数 `strcmp` 和 `strncmp` 始终返回 −1、0 或 1，如图 22.24 的示例输出所示。对于其他编译器，这些函数返回 0，或返回被比较字符串中第一个不同字符的数字代码之差。例如，当比较 s1 和 s3 时，它们之间第一个不同的字符是每个字符串中第二个单词的第一个字符——s1 中的 N（数字代码 78）和 s3 中的 H（数字代码 72）。在这种情况下，返回值将为 6（如果比较 s3 和 s1，则为 −6）。]

## 使用 strtok 将字符串标记化

函数 `strtok` 将一个字符串分割为一系列标记。标记是由分隔符（通常是空格或标点符号）分隔的字符序列。例如，在一行文本中，每个单词都可以视为一个标记，而分隔单词的空格可以视为分隔符。要将一个字符串分割为标记，需要多次调用 `strtok`（假设该字符串包含多个标记）。第一次调用 `strtok` 时包含两个参数：一个要标记化的字符串，以及一个包含用于分隔标记的字符（即分隔符）的字符串。图 22.25 中的第 15 行将指向 sentence 中第一个标记的指针赋给 `tokenPtr`。第二个参数 `" "` 表示 sentence 中的标记由空格分隔。函数 `strtok` 查找 sentence 中第一个不是分隔字符（空格）的字符。这标志着第一个标记的开始。然后，该函数在字符串中查找下一个分隔字符，并将其替换为空（`'\0'`）字符。这结束了当前标记。函数 `strtok`（在一个静态变量中）保存指向 sentence 中该标记之后下一个字符的指针，并返回指向当前标记的指针。

```cpp
// Fig. 22.25: fig22_25.cpp
// Using strtok to tokenize a string.
#include <iostream>
#include <cstring> // prototype for strtok
using namespace std;

int main()
{
   char sentence[] = "This is a sentence with 7 tokens";

   cout << "The string to be tokenized is:\n" << sentence
        << "\n\nThe tokens are:\n";

   // begin tokenization of sentence
   char *tokenPtr = strtok( sentence, " " );

   // continue tokenizing sentence until tokenPtr becomes NULL
   while ( tokenPtr != NULL )
   {
      cout << tokenPtr << '\n';
      tokenPtr = strtok( NULL, " " ); // get next token
   } // end while
```

**图 22.25** | 使用 `strtok` 将字符串标记化。（第 1 部分，共 2 部分。）

