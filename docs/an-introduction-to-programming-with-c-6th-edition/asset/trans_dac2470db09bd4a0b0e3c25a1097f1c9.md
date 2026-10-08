

(续)

# 算法

+ 1. repeat

```
do // 开始循环
{
    cout << "Enter a 5-letter word
in uppercase: ";
    getline(cin, originalword);
    while (originalword.length() != 5) {
        system("cls");
        cout << "Guess this word: " <<
        displayWord << endl;
        while (gameOver != 'N') {
            cout << "Enter an uppercase letter:";
            cin >> letter;
            for (int x = 0; x < 5; x += 1) {
                if (originalword.substr(x, 1) == letter) {
                    displayWord.replace(x, 1, letter);
                }
            }
            dashReplaced = 'Y';
        }
        if (dashReplaced == 'Y') {
            if (displayWord.find("-") == -1) {
                gameOver = 'Y';
            }
        }
        cout << endl << "Yes, the word is " << originalword
        << endl;
        cout << "Great guessing!"
        << endl;
    }
}
```

+ 获取原始单词
当（原始单词）不恰好包含五个字符时

+ 2. 清屏

+ 3. 在显示单词中显示五个横线

+ 4. 重复，直到（游戏未结束）
获取一个大写字母
t 原始单词

+ 针对原始单词中的每个字母重复
如果（原始单词中的当前字符与该字母匹配）

+ 用该字母替换显示单词中的横线
向跟踪横线是否被替换的变量赋值 'Y'

+ 结束
重复
如果（某条横线被替换了）
如果（显示单词中不再包含任何横线）

+ 向跟踪游戏是否结束的变量赋值为 'Y'

+ 显示原始单词
显示“Great guessing（猜得好！）”消息

显示显示单词的状态

图 13-41 实验 13-2 的问题规范、IPO 图表信息和 C++ 指令（续）

![](img/d64a28a68f49d61137bf2f3170ac40ad_583_0.png)

# 第 13 章 字符串

（续）

```
将变量重置为 'N'
dashReplaced = 'N';
跟踪
横线是否被替换
结束 if
    } // 结束 if
else
    向数量加 1
    numIncorrect += 1;
错误猜测
    如果（错误的
    if (numIncorrect == 10)
    猜测是 >= 10)
    {
        向变量赋值 'Y'
    }
跟踪的，或哪个
gameOver = 'Y';
游戏已结束
```

显示“Sorry, the word is（抱歉，单词是）”
以及原始单词

```cpp
cout << endl <<
"Sorry, the word
is " << origword
    << endl;
    } // 结束 if
} // 结束 if
} // 结束 while
```

结束 if
重复

图 13-41 实验 13-42 的问题规范、IPO 图表信息和 C++ 指令

图 13-42 显示了整个吊字游戏（Hangman）程序的代码，13-43 和 13-44 显示了程序的运行示例。

+ 1/Lab13-2.cpp - 模拟吊字游戏
2 //创建/修订于 <你的名字> 于 <当前日期>
3
4
5 #include <iostream>
6 #include <string>
7 using namespace std;
8
9 int main()
10 {
11 //声明变量
12 string origword = "";
13 string letter = "";
14 char dashReplaced = 'N';
15 gameOver = 'N';
16 int numIncorrect = 0;
17 string displayWord = "------";
18
19 //获取原始单词
20 do// 开始循环
21 {
22
23 cout << "Enter a 5-letter word in uppercase: ";
24 getline(cin, origword);
25 } while (origword.length() != 5);
26

图 13-44 吊字游戏程序（续）

（续）

图 13-42 吊字游戏程序（续）

# 第 13 章 字符串

（续）

| 82 | //结束 if |
| 83 | //结束 while |
| 84 | |
| 85 | system("pause"); |
| 86 | return 0; |
| 87 | //结束 main 函数 |

![](img/d64a28a68f49d61137bf2f3170ac40ad_586_0.png)

13-42 吊字游戏程序

![](img/d64a28a68f49d61137bf2f3170ac40ad_586_1.png)

13-43 吊字游戏运行示例

![](img/d64a28a68f49d61137bf2f3170ac40ad_586_2.png)

13-44 吊字游戏另一个运行示例 56

# 指示

按照启动 C++ 开发工具的说明。根据你的开发工具，可能需要创建一个新项目；如果是，将其命名为 Lab13-2 Project 并保存在 CppChap13 文件夹中。在 Lab13-2.cpp 源文件中输入图 13-42 中的指令（不要换行）。将文件保存在项目文件夹或 CppChap13 文件夹中。现在按照相应的说明运行 Lab13-2.cpp。使用不恰包含五个字符的原始单词测试程序。还要使用图 13-43 和 13-44 中的数据测试程序。如有，修正程序中的任何错误。

# LAB 13-3

如有，创建一个名为 Lab13-3 Project 的项目。将 Lab13-2.cpp 复制到名为 cpp 的新文件中。修改 Lab13-2.cpp：目前吊字游戏允许用户输入五个字符的单词。修改程序使用户可以输入任意长度的单词。保存并运行程序。

# LAB 台台检查

检查图 13-45 显示的代码。屏幕上将显示什么？

```cpp
//Lab13-4.cpp - 显示消息
//创建/修订于 <名字> 于 <日期>

#include <iostream>
#include <string>
using namespace std;

int main()
{
    string message = "programming fun";
    string submessage1 = "";
    string submessage2 = "";

    message.erase(5, 2);
    message.insert(11, "is");
    message.replace(1, "f");

    submessage1 = message.substr(0, 11);
    submessage1.replace(7, 1, "m");
    submessage1.erase(2, 2);
    submessage1.replace(0, 1, "p");
    submessage1.insert(2, "o");
```

图 13-45 Lab 13-4 代码（续）

# 第 13 章 字符串

（续）

```cpp
subMessage2 = subMessage2.assign(5)
```

图 13-45 Lab 13-4 代码

![](img/d64a28a68f49d61137bf2f3170ac40ad_588_0.png)

# LAB 13-5 调试

按照启动 C++ 的说明打开 Lab13-5.cpp 文件。该文件位于 CppChap13/Lab13-5 Project 文件夹或 CppChap13 文件夹中。输入 Joe 并回车。在分别显示字母 J、o 和 e 后，程序显示 Joe。停止并调试程序。

# 总结

* string 数据类型通过 string 类添加到 C++ 语言中。
* 类型为 string 的内存位置（变量和命名常量）使用字符串字面量初始化，即包含在引号内的零或多个字符。大多数字符串变量初始化为空字符串。
* 你可以使用提取操作符从键盘获取字符串，但前提是该字符串不包含空白字符（空格、制表符或换行符）。
* getline 函数获取从键盘输入的字符串并将其存储在字符串变量中。字符串可以包含任何字符，包括空白字符（空格、制表符和换行）。getline 函数在遇到输入中的分隔符时停止读取和存储字符。该函数的默认分隔符是换行符。该函数读取并消耗（丢弃）分隔符。
* 计算机将键盘输入的字符存储在 cin 对象中。提取操作符和 getline 从对象中移除字符。然而，与提取操作符不同，它会将换行符留在 cin 对象中，getline 函数会消耗换行符。

- ignore 函数读取并消耗键盘输入的字符。该函数在消耗指定数量的字符或分隔符（以先到者为准）时停止读取和消耗。默认消耗数为1。

- 图 13-46 显示了本章涵盖每个函数的语法和目的。它还包含了字符串拼接运算符。assign、erase、insert 和 replace 函数是改变字符串值的自包含语句。

| 函数/操作符 | 语法 | 目的 |
| --- | --- | --- |
| assign 函数 | string.assign(count, character); | 拼接字符串；在字符串变量内重复字符 |
| erase 函数 | string.erase(subscript, count); | 移除字符串变量中任意位置的一个或多个字符 |
| find 函数 | string.find(searchString, subscript); | 搜索字符串变量以确定其是否包含特定的字符序列 |
| getline 函数 | getline(cin, variableName, delimiter); | 从键盘获取字符串输入 |
| ignore 函数 | cin.ignore(numberOfCharacters, delimiter); | 读取并消耗键盘输入的字符 |
| insert 函数 | string.insert(subscript, insertString); | 在字符串变量内插入字符 |
| length 函数 | string.length() | 确定字符串中包含的字符数量 |
| replace 函数 | string.replace(subscript, count, replacementString); | 用另一个字符序列替换字符串中的字符序列 |
| substr 函数 | string.substr(subscript, count)) | 访问字符串中包含的任意数量的字符 |

