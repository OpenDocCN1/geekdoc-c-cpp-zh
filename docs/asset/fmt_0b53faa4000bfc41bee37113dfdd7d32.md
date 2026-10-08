
## 示例 10.4

程序 10.3 在 `str4` 的字面量字符串中包含一个空字符，仅是为了说明该字面量是由空字符终止的，其余字符不是字面量字符串的一部分（第 15 行）。换句话说，字符串有 8 个字符，而不是 19 个。我们输入了 `str5` 的字符，但请注意只有第一个单词存储在字符串中；其余部分被忽略了，因为提取运算符在第一个空白字符处停止。

### 程序 10.2 查找两个字符串的长度

```
*****************************************************
* 程序展示了如何获取 C 字符串的长度，即 *
* 是空字符之后的字符数量 *
*****************************************************/
5 #include <string>
6 #include <iostream>
7 using namespace std;
9 int main () {
10 // 四个字符串的声明与定义
11 const char* str1 = "Hello my friends";
12 char str2[] = {'H', 'e', 'l', 'l', 'o', '\0'};
14 // 查找并打印每个字符串的长度
15 cout << "Length of str1: " << strlen(str1) << endl;
16 cout << "Length of str2: " << strlen(str2) << endl;
18 return 0;
运行结果:
Length of str1: 17
Length of str2: 5
```

### 程序 10.3 使用 C 字符串

```
**************************************************************
2 * 程序展示了如何创建 C 字符串并对它们使用输入和
3 * 输出操作。
4 ***************************************************************
5 #include<iostream>
6 using namespace std;
7 int main ()
8 {
9 // 创建一个常量非常量字符串。
10 char str1[] = {'H', 'e', 'l', 'l', '\0'};
11 const char str2[] = {'H', 'e', 'l', 'l', '\0'};
12 // 创建两个常量字符串类型并使用字符串字面量。
13 const char *str3 = "Goodbye";
14 const char *str4 = "Goodbye my friend";
15 // 打印四个字符串
16 cout << "str1: " << str1 << endl;
17 cout << "str2: " << str2 << endl;
18 cout << "str3: " << str3 << endl;
19 cout << "str4: " << str4 << endl;
20 // 创建并输入第五个字符串。
21 char str5[20];
22 cout << "The characters for str5: ";
23 cin >> str5;
24 cout << "str5: " << str5;
```

### 程序 10.3 使用 C 字符串（继续）

```cpp
26 return 0;
27 }
```

运行结果:
str1: Hello
str2: Hello
str3: Goodbye
str4: Goodbye
Enter the characters for str5: This is the one.
str5: This

### getline 函数

为了读取包含空白字符的行字符，我们必须为此目的使用 `getline()` 函数。`getline()` 函数是 `istream` 类的成员，这意味着我们必须有一个输入对象（键盘或文件）。`getline()` 函数读取字符直到遇到换行符为止，并在末尾添加空字符。

### 示例 10.5

程序 10.4 展示了如何读取带空格的字符串。

```cpp
*************************************
* 程序展示了如何使用 getline() 读取 *
* 带空格的字符串。*
*************************************/
5 #include <iostream>
6 #include <string>
7 using namespace std;
8 int main () {
9 {
10 char str[100];
11 cout << "Enter a string: ";
12 getline(cin, str);
13 cout << "You entered: " << str;
14 return 0;
15 }
```

### 访问字符

下一个讨论的操作是如何访问字符串中的任何字符。如果我们知道位置，可以使用下标运算符来访问字符。如果字符串是常量，则意味着检索；如果是非常量，则意味着修改。

```cpp
char c = str[i]; // 字符串是常量
str[i] = c; // 字符串是非常量
```

### 示例 10.6

程序 10.5 展示了如何在常量和非常量字符串中访问字符。

```cpp
*************************************
* 程序展示了如何在常量和非常量 *
* 字符串中访问字符。*
*************************************/
5 #include <cstring>
6 #include <iostream>
7 using namespace std;
8 int main () {
9 {
10 const char* str1 = "Hello my friends.";
11 char str2[] = "This is the second string";
12 // 获取指定位置的字符
13 cout << "Character at index 6 in str1: " << str1[6] << endl;
14 // 修改指定位置的字符
15 str2[0] = 't';
16 cout << "str2 after change: " << str2;
17 return 0;
18 }
```

### 查找字符

我们可以使用搜索来查找字符。搜索可以返回第一次出现（正向搜索）或最后一次出现（反向搜索）的指针。第一次搜索使用 `strchr` 函数；第二次使用 `strrch` 函数。设置指针后，如果字符串不是常量，我们可以使用它修改字符。如果找不到字符，则返回空指针。

```cpp
char* ptr = strchr(str, 'c'); // 正向搜索
char* ptr = strrch(str, 'c'); // 反向搜索
```

## 示例 10.7

程序 10.6 展示了如何查找字符。

```cpp
**************************************************************
* 程序使用正向搜索查找第一次出现或反向搜索 *
* 查找最后一次出现，以查找给定的 *
* 字符*
***************************************************************
5 #include <iostream>
6 #include <cstring>
7 using namespace std;
8 int main () {
9 {
10 char str[] = "The quick brown fox jumps over the lazy dog";
11 char c = 'o';
12 char* ptr = strchr(str, c);
13 if (ptr) cout << "First 'o' at index: " << (ptr - str) << endl;
14 ptr = strrch(str, c);
15 if (ptr) cout << "Last 'o' at index: " << (ptr - str) << endl;
16 return 0;
17 }
```

# 程序 10.6 查找字符串的子串（续）

```cpp
12 // 字符串声明
13 char str [] = "Hello friends.";
14 // 将第一次出现的的字符大写
15 char *pPtr = strchr(str, 'e');
16 *pPtr = 'E';
17 cout << "str after first change: " << str << endl;
18 // 将最后一次出现的字符大写
19 pPtr = strchr(str, 'e');
20 *pPtr = 'E';
21 cout << "str after last change: " << str << endl;
22 return 0;
```

运行：
str after first change: Hello friends.
str after last change: HEllo friends.

# 查找子串

我们可以使用 `strstr` 函数搜索字符串以找到子串的位置。该函数返回指向字符串中第一个字符的指针。如果从字符串中找不到该子串，则返回一个空指针。

```cpp
char* ptr = strstr(str, substr); // 查找子串
```

# 示例 10.8

程序 10.7 展示了如何查找子串。

# 程序 10.7 查找子串

```cpp
1 ********************************************************
2 * 该程序展示了如何使用 strstr 成员函数
3 * 查找字符串中子串的出现位置。
4 ***************************************/
5 #include <cstring>
6 #include <iostream>
7 using namespace std;
9 int main ()
10 {
11 // 创建一个字符串
12 char str [] = "Hello friends of mine.";
13 // 查找子串的位置
14 char *sPtr = strstr(str, "friends");
15 cout << "The substring starts at index: " << sPtr - str;
```

（续）

# 程序 10.7 查找子串（续）

```cpp
16 return 0;
17 }
```
运行：The substring starts at index: 6

# 查找集合中的任意字符

有时，我们需要搜索字符串以找到字符集中定义的任意一个字符的位置。换句话说，我们并不是想找到字符串中指定字符的位置，而是想找到集合中任意字符的首次出现的位置。在本章的后面，我们将学习到这种操作用于对字符串进行分词（tokenize）。该集合也被定义为字符串。`strbrk` 函数专门用于此目的。如果没有找到任何字符，则返回空指针。

```cpp
char* p = strbrk(str, set); // 在集合中查找字符
```

> 成员函数 `strbrk(...)` 允许我们找到字符集中任意字符首次出现的位置。

# 示例 10.9

程序 10.8 展示了如何使用 `strbrk(...)` 函数。

# 程序 10.8 在集合中查找字符

```cpp
****************************************************
1 * 该程序展示了我们如何使用 strbrk 函数来*
2 * 查找字符集中任意字符的位置。
3 *****************************************************/
4 #include <string>
5 #include <iostream>
6 using namespace std;
8 int main () {
9 // 创建字符串
10 char str [] = "Hello friends of mine.";
11 // 查找集合中任意字符的首次出现
12 char* pPtr = strbrk(str, "fnd");
13 cout << "The character " << pPtr << " was found." << endl;
14 cout << "It is at index: " << pPtr - str;
15 return 0;
16 }
```

运行：
The character f was found.
It is at index: 6

# 第 10 章字符串

# 比较

我们使用 `strcmp` 和 `strncmp` 函数来比较两个字符串。第一个比较比较两个字符串；第二个只比较两个字符串的前 `n` 个字符。比较通过逐个字符进行，直到遇到不相同的字符为止（注意比较过程中也会使用空字符）。当发现不相等的字符时，比较停止；如果第一个字符串中的字符小于第二个，则返回一个负数；如果第一个字符串中的字符大于第二个，则返回一个正整数。如果没有找到不同的字符，函数返回 0。

```cpp
int value = strcmp(str1, str2); // 将 str1 与整个 str2比较
int value = strncmp(str1, str2, n); // 将 str1 与 str2 的前 n 个字符比较
```

> 两个字符串可以使用 `strcmp(...)` 和 `strncmp(...)` 成员函数进行比较。

示例 10.10
程序 10.9 使用这两个函数。注意，比较函数不会修改这两个字符串中的任何一个。

# 程序 10.9 比较 C 字符串

```cpp
 * 该程序展示了我们如何使用 strcmp 和 strncmp 
 * 函数来比较两个字符串。
 *****************************************************/
#include <cstring>
#include <iostream>
using namespace std;
int main ( )
{
    // 声明两个 C 字符串
    const char *str1 = "Hello Alice.";
    const char *str2 = "Hello John.";
    const char *str3 = "Hello Betsy.";
    // 使用全长度进行比较
    cout << "Comparing str1 and str2:" << endl;
    cout << strcmp(str1, str2) << endl;
    cout << strcmp(str2, str3) << endl;
    cout << strcmp(str2, str3) << endl;
    // 使用前几个字符进行比较
    cout << "Comparing first 5 characters of str1 and str2:" << endl;
    cout << strncmp(str1, str2, 5) << endl;
23 return 0;
24 }
```

运行：
Comparing str1 and str2:-1
Comparing str2 and str3: 1
Comparing first 5 characters of str1 and str2: 0

# 拼接（追加）

我们可以在另一个字符串的末尾添加一个字符串。在这种情况下，目标字符串会被改变，但源字符串保持不变。库为此目的定义了两个成员函数：`strcat` 和 `strnc`。第一个函数将 `str2` 中的所有内容连接到 `str1` 的末尾。第二个函数将第二个字符串的前 `n` 个字符连接到第一个字符串的末尾。然而，我们必须确保 `str1` 有足够的内存来接受拼接。

# 程序 10.10 使用 strcat

```cpp
************************************************
* 该程序展示了我们如何使用 strcat 函数
* 拼接字符串。
**********************************
#include <cstring>
#include <iostream>
using namespace std;
int main() {
    // (此处代码省略，根据原文逻辑)
}
```
