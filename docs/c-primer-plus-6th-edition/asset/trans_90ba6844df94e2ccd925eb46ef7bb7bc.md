

# 第4章 复合类型

## 列表 4.7 strtype1.cpp

```
// strtype1.cpp -- using the C++ string class
#include <iostream>
#include <string> // make string class available
int main()
{
    using namespace std;
    char char1[20]; // create an empty array
    char char2[20] = "jaguar"; // create an initialized array
    string str1; // create an empty string object
    string str2 = "panther"; // create an initialized string

    cout << "Enter a kind of feline: ";
    cin >> str1;
    cout << "Enter another kind of feline: ";
    cin >> str2; // use cin for input
    cout << "Here are some felines:\n";
    cout << char1 << " " << char2 << " "
         << str1 << " " << str2 << " use cout for output\n";
    cout << endl;
    cout << "The third letter in " << char2 << " is ";
    cout << char2[2] << endl;
    cout << "The third letter in " << str2 << " is ";
    cout << str2[2] << endl; // use array notation

    return 0;
}
```

以下是列表 4.7 程序的示例运行：

Enter a kind of feline: ocelot
Enter another kind of feline: tiger
Here are some felines:
ocelot jaguar tiger panther
The third letter in jaguar is g
The third letter in panther is n

- 你可以将字符串对象初始化为 C 风格字符串。
- 你可以使用 cin 将输入存储到字符串对象中。
- 你可以使用 cout 显示字符串对象。
- 你可以使用数组表示法访问字符串对象中存储的单个字符。

## 介绍 string 类

string 对象与列表 4.7 中显示的字符数组之间的主要区别在于，你将 string 对象声明为简单变量，而不是数组：

```
string str1; // create an empty string object
string str2 = "panther"; // create an initialized string
```

类设计允许程序自动处理大小调整。例如，str1 的声明创建了一个长度为零的字符串对象，但程序在读取 str1 时会自动调整 str1 的大小：

```
cin >> str1; // str1 resized to fit input
```

这使得使用 string 对象比使用数组更方便、更安全。从概念上讲，人们把数组看作是用于存储字符串的 char 存储单元的集合，而把 string 类看作是代表字符串的单一实体。

## C++11 字符串初始化

正如你现在可能预料的那样，C++11 允许对 C 风格字符串和 string 对象进行列表初始化：

```
char first_date[] = {"The Chadon Dudu"};
char second_date[] = {"The Elephant Plate"};
string third_date = {"The Bread Bowl"};
string fourth_date = {"Hank's Fine Eats"};
```

## 赋值、连接和追加

string 类使某些操作比数组的情况更简单。例如，你不能简单地将一个数组赋给另一个数组。但你可以将一个 string 对象赋给另一个：

```
char char1[20]; // create an empty array
char char2[20] = "jaguar"; // create an initialized array
string str1; // create an empty string object
string str2 = "panther"; // create an initialized string
char1 = char2; // INVALID, no array assignment
str1 = str2; // VALID, object assignment ok
```

该类简化了字符串的组合。你可以使用 + 运算符将两个 string 对象相加，并使用 += 运算符将一个字符串添加到现有字符串的末尾。继续使用前面的代码，我们有以下可能性：

```
string str3;
str3 = str1 + str2; // assign str3 the joined strings
str1 += str2; // add str2 to the end of str1
```

列表 4.8 说明了这些用法。请注意，你可以向 string 对象添加 C 风格字符串以及 string 对象。

## 134 第4章 复合类型

### 列表 4.8 strtype2.cpp

```
// strtype2.cpp -- assigning, adding, and appending
#include <iostream>
#include <string> // make string class available
int main() {
    using namespace std;
    string s1 = "penguin";
    string s2, s3;

    cout << "You can assign one string to another: " << s2 = s1 << "\n";
    s2 = s1;
    cout << "s1: " << s1 << " " << s2 << endl;
    cout << "You can assign a C-style string to a string object.\n";
    cout << "s2 = \"buzzard\"\n";
    s2 = "buzzard";
    cout << "s2: " << s2 << endl;
    cout << "You can concatenate strings: " << s3 = s1 + s2 << "\n";
    s3 = s1 + s2;
    cout << "s3: " << s3 << endl;
    cout << "You can append strings.\n";
    s1 += s2;
    cout << "s1 += s2 yields s1 = " << s1 << endl;
    s2 += " for a day\n";
    cout << "s2 += \" for a day\" yields s2 = " << s2 << endl;

    return 0;
}
```

请记住转义序列 \" 表示用作字面字符的双引号，而不是标记字符串的界限。以下是列表 4.8 程序的输出：

You can assign one string to another: s2 = s1
s1: penguin, s2: penguin
You can assign a C-style string to a string object.
s2 = "buzzard"
s2: "buzzard"
You can concatenate strings: s3 = s1 + s2
s3: penguinbuzzard
You can append strings.
s1 += s2 yields s1 = penguinbuzzard
s2 += "" for a day" yields s2 = buzzard for a day

## 更多 string 类操作

即使在 string 类被添加到 C++ 之前，程序员也需要做诸如分配字符串之类的事情。对于 C 风格字符串，他们使用 C 库中的函数来完成这些任务。cstring 头文件（以前是 string.h）支持这些函数。例如，你可以使用 strcpy() 函数将字符串复制到字符数组，并使用 strcat() 函数将字符串追加到字符数组：

```
strcpy(char1, char2); // copy char2 to char1
strcat(char1, char2); // append contents of char2 to char1
```

列表 4.9 比较了使用 string 对象和字符数组的技术。

### 列表 4.9 strtype3.cpp

```
// strtype3.cpp -- more string class features
#include <iostream>
#include <string>                // make string class available
#include <cstring>               // C-style string library
int main()
{
    using namespace std;
    char char1[20];
    char char2[20] = "jaguar";
    string str1;
    string str2 = "panther";

    // assignment for string objects and character arrays
    str1 = str2;                    // copy str2 to str1
    strcpy(char1, char2);           // copy char2 to char1

    // appending for string objects and character arrays
    str1 += "paste";               // add paste to end of str1
    strcat(char1, "juice");        // add juice to end of char1

    // finding the length of a string object and a C-style string
    int len1 = str1.size();        // obtain length of str1
    int len2 = strlen(char1);      // obtain length of char1

    cout << "The string " << str1 << " contains "
         << len1 << " characters.\n";
    cout << "The string " << char1 << " contains "
         << len2 << " characters.\n";

    return 0;
}
```

## 第4章 复合类型

以下是输出：

The string panther paste contains 13 characters.
The string jaguar juice contains 12 characters.

使用 string 对象的语法往往比 C 字符串函数更简单。这对于更复杂的操作尤其如此。例如，C 库中 `str3 = str1 + str2;` 的等价物是：

```
strcpy(char3, char1);
strcat(char3, char2);
```

此外，使用数组时，始终存在数组太小而无法容纳信息的危险，如以下示例所示：

```
char site[10] = "house";
strcat(site, "pancakes"); // memory problem
```

strcat() 函数将尝试将所有 12 个字符复制到 site 数组中，从而溢出相邻内存。这可能会导致程序中止，或在数据损坏的情况下继续运行。string 类通过根据需要自动调整大小来避免此类问题。C 库提供了 strcpy() 和 strcat() 的近亲，称为 strncpy() 和 strncat()，它们通过采用第三个参数来指示目标数组的最大允许大小而更安全，但使用它们会在编写程序时增加另一层复杂性。

注意字符串中字符数量的差异：

```
int len1 = str1.size(); // length of str
int len2 = strlen(char1); // length of char
```

strlen() 函数是一个常规函数，它以 C 风格字符串作为参数并返回字符串中的字符数。size() 函数基本上做同样的事情，但对于字符串来说是不同的。不是传递参数，str1 位于函数名称之前并通过点与之连接。正如你在第 3 章中看到的 put() 方法，这种语法表示 str1 是一个对象，size() 是一个类方法。方法只能由属于与该方法相同类的对象调用。在这种特定情况下，str1 是一个 string 对象，size() 是一个 string 方法。简而言之，C 函数使用函数参数来标识要使用的字符串，而 C++ string 对象使用对象名称和点运算符来指示要使用的字符串。

## 更多关于 string 类 I/O 的内容

正如你所见，你可以使用 cin 和 >> 运算符读取 string 对象，并使用 cout 和 << 运算符显示 string 对象，使用与使用

