

实际数据。例如，假设标准输入是一个整数文件。我们想要读取并加总所有这些整数，直到到达文件末尾。处理输入文件的正确方法如下所示（使用之前编写的 eat_white 函数）：

```cpp
int sum = 0; // The sum of all the numbers that we read
int next; // The next number that we read

eat_white(); // Skip any whitespace at the front of the file.
while (cin && (cin.peek() != EOF))
{
    cin >> next;
    eat_white();
    sum += next;
}

cout << "The total of all numbers is: " << sum << endl;
```

文件末尾的特殊 EOF 字符可以通过常规 get 函数读取。读取该字符后，成员函数 cin.eof() 将返回 true。

## 写入或读取文本文件

迄今为止，我们已使用标准流 cout 和 cin 演示了输出和输入。程序也可以创建自己的流，将这些流连接到文件。此类程序应同时包含 <iostream> 和 <fstream>，并按以下步骤进行。

### 打开文件。

对于写入，程序应声明 ofstream 类型的变量。对于读取，程序应声明 ifstream 类型的变量。声明变量后，可以使用 open 成员函数将其连接到实际文件，如下所示：

### 打开输出文件：

```cpp
#include <iostream>
#include <fstream>
ofstream outfile;
outfile.open("results");
```

### 打开输入文件：

```cpp
#include <iostream>
#include <fstream>
ifstream infile;
infile.open("data");
```

open 函数的参数是你希望写入的文件名。在我们的输出示例中，此参数是常量字符串 "results"，因此我们将写入名为 results 的文件。我们的输入示例正在从名为 data 的文件中读取文本。open 函数的参数也可以是字符串变量，或任何其他字符串表达式。

### 检查失败。

有时，当你打开文件时，打开操作会失败。例如，如果计算机磁盘已满，打开文件进行写入可能会失败。如果找不到指定文件，打开文件进行输入将失败。如果打开操作失败，则流将被标记为失败。你可以将流的名称用作布尔表达式来测试流是否出错。失败的流会导致表达式为假；仍然正常的设备会导致表达式为真。因此，在打开文件后，你应该检查可能的失败。一种简单的方法是使用 assert 函数（来自 <cassert>），如下所示：

### 检查输出文件是否失败：

```cpp
#include <iostream>
#include <fstream>
#include <cassert>

ofstream outfile;
outfile.open("results");
assert(outfile);
```

### 检查输入文件是否失败：

```cpp
#include <iostream>
#include <fstream>
#include <cassert>

ifstream infile;
infile.open("data");
assert(infile);
```

使用 ofstream 或 ifstream。一旦 ofstream 打开，你可以像使用 cout 一样使用它。例如，使用 outfile（如上所示打开），你可以写入：

```cpp
outfile << "This sentence will be written to the file." << endl;
```

一旦 ifstream 打开，你可以像使用 cin 一样使用它。例如，假设 infile（如上所示打开）包含数字行。你可以读取输入文件中的下一个整数，并将结果存储在整数变量 i 中，如下所示：

```cpp
infile >> i;
```

### 关闭输出文件：

```cpp
#include <iostream>
#include <fstream>
#include <cassert>

ofstream outfile;
outfile.open("results");
assert(outfile);

...Statements that use outfile...

outfile.close();
```

### 关闭输入文件：

```cpp
#include <iostream>
#include <fstream>
#include <cassert>

ifstream infile;
infile.open("data");
assert(infile);

...Statements that use infile...

infile.close();
```

关闭文件会释放文件实现使用的任何资源。如果使用输出缓冲，则关闭输出文件还会刷新输出缓冲区。

## 附录 G 选定的库函数

### <cassert> 设施

<cassert> 中的 assert 设施可以通过编写如下形式的语句来使用：

```cpp
assert(expression);
```

请注意，assert 不是 std 命名空间的一部分（名称只是 assert，而不是 std::assert）。如果表达式为真，则断言不执行任何操作。如果表达式为假，则断言将打印包含表达式文本的错误消息并停止程序。

例如，考虑此断言：

```cpp
assert(i > 0);
```

如果 i 为正，则断言不执行任何操作。如果 i 为非正，则断言将打印诸如“第 42 行断言失败：i > 0”之类的消息。使用此类断言的主要目的是帮助程序员尽早发现错误。

一旦程序不再进行测试，程序员可以通过在每个文件顶部放置以下内容来关闭所有断言：

```cpp
#define NDEBUG
```

### <cctype> 中用于操作字符的函数

```cpp
isalpha(c); // Returns true if c is a letter from 'A' to 'Z' or from 'a' to 'z'.
isalnum(c); // Returns true if c is a letter from 'A' to 'Z' or 'a' to 'z', or a digit from '0' to '9'.
isdigit(c); // Returns true if c is a digit from '0' to '9'.
isspace(c); // Returns true if c is a blank, tab, newline, or carriage return.
tolower(c); // If c is an uppercase letter, then the function returns the equivalent lowercase letter. Otherwise c is returned unchanged.
toupper(c); // If c is a lowercase letter, then the function returns the equivalent uppercase letter. Otherwise c is returned unchanged.
```

### <cstdlib> 中的随机数设施

```cpp
int rand(); // Successive calls to rand() return a sequence of // pseudorandom numbers in the range 0 to RAND_MAX.
void srand(unsigned int seed); // The seed for the pseudorandom number generator // has been set to the specified value.
const int RAND_MAX; // The largest return value from the rand function
```

### <cstdlib> 中的字符串转换

```cpp
int atoi(const char[] s);
// The name stands for "ascii to integer." The parameter s is a null-terminated string. The
// function interprets the string as if it were typed from the keyboard and read into an
// integer. For example, the return value of atoi("42") is the integer 42.
// The function may also be used with a C++ string s, such as atoi(s.c_str());
// In this example, s activates c_str(), which returns an equivalent null-terminated string.
```

```cpp
double atof(const char[] s);
// The name stands for "ascii to float," although the return value is actually a double
// number rather than a float. The parameter s is a null-terminated string. The function
// interprets the string as if it were typed from the keyboard and read into a double
// variable. For example, the return value of atof("42.2") is the double number 42.2.
```

### 标准库排序函数

（详情请参见第 13.4 节）

```cpp
void sort(Iterator begin, Iterator end);
void qsort(
    void* base,
    size_t number_of_elements,
    size_t element_size,
    int compare(const void*, const void*)
);
```

### <cstring> 中用于操作以空字符结尾的字符串的函数

```cpp
char* strcat(char target[], const char source[]);
// A copy of the null-terminated string source is copied to the end of the null-terminated
// string target. The function returns a pointer to the first character of target.
int strcmp(const char s1[], const char s2[]);
// Compares two null-terminated strings. A negative return value indicates s1 < s2; a zero
// return value indicates that s1 == s2; a positive return value indicates s1 > s2.
char* strcpy(char target[], const char source[]);
// Copies the null-terminated string source to the null-terminated string target. The function
// returns a pointer to the first character of target.
size_t strlen(const char s[]);
// The return value is the length of s (a null-terminated string).
char* strchr(const char s[], char c);
// The return value is a pointer to the first occurrence of c in the null-terminated string s (or
// the NULL pointer if c does not appear in s).
int strpos(const char s[], char c);
// The return value is the first index i such that s[i] = c (or -1 if c does not appear in the
// null-terminated string s).
char* strstr(const char s[], const char sub[]);
// Returns a pointer to the first occurrence of the substring sub in the null-terminated
// string s (or the NULL pointer if sub does not appear in s).
```

