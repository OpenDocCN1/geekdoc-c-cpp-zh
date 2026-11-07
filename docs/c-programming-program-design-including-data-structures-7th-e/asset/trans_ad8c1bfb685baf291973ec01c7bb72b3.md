

```cpp
string::size_type len;                                      //Line 8

cout << "Line 9: str3: " << str3 << endl;                 //Line 9
str3.clear();                                               //Line 10
cout << "Line 11: After clear, str3: " << str3             //Line 11
     << endl;

cout << "Line 12: str1.empty(): " << str1.empty()          //Line 12
     << endl;
cout << "Line 13: str2.empty(): " << str2.empty()          //Line 13
     << endl;

cout << "Line 14: str4: " << str4 << endl;                 //Line 14
str4.erase(11, 4);                                          //Line 15
cout << "Line 16: After erase(11, 4), str4: "              //Line 16
     << str4 << endl;

cout << "Line 17: Length of \"" << firstName << "\" = "  
     << static_cast<unsigned int> (firstName.length())
     << endl;                                               //Line 17
cout << "Line 18: Length of \"" << name << "\" = "       
     << static_cast<unsigned int> (name.length())
     << endl;                                               //Line 18
cout << "Line 19: Length of \"" << str1 << "\" = "       
     << static_cast<unsigned int> (str1.length())
     << endl;                                               //Line 19
cout << "Line 20: Size of \"" << str5 << "\" = "         
     << static_cast<unsigned int> (str5.size())
     << endl;                                               //Line 20

len = name.length();                                        //Line 21
cout << "Line 22: len = "
     << static_cast<unsigned int> (len) << endl;            //Line 22

return 0;                                                   //Line 23
}
```

### 示例运行

```
Line 9: str3: computer science
Line 11: After clear, str3:
Line 12: str1.empty(): 0
Line 13: str2.empty(): 0
Line 14: str4: C++ programming.
Line 16: After erase(11, 4), str4: C++ program.
Line 17: Length of "Elizabeth" = 9
Line 18: Length of "Elizabeth Jones" = 15
Line 19: Length of "It is sunny." = 12
Line 20: Size of "Elizabeth is taking C++ programming." = 36
Line 22: len = 15
```

该程序的输出不言自明。详细内容留作练习。请注意，该程序使用静态转换运算符来输出 `length` 函数返回的值。这是因为 `length` 函数返回的是 `string::size_type` 类型的值。如果没有转换运算符，某些编译器可能会给出以下警告信息：

```
conversion from 'size_t' to 'unsigned int', possible loss of data
```

## 示例 7-15（find 函数）

假设 `str1` 和 `str2` 是 `string` 类型。以下是对 find 函数的有效调用：

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
|---|---|
| `cout << sentence.find("is") << endl;` | 输出 11 |
| `cout << sentence.find('s') << endl;` | 输出 3 |
| `cout << sentence.find(str) << endl;` | 输出 14 |
| `cout << sentence.find("the") << endl;` | 输出 `string::npos` 的值 |
| `cout << sentence.find('i', 6) << endl;` | 输出 8 |
| `position = sentence.find("warm");` | 将 25 赋给 position |

请注意，搜索是区分大小写的。因此，字符串 sentence 中 o（小写 o）的位置是 16。

下面的程序对上述语句进行了验证。

```cpp
//Example: find function

#include <iostream>
#include <string>

using namespace std;
```

该程序的输出不言自明。详细内容留作练习。请注意，该程序使用静态转换运算符来输出 `find` 函数返回的值。这是因为 `find` 函数返回的是 `string::size_type` 类型的值。如果没有转换运算符，某些编译器可能会给出以下警告信息：

```
conversion from 'size_t' to 'unsigned int', possible loss of data
```

## 示例 7-16（insert 和 replace 函数）

假设有以下语句：

```cpp
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

下面的程序对上述语句进行了验证。

```cpp
//Example: insert and replace functions
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string firstString = "Cloudy and warm.";                  //Line 1
    string secondString = "Hello there";                      //Line 2
    string thirdString = "Henry is taking programming I.";    //Line 3
    string str1 = " very ";                                      //Line 4
    string str2 = "Lisa";                                         //Line 5

    cout << "Line 6: firstString = " << firstString               //Line 6
         << endl;
    firstString.insert(10, str1);                                  //Line 7
    cout << "Line 8: After insert; firstString = "                //Line 8
         << firstString << endl;

    cout << "Line 9: secondString = " << secondString              //Line 9
         << endl;
    secondString.insert(11, 5, '!');                               //Line 10
    cout << "Line 11: After insert; secondString = "               //Line 11
         << secondString << endl;

    cout << "Line 12: thirdString = " << thirdString               //Line 12
         << endl;
    thirdString.replace(0, 5, str2);                               //Line 13
    cout << "Line 14: After replace, thirdString = "               //Line 14
         << thirdString << endl;

    return 0;                                                       //Line 15
}
```

### 示例运行

```
Line 6: firstString = Cloudy and warm.
Line 8: After insert; firstString = Cloudy and very warm.
Line 9: secondString = Hello there
Line 11: After insert; secondString = Hello there!!!!!
Line 12: thirdString = Henry is taking programming I.
Line 14: After replace, thirdString = Lisa is taking programming I.
```

该程序的输出不言自明。详细内容留作练习。

## 示例 7-17（substr 函数）

考虑以下语句：

```cpp
string sentence;
string str;

sentence = "It is cloudy and warm.";
```

接下来，我们展示 substr 函数的效果。

| 语句 | 效果 |
|---|---|
| cout << sentence.substr(0, 5) << endl; | 输出：It is |
| cout << sentence.substr(6, 6) << endl; | 输出：cloudy |
| cout << sentence.substr(6, 16) << endl; | 输出：cloudy and warm. |
| cout << sentence.substr(17, 10) << endl; | 输出：warm. |
| cout << sentence.substr(3, 6) << endl; | 输出：is clo |
| str = sentence.substr(0, 8); | str = "It is cl" |
| str = sentence.substr(2, 10); | str = " is cloudy" |

下面的程序演示了如何使用字符串函数 substr。

```cpp
//Example: substr function

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string sentence;                        //Line 1
    string str;                              //Line 2

    sentence = "It is cloudy and warm.";     //Line 3

    cout << "Line 4: substr(0, 5) in \"" 
         << sentence << "\" = \"" 
         << sentence.substr(0, 5) << "\"" << endl;  //Line 4

    cout << "Line 5: substr(6, 6) in \"" 
         << sentence << "\" = \"" 
         << sentence.substr(6, 6) << "\"" << endl;  //Line 5

    cout << "Line 6: substr(6, 16) in \"" 
         << sentence << "\" = " << endl
         << "    \"" << sentence.substr(6, 16) 
         << "\"" << endl;                         //Line 6

    cout << "Line 7: substr(17, 10) in \"" 
         << sentence << "\" = \"" 
         << sentence.substr(17, 10) << "\"" << endl; //Line 7

    cout << "Line 8: substr(3, 6) in \"" 
         << sentence << "\" = \"" 
         << sentence.substr(3, 6) << "\"" << endl;  //Line 8
}
```

