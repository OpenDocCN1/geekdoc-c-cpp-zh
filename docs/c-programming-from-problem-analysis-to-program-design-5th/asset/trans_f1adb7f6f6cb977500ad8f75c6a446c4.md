
以下程序演示了 length 函数的用法。

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

    string::size_type len;                                  //Line 8

    cout << "Line 9: str3: " << str3 << endl;               //Line 9
    str3.clear();                                           //Line 10
    cout << "Line 11: After clear, str3: " << str3          //Line 11
         << endl;

    cout << "Line 12: str1.empty(): " << str1.empty()        //Line 12
         << endl;
    cout << "Line 13: str2.empty(): " << str2.empty()        //Line 13
         << endl;

    cout << "Line 14: str4: " << str4 << endl;               //Line 14
    str4.erase(11, 4);                                      //Line 15
    cout << "Line 16: After erase(11, 4), str4: "            //Line 16
         << str4 << endl;

    cout << "Line 17: Length of \"" << firstName << "\" = "  //Line 17
         << static_cast<unsigned int> (firstName.length())
         << endl;
    cout << "Line 18: Length of \"" << name << "\" = "       //Line 18
         << static_cast<unsigned int> (name.length())
         << endl;
    cout << "Line 19: Length of \"" << str1 << "\" = "       //Line 19
         << static_cast<unsigned int> (str1.length())
         << endl;
    cout << "Line 20: Size of \"" << str5 << "\" = "         //Line 20
         << static_cast<unsigned int> (str5.size())
         << endl;

    len = name.length();                                   //Line 21
    cout << "Line 22: len = "                               //Line 22
         << static_cast<unsigned int> (len) << endl;

    return 0;                                               //Line 23
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

该程序的输出不言自明。详细过程留作练习。注意，此程序使用 static cast 运算符输出 length 函数返回的值。这是因为 length 函数返回 string::size_type 类型的值。如果不使用该强制转换运算符，某些编译器可能会给出以下警告消息：

```text
conversion from 'size_t' to 'unsigned int', possible loss of data
```

## 示例 8-15（find 函数）

假设 str1 和 str2 是 string 类型。以下是对 find 函数的有效调用：

```text
str1.find(str2)
str1.find("the")
str1.find('a')
str1.find(str2 + "xyz")
str1.find(str2 + 'b')
```

考虑以下语句：

```text
string sentence = "Outside it is cloudy and warm.";
string str = "cloudy";

string::size_type position;
```

接下来，我们展示 find 函数的效果。

| 语句 | 效果 |
|---|---|
| `cout << sentence.find("is") << endl;` | 输出 11 |
| `cout << sentence.find('s') << endl;` | 输出 3 |
| `cout << sentence.find(str) << endl;` | 输出 14 |
| `cout << sentence.find("the") << endl;` | 输出 string::npos 的值 |
| `cout << sentence.find('i', 6) << endl;` | 输出 8 |
| `position = sentence.find("warm");` | 将 25 赋给 position |

注意，搜索区分大小写。因此，字符串 sentence 中 o（小写 o）的位置是 16。

以下程序运行前面的语句。

```cpp
//Example: find function

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string sentence = "Outside it is cloudy and warm.";  //Line 1
    string str = "cloudy";                               //Line 2

    string::size_type position;                          //Line 3

    cout << "Line 4: sentence = \"" << sentence
         << "\"" << endl;                                //Line 4

    cout << "Line 5: The position of \"is\" in sentence = "
         << static_cast<unsigned int> (sentence.find("is"))
         << endl;                                        //Line 5

    cout << "Line 6: The position of 's' in sentence = "
         << static_cast<unsigned int> (sentence.find('s'))
         << endl;                                        //Line 6

    cout << "Line 7: The position of \"" << str
         << "\" in sentence = "
         << static_cast<unsigned int> (sentence.find(str))
         << endl;                                        //Line 7

    cout << "Line 8: The position of \"the\" in sentence = "
         << static_cast<unsigned int> (sentence.find("the"))
         << endl;                                        //Line 8

    cout << "Line 9: The first occurrence of 'i' in "
         << "sentence \n     after position 6 = "
         << static_cast<unsigned int> (sentence.find('i', 6))
         << endl;                                        //Line 9

    position = sentence.find("warm");                    //Line 10
    cout << "Line 11: " << "Position = "
         << position << endl;                            //Line 11

    return 0;                                            //Line 12
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

该程序的输出不言自明。详细过程留作练习。注意，此程序使用 static cast 运算符输出 find 函数返回的值。这是因为 find 函数返回 string::size_type 类型的值。如果不使用该强制转换运算符，某些编译器可能会给出以下警告消息：

```text
conversion from 'size_t' to 'unsigned int', possible loss of data
```

## 示例 8-16（insert 和 replace 函数）

假设有以下语句：

```text
string firstString = "Cloudy and warm.";
string secondString = "Hello there";
string thirdString = "Henry is taking programming I.";
string str1 = " very ";
string str2 = "Lisa";
```

接下来，我们展示 insert 和 replace 函数的效果。

| 语句 | 效果 |
|---|---|
| `firstString.insert(10, str1);` | `firstString = "Cloudy and very warm."` |
| `secondString.insert(11, 5, '!');` | `secondString = "Hello there!!!!!"` |
| `thirdString.replace(0, 5, str2);` | `thirdString = "Lisa is taking programming I."` |

以下程序运行前面的语句。

```cpp
//Example: insert and replace functions

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string firstString = "Cloudy and warm.";                 //Line 1
    string secondString = "Hello there";                     //Line 2
    string thirdString = "Henry is taking programming I.";   //Line 3
    string str1 = " very ";                                  //Line 4
    string str2 = "Lisa";                                    //Line 5

    cout << "Line 6: firstString = " << firstString
         << endl;                                             //Line 6
    firstString.insert(10, str1);                             //Line 7
    cout << "Line 8: After insert; firstString = "
         << firstString << endl;                              //Line 8

    cout << "Line 9: secondString = " << secondString
         << endl;                                             //Line 9
    secondString.insert(11, 5, '!');                          //Line 10
    cout << "Line 11: After insert; secondString = "
         << secondString << endl;                             //Line 11

    cout << "Line 12: thirdString = " << thirdString
         << endl;                                             //Line 12
    thirdString.replace(0, 5, str2);                          //Line 13
    cout << "Line 14: After replace, thirdString = "
         << thirdString << endl;                              //Line 14

    return 0;                                                  //Line 15
}
```

### 示例运行：

```text
Line 6: firstString = Cloudy and warm.
Line 8: After insert; firstString = Cloudy and very  warm.
Line 9: secondString = Hello there
Line 11: After insert; secondString = Hello there!!!!!
Line 12: thirdString = Henry is taking programming I.
Line 14: After replace, thirdString = Lisa is taking programming I.
```

该程序的输出不言自明。详细过程留作练习。

## 示例 8-17（substr 函数）

考虑以下语句：

```cpp
string sentence;
string str;

sentence = "It is cloudy and warm.";
```

