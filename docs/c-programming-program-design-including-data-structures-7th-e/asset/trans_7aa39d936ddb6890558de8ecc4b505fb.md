
12. 下面的程序有什么错误？(10)

```cpp
#include <iostream> //Line 1

namespace mySpace //Line 2
{ //Line 3
    const double RATE = 15.35; //Line 4
    int a; //Line 5
} //Line 6

using namespace std; //Line 7

int main() //Line 8
{ //Line 9
        int b; //Line 10

        cin >> b; //Line 11
        a = b; //Line 12
        cout << RATE << " " << a + 2 << " " << b //Line 13
             << endl;

        return 0; //Line 14
} //Line 15
```

13. 下面的程序有什么错误？(10)

```cpp
#include <iostream> //Line 1

namespace aaa //Line 2
{ //Line 3
    const int X = 0; //Line 3
    double y; //Line 4
}

using namespace std; //Line 5

int main() //Line 6
{
        y = 34.50; //Line 7
        cout << "X = " << X << ", y = " << y //Line 8
             << endl;
        return 0; //Line 9
}
```

14. 下面的程序有什么错误？(10)

```cpp
#include <iostream> //Line 1
#include <cmath> //Line 2

using name std; //Line 3

int main() //Line 4
{ //Line 5
        std::cout << sqrt (14.56) << endl; //Line 6
        return 0; //Line 7
} //Line 8
```

15. 考虑以下 C++ 代码：

```cpp
string str1;
string str2;
char ch;
int index;

cin >> str1;
cin >> str2;
cin >> index;

ch = str1[index];
str1[index] = str2[index];
str2[index] = ch;

cout << str1 << " " << str2 << endl;
```

回答以下问题：(11)

- a. 如果输入是 `Hello There 2`，输出是什么？
- b. 如果输入是 `Diamond Gold 0`，输出是什么？
- c. 如果输入是 `C++ Java 1`，输出是什么？

16. 假设有以下语句：

```cpp
string str1, str2;

cin >> str1 >> str2;

if (str1 == str2)
    cout << str1 + "!" << endl;
else if (str1 > str2)
    cout << str1 + " > " + str2 << endl;
else
    cout << str1 + " < " + str2 << endl;
```

回答以下问题：(11)

- a. 如果输入是 `Programming Project`，输出是什么？
- b. 如果输入是 `Summer Trip`，输出是什么？
- c. 如果输入是 `Winter Cold`，输出是什么？

17. 下面程序的输出是什么？(11)

```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string str = "Regular exercise can reduce health insurance cost.";
    string str1;
    string str2 = "low fat diet";
    string newStr;

    string::size_type index;

    index = str.find("can");
    str1 = str.substr(0, index - 1);
    cout << str1 << endl;

    newStr = str1 + " and " + str2;
    cout << newStr << endl;
    cout << newStr.length() << endl;

    cout << str1.find("ex") << endl;
    cout << str2.find('d') << endl;

    index = str.find("health");
    newStr = str.substr(index, 17);

    cout << newStr << endl;
    cout << newStr.substr(7, 14) << endl;

    index = str.find("cost");
    cout << str.replace(index, 4, "$$$$") << endl;

    str = "Social Media!!";
    cout << str << endl;
    cout << str.length() << endl;

    str[0] = 'S';
    index = str.find('N');
    str[index] = 'M';

    cout << str << endl;

    return 0;
}
```

18. 考虑以下语句：

```cpp
string str = "Now is the time for the party!";
```

以下语句的输出是什么？（假设各部分彼此独立。）(11)

- a. `cout << str.size() << endl;`
- b. `cout << str.substr(7, 8) << endl;`
- c.
    ```cpp
    string::size_type ind = str.find('t');
    string s = str.substr(ind + 4, 9);
    cout << s << endl;
    ```
- d. `cout << str.insert(11, "best ") << endl;`
- e.
    ```cpp
    str.erase(16, 14);
    str.insert(16, "to study for the exam?");
    cout << str << endl;
    ```

## 编程练习

- **1.**
  
  - **a.** 定义枚举类型 `triangleType`，其值为 `scalene`、`isosceles`、`equilateral` 和 `noTriangle`。
  - **b.** 编写函数 `triangleShape`，以三个数为参数，每个数表示三角形一条边的长度。该函数应返回三角形的形状。*（注：在三角形中，任意两边长度之和大于第三边长度。）*
  - **c.** 编写程序，提示用户输入三角形各边的长度，并输出三角形的形状。

- **2.** 重做第4章编程练习14（手机公司），使所有命名常量都在一个命名空间中定义。

- **3.** 编程示例：Pig Latin 字符串将字符串转换为 Pig Latin 形式，但它只处理一个单词。重写该程序，使其可用于处理长度未指定的文本。如果一个单词以标点符号结尾，则在 Pig Latin 形式中，将标点放在字符串末尾。例如，`Hello!` 的 Pig Latin 形式是 `ello-Hay!`。假设文本包含以下标点符号：`,`（逗号）、`.`（句号）、`?`（问号）、`;`（分号）和 `:`（冒号）。（你的程序可以将输出存储在文件中。）

- **4.** 编写程序，提示用户输入一个字符串。然后程序使用函数 `substr` 从字符串中删除所有元音字母。例如，如果 `str = "There"`，则删除所有元音字母后，`str = "Thr"`。删除所有元音字母后，输出该字符串。你的程序必须包含一个删除所有元音字母的函数，以及一个判断字符是否为元音字母的函数。

- **5.** 编写一个可用于计算联邦税的程序。税额计算如下：对于单身人士，标准免税额为 $4,000；对于已婚人士，标准免税额为 $7,000。一个人还可以将其总收入的至多 6% 存入养老金计划。税率如下：
  
  - 在 $0 到 $15,000 之间，税率为 15%。
  - 在 $15,001 到 $40,000 之间，税额为 $2,250 加上超过 $15,000 的应纳税所得额的 25%。
  - 超过 $40,000 时，税额为 $8,460 加上超过 $40,000 的应纳税所得额的 35%。
  
  提示用户输入以下信息：
  
  - 婚姻状况
  - 如果婚姻状况为“已婚”，询问未满14岁的子女数量
  - 总工资（如果婚姻状况为“已婚”且夫妻双方均有收入，请输入合并工资。）
  - 向养老基金缴纳的总收入百分比
  
  你的程序必须至少包含以下函数：
  
  - a. 函数 getData：该函数要求用户输入相关数据。
  - b. 函数 taxAmount：该函数计算并返回应缴税款。
  
  计算应纳税所得额时，减去标准免税额、向养老金计划缴纳的金额以及个人免税额之和；个人免税额为每人 $1,500。（注意，如果一对已婚夫妇有两个未满14岁的子女，则个人免税额为 $1,500 * 4 = $6,000。）

- **6.** 编写程序，使用随机数生成器生成一个两位正整数，并允许用户执行以下一项或多项操作：
  
  - a. 将该数加倍。
  - b. 反转该数的数字。
  - c. 将该数提高到 2、3 或 4 次幂。
  - d. 求该数各位数字之和。
  - e. 如果该数是两位数，则将第一位数字提高到第二位数字的幂。
  - f. 如果该数是三位数且最后一位数字小于或等于4，则将前两位数字提高到最后一位数字的幂。
  
  执行一次操作后，如果该数小于10，则给该数加10。此外，每次操作后判断该数是否为质数。
  
  后续每次操作都应基于上一次操作生成的数执行。你的程序不应包含任何全局变量，并且这些操作中的每一个都必须由单独的函数实现。此外，你的程序应采用菜单驱动方式。

- **7.** **（分数计算器）** 编写程序，让用户对分数执行算术运算。分数形式为 *a/b*，其中 *a* 和 *b* 是整数，且 *b* ≠ 0。你的程序必须采用菜单驱动方式，允许用户选择运算（+, −, *, /），并输入每个分数的分子和分母。此外，你的程序必须至少包含以下函数：
  
  - a. 函数 menu：该函数向用户说明程序的目的，解释如何输入数据，并允许用户选择运算。
  - b. 函数 addFractions：该函数接受四个整数作为输入，分别表示两个分数的分子和分母，将这两个分数相加，并返回结果的分子和分母。（注意，该函数总共有六个参数。）

![](img/d0be7fc6d804b63484835c6c8bc67a07_567_0.png)

