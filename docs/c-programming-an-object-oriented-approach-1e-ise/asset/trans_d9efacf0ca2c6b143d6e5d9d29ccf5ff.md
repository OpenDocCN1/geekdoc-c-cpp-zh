

### 程序 10.5 访问 C 字符串中的字符（续）

```cpp
// Creation of two C-strings
const char* str1 = "Hello my friends.";
char str2[] = "This is the second string.";
// Retrieving character at a given position
cout << "Character at index 6 in str1: " << str1[6] << endl;
// Changing character at a given position
str2[0] = 't';
cout << "str2 after change: " << str2;
return 0;
}
```

**运行：**
```text
Character at index 6 in str1: m
str2 after change: this is the second string.
```

## 搜索字符

我们可以搜索字符串以查找某个字符。搜索可以返回第一次出现该字符的位置的指针（正向搜索），也可以返回最后一次出现该字符的位置的指针（反向搜索）。前一种搜索使用 `strchr` 函数，后一种使用 `strrchr` 函数。设置好指向该字符的指针后，如果字符串不是常量，就可以使用该指针修改字符。如果找不到该字符，则返回空指针。

```cpp
char* ptr = strchr (str, 'c');       // Forward search
char* ptr = strrchr (str, 'c');      // Backward search
```

> 我们可以使用 strchr (...) 和 strrchr (...) 成员函数来创建指向某个字符的指针。

### 示例 10.7

程序 10.6 展示了如何搜索字符。

### 程序 10.6 查找子字符串的起始位置

```cpp
/*************************************************************
 * A program to search for a given character using forward
 * search to find the first occurrence or backward search to
 * find the last occurrence
 *************************************************************/
#include <cstring>
#include <iostream>
using namespace std;

int main()
{
    // Declaration of a string
    char str[ ] = "Hello friends.";
    // Capitalizing the first occurrence of character e
    char* cPtr = strchr (str, 'e');
    *cPtr = 'E';
    cout << "str after first change: " << str << endl;
    // Capitalizing the last occurrence of character e
    cPtr = strrchr (str, 'e');
    *cPtr = 'E';
    cout << "str after last change: " << str << endl;
    return 0;
}
```

**运行：**
```text
str after first change: HEllo friends.
str after last change: HEllo friEnds.
```

## 搜索子字符串

我们可以使用 *strstr* 函数搜索字符串，以查找子字符串的位置。该函数返回指向子字符串中第一个字符的指针。如果在字符串中找不到该子字符串，则返回空指针。

```cpp
char* ptr = strstr (str, substr);        // Searching for a substring
```

### 示例 10.8

程序 10.7 展示了如何查找子字符串。

### 程序 10.7 查找子字符串

```cpp
/************************************************************
 * The program shows how to use the strstr member function to
 * find the occurrence of a substring in a string.
 ************************************************************/
#include <cstring>
#include <iostream>
using namespace std;

int main ( )
{
    // Creating a string
    char str[ ] = "Hello friends of mine.";
    // Finding the location of the substring
    char* sPtr = strstr (str, "friends");
    cout << "The substring starts at index: " << sPtr - str;
    return 0;
}
```

**运行：**
```text
The substring starts at index: 6
```

## 搜索字符集中的任意字符

有时，我们需要搜索字符串，以查找字符集所定义的任意字符的位置。换句话说，我们不是要查找字符串中特定字符的位置，而是要查找字符集中任意字符第一次出现的位置。本章稍后将介绍，这种操作用于对字符串进行标记化处理。该字符集也定义为一个字符串。`strpbrk` 函数用于此目的。如果找不到任何字符，则返回空指针。

```cpp
char* p = strpbrk (str, set);             // Searching for character in a set
```

> 成员函数 strpbrk (...) 允许我们查找字符集中任意字符第一次出现的位置。

### 示例 10.9

程序 10.8 展示了如何使用 `strpbrk (...)` 函数。

### 程序 10.8 搜索字符集中的字符

```cpp
/***************************************************************
 * The program shows how we can use the strpbrk function to
 * find the location of any character in a set of characters.
 ***************************************************************/
#include <cstring>
#include <iostream>
using namespace std;

int main ()
{
    // Creation of a string
    char str[ ] = "Hello friends of mine.";
    // Finding the first occurrence of any character in a set
    char* pPtr = strpbrk (str, "pfmd");
    cout << "The character " << *pPtr << " was found." << endl;
    cout << "It is at index: " << pPtr - str;
    return 0;
}
```

**运行：**
```text
The character f was found.
It is at index: 6
```

## 比较

我们可以使用 `strcmp` 和 `strncmp` 函数比较两个字符串。前者比较两个完整的字符串；后者只比较两个字符串的前 *n* 个字符。比较会逐字符进行，直到遇到不同的字符为止（注意，空字符也会参与比较）。当找到不相等的字符时，比较停止。如果第一个字符串中的字符小于第二个字符串中的字符，函数返回负数；如果第一个字符串中的字符大于第二个字符串中的字符，则返回正整数。如果没有找到不同的字符，函数返回 0。

```cpp
int value = strcmp(str1, str2);        // Comparing str1 with the whole str2
int value = strncmp(str1, str2, n);     // Comparing str1 with the first n characters of str2
```

> 可以使用 `strcmp (...)` 和 `strncmp (...)` 成员函数比较两个字符串。

### 示例 10.10

程序 10.9 使用了这两个函数。请注意，比较函数不会修改两个字符串中的任何一个。

### 程序 10.9 比较 C 字符串

```cpp
/*******************************************************
 * The program shows how we can compare two strings using the
 * strcmp and strncmp functions.
 *******************************************************/
#include <cstring>
#include <iostream>
using namespace std;

int main( )
{
    // Declaration of two C-strings
    const char* str1 = "Hello Alice.";
    const char* str2 = "Hello John.";
    const char* str3 = "Hello Betsy.";
    // Comparison uses the whole length
    cout << "Comparing str1 and str2: ";
    cout << strcmp (str1, str2) << endl;
    cout << "Comparing str2 and str3: ";
    cout << strcmp (str2, str3) << endl;
    // Comparison using one of the first characters
    cout << "Comparing first 5 characters of str1 and str2: ";
    cout << strncmp (str1, str2, 5);
    return 0;
}
```

**运行：**
```text
Comparing str1 and str2: -1
Comparing str2 and str3: 1
Comparing first 5 characters of str1 and str2: 0
```

## 连接（追加）

我们可以将一个字符串添加到另一个字符串的末尾。在这种情况下，目标字符串会发生变化，而源字符串保持不变。库为此定义了两个成员函数：*strcat* 和 *strncat* 函数。前一个函数将 *str2* 中的所有字符连接到 *str1* 的末尾。后一个函数只将第二个字符串的前 *n* 个字符连接到第一个字符串的末尾。但是，我们必须确保为 *str1* 分配了足够的内存来容纳连接后的字符串（程序 10.10）。

```cpp
strcat(str1, str2);      // Appending the whole str2 to str1
strncat(str1, str2, n);  // Appending the first n characters of str2 to str1
```

> 可以使用成员函数 *strcat* (...) 和 *strncat* (...) 将一个字符串连接到另一个字符串的末尾。

### 示例 10.11

程序 10.10 使用了两个与字符串连接相关的成员函数。

### 程序 10.10 使用 strcat 和 strncat

```cpp
/**************************************************************
 * We use strcat and strncat to concatenate a string at the
 * end of another string.
 **************************************************************/
#include <cstring>
#include <iostream>
using namespace std;

int main( )
{
    // Using strcat function
    char str1[20] = "This is ";
    const char* str2 = "a string.";
    strcat(str1, str2);
    cout << "str1: " << str1 << endl;
    // Using strncat function
```

