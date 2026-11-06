

```cpp
1  // Fig. 21.33: fig21_33.cpp
2  // Using strtoul.
3  #include <iostream>
4  #include <cstdlib> // strtoul prototype
5  using namespace std;
6
7  int main()
8  {
9     unsigned long x;
10    const char *string1 = "1234567abc";
11    char *remainderPtr;
12
13    // convert a sequence of characters to unsigned long
14    x = strtoul( string1, &remainderPtr, 0 );
15
16    cout << "The original string is \"" << string1
17       << "\"\nThe converted value is " << x
18       << "\nThe remainder of the original string is \"" << remainderPtr
19       << "\"\nThe converted value minus 567 is " << x - 567 << endl;
20 } // end main
```

```text
The original string is "1234567abc"
The converted value is 1234567
The remainder of the original string is "abc"
The converted value minus 567 is 1234000
```

**图 21.33** | 字符串转换函数 `strtoul`。

### 21.12 基于指针的字符串处理库中的搜索函数

本节介绍字符串处理库中用于在字符串中搜索字符和其他字符串的函数。图 21.34 对这些函数进行了总结。函数 `strspn` 和 `strcspn` 指定返回类型为 `size_t`。类型 `size_t` 是由标准定义的一种类型，表示 `sizeof` 运算符返回值的整型类型。

| 原型 | 描述 |
| --- | --- |
| `char *strchr( const char *s, int c )` | 定位字符串 `s` 中字符 `c` 的首次出现位置。如果找到 `c`，则返回指向 `s` 中该字符的指针；否则返回空指针。 |
| `char *strrchr( const char *s, int c )` | 从字符串 `s` 的末尾开始搜索，并定位字符 `c` 在字符串 `s` 中最后一次出现的位置。如果找到 `c`，则返回指向字符串 `s` 中该字符的指针；否则返回空指针。 |
| `size_t strspn( const char *s1, const char *s2 )` | 确定并返回字符串 `s1` 初始部分的长度，该部分仅由字符串 `s2` 中包含的字符组成。 |
| `char *strpbrk( const char *s1, const char *s2 )` | 定位字符串 `s1` 中字符串 `s2` 的任意字符首次出现的位置。如果找到字符串 `s2` 中的某个字符，则返回指向字符串 `s1` 中该字符的指针；否则返回空指针。 |
| `size_t strcspn( const char *s1, const char *s2 )` | 确定并返回字符串 `s1` 初始部分的长度，该部分由字符串 `s2` 中不包含的字符组成。 |
| `char *strstr( const char *s1, const char *s2 )` | 定位字符串 `s2` 在字符串 `s1` 中首次出现的位置。如果找到该字符串，则返回指向 `s1` 中该字符串的指针；否则返回空指针。 |

**图 21.34** | 基于指针的字符串处理库中的搜索函数。

函数 **`strchr`** 用于搜索字符在字符串中首次出现的位置。如果找到该字符，`strchr` 将返回指向字符串中该字符的指针；否则，`strchr` 返回空指针。图 21.35 中的程序使用 `strchr`（第 14 行和第 22 行）在字符串 `"This is a test"` 中搜索 `'a'` 和 `'z'` 首次出现的位置。

```cpp
// Fig. 21.35: fig21_35.cpp
// Using strchr.
#include <iostream>
#include <cstring> // strchr prototype
using namespace std;

int main()
{
   const char *string1 = "This is a test";
   char character1 = 'a';
   char character2 = 'z';

   // search for character1 in string1
   if ( strchr( string1, character1 ) != NULL )
      cout << '\'' << character1 << "' was found in \""
         << string1 << "\"\n";
   else
      cout << '\'' << character1 << "' was not found in \""
         << string1 << "\"\n";

   // search for character2 in string1
   if ( strchr( string1, character2 ) != NULL )
      cout << '\'' << character2 << "' was found in \""
         << string1 << "\"\n";
```

**图 21.35** | 字符串搜索函数 `strchr`。（第 1 部分，共 2 部分。）

### 21.13 基于指针的字符串处理库中的内存函数

本节介绍的字符串处理库函数有助于操作、比较和搜索内存块。这些函数将内存块视为字节数组。这些函数可以操作任意数据块。图 21.41 总结了字符串处理库中的内存函数。在函数说明中，“对象”是指一个数据块。[注意：前几节中的字符串处理函数操作的是以空字符结尾的字符串。本节中的函数操作的是字节数组。空字符值（即包含 0 的字节）对本节中的函数没有特殊意义。]

| 原型 | 描述 |
| --- | --- |
| `void *memcpy( void *s1, const void *s2, size_t n )` | 将 `s2` 所指向对象中的 `n` 个字符复制到 `s1` 所指向的对象中。返回指向结果对象的指针。复制字符的区域不能与被复制到的区域重叠。 |
| `void *memmove( void *s1, const void *s2, size_t n )` | 将 `s2` 所指向对象中的 `n` 个字符复制到 `s1` 所指向的对象中。复制过程相当于先将字符从 `s2` 所指向的对象复制到临时数组中，再从临时数组复制到 `s1` 所指向的对象中。返回指向结果对象的指针。复制字符的区域可以与被复制到的区域重叠。 |
| `int memcmp( const void *s1, const void *s2, size_t n )` | 比较 `s1` 和 `s2` 所指向对象的前 `n` 个字符。如果 `s1` 分别等于、小于或大于 `s2`，函数返回 0、小于 0 或大于 0 的值。 |
| `void *memchr( const void *s, int c, size_t n )` | 在 `s` 所指向对象的前 `n` 个字符中定位 `c`（转换为 `unsigned char`）首次出现的位置。如果找到 `c`，则返回指向对象中该字符的指针；否则返回 0。 |
| `void *memset( void *s, int c, size_t n )` | 将 `c`（转换为 `unsigned char`）复制到 `s` 所指向对象的前 `n` 个字符中。返回指向结果的指针。 |

图 21.41 | 字符串处理库中的内存函数。

这些函数的指针参数声明为 `void *`。在第 8 章中，我们了解到，任何数据类型的指针都可以直接赋值给 `void *` 类型的指针。因此，这些函数可以接收指向任意数据类型的指针。请记住，`void *` 类型的指针不能直接赋值给任何其他数据类型的指针。由于 `void *` 指针不能被解引用，因此每个函数都接收一个大小参数，用于指定函数要处理的字符（字节）数量。为简单起见，本节中的示例操作字符数组（字符块）。

函数 **`memcpy`** 将指定数量的字符（字节）从其第二个参数所指向的对象复制到其第一个参数所指向的对象中。该函数可以接收指向任意类型对象的指针。如果两个对象在内存中重叠（即属于同一个对象），则该函数的结果未定义。图 21.42 中的程序使用 `memcpy`（第 14 行）将数组 `s2` 中的字符串复制到数组 `s1` 中。

```cpp
// Fig. 21.42: fig21_42.cpp
// Using memcpy.
#include <iostream>
#include <cstring> // memcpy prototype
using namespace std;

int main()
{
   char s1[ 17 ];

   // 17 total characters (includes terminating null)
   char s2[] = "Copy this string";

   memcpy( s1, s2, 17 ); // copy 17 characters from s2 to s1

   cout << "After s2 is copied into s1 with memcpy,\n"
        << "s1 contains \"" << s1 << "\"\n" << endl;
} // end main
```

```text
After s2 is copied into s1 with memcpy,
s1 contains "Copy this string"
```

**图 21.42** | 内存处理函数 `memcpy`。

函数 **`memmove`** 与 `memcpy` 类似，将指定数量的字节从其第二个参数所指向的对象复制到其第一个参数所指向的对象中。复制过程相当于先将字节从第二个参数复制到临时字符数组中，再从临时数组复制到第一个参数中。这使得我们能够将字符串某一部分中的字符复制到同一字符串的另一部分中。

![](img/023f159fdd47d944d48e08843cea732d_932_0.png)

图 21.43 中的程序使用 `memmove`（第 13 行）将数组 `x` 的最后 10 个字节复制到数组 `x` 的前 10 个字节中。

```cpp
// Fig. 21.43: fig21_43.cpp
// Using memmove.
#include <iostream>
#include <cstring> // memmove prototype
using namespace std;
```

**图 21.43** | 内存处理函数 `memmove`。（第 1 部分，共 2 部分。）

