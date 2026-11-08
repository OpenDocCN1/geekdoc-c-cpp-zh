

## **表7-1** 一些字符串函数（续）

| 表达式 | 作用 |
| --- | --- |
| `strVar.find(str)` | 返回 `str` 在 `strVar` 中首次出现的索引。如果未找到 `str`，则返回特殊值 `string::npos`。 |
| `strVar.find(str, pos)` | 返回 `str` 在 `strVar` 中从 `pos` 处或之后首次出现的索引。 |
| `strVar.find_first_of(str, pos)` | 返回 `strVar` 中 `str` 的任一字符首次出现的索引。搜索从 `pos` 开始。 |
| `strVar.find_first_not_of(str, pos)` | 返回第一个不在 `str` 中的字符的索引。搜索从 `pos` 开始。 |
| `strVar.insert(pos, n, ch);` | 将字符 `ch` 的 `n` 次重复插入到 `strVar` 中索引 `pos` 处；`pos` 和 `n` 是 `string::size_type` 类型；`ch` 是字符。 |
| `strVar.insert(pos, str);` | 将 `str` 的所有字符插入到 `strVar` 中索引 `pos` 处。 |
| `strVar.length()` | 返回 `string::size_type` 类型的值，表示 `strVar` 中字符的数量。 |
| `strVar.replace(pos, n, str);` | 从索引 `pos` 开始，用 `str` 的所有字符替换 `strVar` 中接下来的 `n` 个字符。如果 `n` 大于 `strVar` 的长度，则替换直到 `strVar` 末尾的所有字符。 |
| `strVar.substr(pos, len)` | 返回从 `pos` 开始的 `strVar` 的子字符串。子字符串的长度最多为 `len` 个字符。如果 `len` 过大，则表示 `strVar` 中字符串的“末尾”。 |
| `strVar.size()` | 返回 `string::size_type` 类型的值，表示 `strVar` 中字符的数量。 |
| `strVar.swap(str1);` | 交换 `strVar` 和 `str1` 的内容。`str1` 是字符串变量。 |

接下来，我们展示其中一些函数的使用方法。

### 示例 7-14（clear、empty、erase、length 和 size 函数）

考虑以下语句：

```cpp
string firstName = "Elizabeth";
string name = firstName + " Jones";
string str1 = "It is sunny.";
string str2 = "";
string str3 = "computer science";
string str4 = "C++ programming.";
string str5 = firstName + " is taking " + str4;

string::size_type len;
```

接下来，我们展示 clear、empty、erase、length 和 size 函数的效果。

| 语句 | 效果 |
| --- | --- |
| `str3.clear();` | `str3 = "";` |
| `str1.empty();` | 返回 false； |
| `str2.empty();` | 返回 true； |
| `str4.erase(11, 4);` | `str4 = "C++ program.";` |
| `cout << firstName.length() << endl;` | 输出 9 |
| `cout << name.length() << endl;` | 输出 15 |
| `cout << str1.length() << endl;` | 输出 12 |
| `cout << str5.size() << endl;` | 输出 36 |
| `len = name.length();` | len 的值为 15 |

以下程序演示了 length 函数的使用。

```cpp
//Example: clear, empty, erase, length, and size functions

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string firstName = "Elizabeth";                         //Line 1
    string name = firstName + " Jones";                     //Line 2
    string str1 = "It is sunny.";                           //Line 3
    string str2 = "";                                       //Line 4
    string str3 = "computer science";                       //Line 5
    string str4 = "C++ programming.";                       //Line 6
    string str5 = firstName + " is taking " + str4;         //Line 7

    string::size_type len;                              //Line 8

    cout << "Line 9: str3: " << str3 << endl;          //Line 9
    str3.clear();                                        //Line 10
    cout << "Line 11: After clear, str3: " << str3
         << endl;                                        //Line 11

    cout << "Line 12: str1.empty(): " << str1.empty()
         << endl;                                        //Line 12
    cout << "Line 13: str2.empty(): " << str2.empty()
         << endl;                                        //Line 13

    cout << "Line 14: str4: " << str4 << endl;          //Line 14
    str4.erase(11, 4);                                   //Line 15
    cout << "Line 16: After erase(11, 4), str4: "
         << str4 << endl;                                //Line 16

    cout << "Line 17: Length of \"" << firstName << "\" = "
         << static_cast<unsigned int> (firstName.length())
         << endl;                                        //Line 17
    cout << "Line 18: Length of \"" << name << "\" = "
         << static_cast<unsigned int> (name.length())
         << endl;                                        //Line 18
    cout << "Line 19: Length of \"" << str1 << "\" = "
         << static_cast<unsigned int> (str1.length())
         << endl;                                        //Line 19
    cout << "Line 20: Size of \"" << str5 << "\" = "
         << static_cast<unsigned int> (str5.size())
         << endl;                                        //Line 20

    len = name.length();                                 //Line 21
    cout << "Line 22: len = "
         << static_cast<unsigned int> (len) << endl;     //Line 22

    return 0;                                            //Line 23
}
```

### 示例运行：

```text
Line 9: str3: computer science
Line 11: After clear, str3:
Line 12: str1.empty(): 0
Line 13: str2.empty(): 1
Line 14: str4: C++ programming.
Line 16: After erase(11, 4), str4: C++ program.
Line 17: Length of "Elizabeth" = 9
Line 18: Length of "Elizabeth Jones" = 15
Line 19: Length of "It is sunny." = 12
Line 20: Size of "Elizabeth is taking C++ programming." = 36
Line 22: len = 15
```

该程序的输出不言自明。具体细节留给读者作为练习。请注意，该程序使用 `static_cast` 运算符来输出 `length` 函数返回的值。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_526_0.png)

这是因为 `length` 函数返回的是 `string::size_type` 类型的值。如果没有强制转换运算符，某些编译器可能会给出以下警告信息：

> 从 'size_t' 转换为 'unsigned int'，可能会丢失数据

### 示例 7-15（find 函数）

假设 `str1` 和 `str2` 是 string 类型。以下是对 `find` 函数的有效调用：

```cpp
str1.find(str2)
str1.find("the")
str1.find('a')
str1.find(str2 + "xyz")
str1.find(str2 + 'b')
```

考虑以下语句：

```cpp
string sentence = "Outside it is cloudy and warm.";
string str = "cloudy";

string::size_type position;
```

接下来，我们展示 find 函数的效果。

| 语句 | 效果 |
| --- | --- |
| `cout << sentence.find("is") << endl;` | 输出 11 |
| `cout << sentence.find('s') << endl;` | 输出 3 |
| `cout << sentence.find(str) << endl;` | 输出 14 |
| `cout << sentence.find("the") << endl;` | 输出 `string::npos` 的值 |
| `cout << sentence.find('i', 6) << endl;` | 输出 8 |
| `position = sentence.find("warm");` | 将 25 赋给 position |

请注意，搜索区分大小写。因此，在字符串 sentence 中，字符 o（小写 o）的位置是 16。

以下程序对上述语句进行验证。

```cpp
//Example: find function

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string sentence = "Outside it is cloudy and warm.";        //Line 1
    string str = "cloudy";                                  //Line 2

    string::size_type position;                              //Line 3

    cout << "Line 4: sentence = \"" << sentence
         << "\n" << endl;                                   //Line 4

    cout << "Line 5: The position of \"is\" in sentence = "
         << static_cast<unsigned int> (sentence.find("is"))
         << endl;                                             //Line 5

    cout << "Line 6: The position of 's' in sentence = "
         << static_cast<unsigned int> (sentence.find('s'))
         << endl;                                             //Line 6

    cout << "Line 7: The position of \"" << str
         << "\" in sentence = "
         << static_cast<unsigned int> (sentence.find(str))
         << endl;                                             //Line 7

    cout << "Line 8: The position of \"the\" in sentence = "
         << static_cast<unsigned int> (sentence.find("the"))
         << endl;                                             //Line 8

    cout << "Line 9: The first occurrence of \'i\' in "
         << "sentence \n        after position 6 = "
         << static_cast<unsigned int> (sentence.find('i', 6))
         << endl;                                             //Line 9

    position = sentence.find("warm");                         //Line 10
    cout << "Line 11: Position = "
         << position << endl;                                 //Line 11

    return 0;                                                 //Line 12
}
```

### 示例运行：

```text
Line 4: sentence = "Outside it is cloudy and warm."
Line 5: The position of "is" in sentence = 11
Line 6: The position of 's' in sentence = 3
Line 7: The position of "cloudy" in sentence = 14
Line 8: The position of "the" in sentence = 4294967295
Line 9: The first occurrence of 'i' in sentence
         after position 6 = 8
Line 11: Position = 25
```

