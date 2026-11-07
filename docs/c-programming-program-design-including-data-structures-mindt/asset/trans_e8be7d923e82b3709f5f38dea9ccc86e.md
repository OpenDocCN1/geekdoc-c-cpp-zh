
```cpp
using namespace std;                                      //Line 7

int main()                                                  //Line 8
{                                                          //Line 9
        double num;                                        //Line 10

        num = 2 * PRIZE;                                   //Line 11
        mySpace::x = static_cast<num>;                     //Line 12
        cout << PRIZE << " " << mySpace::x << " "         //Line 13
             << num << endl;

        return 0;                                          //Line 14
}                                                          //Line 15
```

13. 以下程序有什么问题？(10)

```cpp
#include <iostream>                                      //Line 1

namespace aaa                                             //Line 2
{                                                          //Line 3
        const int x = 0;                                  //Line 3
        double y;                                          //Line 4
}                                                          

using namespace std;                                       //Line 5

int main()                                                  //Line 6
{                                                          
        y = 34.50;                                         //Line 7
        cout << "x = " << x << ", y = " << y             //Line 8
             << endl;                                      
        return 0;                                          //Line 9
}                                                          
```

14. 以下程序有什么问题？(10)

```cpp
#include <iostream>                                      //Line 1
#include <math>                                           //Line 2

using nameSpace std;                                      //Line 3

void main()                                               //Line 4
{                                                          //Line 5
        cout << floor(sqrt(14.56)) << std::endl;           //Line 6
        return 0;                                          //Line 7
}                                                          //Line 8
```

15. 考虑以下 C++ 代码。(11)

```cpp
string str1, str2;
char ch;
int pos;

cin >> str1 >> str2 >> pos;
ch = str1[pos];
str1[pos] = str2[pos];
str2[pos] = ch;

cout << str1 << " " << str2 << endl;
```

回答以下问题。

- a. 如果输入是 **Summer Vacation 1**，输出是什么？
- b. 如果输入是 **Temporary Project 4**，输出是什么？
- c. 如果输入是 **Social Network 0**，输出是什么？

16. 假设有以下语句：

```cpp
string str, str1, str2;

cin >> str1 >> str2;

if (str1 == str2)
    str = str1 + " = " + str2;
else if (str1 > str2)
    str = str1 + " > " + str2;
else
    str = str1 + " < " + str2;
```

回答以下问题。(11)

- a. 如果输入是 **Temporary Storage**，**str** 的值是什么？
- b. 如果输入是 **Main Memory**，**str** 的值是什么？
- c. 如果输入是 **run! run!**，**str** 的值是什么？

17. 以下程序的输出是什么？(11)

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

**18.** 考虑以下语句。

```cpp
string str = "This summer we will drive across the country!";
```

以下语句的输出是什么？（假设各部分彼此独立。）(11)

- a.

  ```cpp
  cout << str.size() << endl;
  ```

- b.

  ```cpp
  cout << str.substr(12, 20) << endl;
  ```

- c.

  ```cpp
  string::size_type ind = str.find('s');
  str.replace(ind + 2, 6, "spring");
  cout << str << endl;
  ```

- d.

  ```cpp
  str.erase(20, 25);
  str.insert(20, "enjoy Caribbean cruise!");
  cout << str << endl;
  ```

## 编程练习

- 1.
  - **a.** 定义枚举类型 `triangleType`，其值为 `scalene`、`isosceles`、`equilateral` 和 `noTriangle`。
  - **b.** 编写函数 `triangleShape`，它接受三个数字作为参数，每个数字表示三角形一条边的长度。该函数
  - **c.** 编写程序，提示用户输入三角形各边的长度，并输出三角形的形状。

- 2. 重做第 4 章的编程练习 16，使所有命名常量都在 `namespace` 中定义。

- 3. 编程示例：Pig Latin 字符串将字符串转换为 pig Latin 形式，但它只处理一个单词。重写该程序，使其可用于处理长度未指定的文本。如果一个单词以标点符号结尾，则在 pig Latin 形式中，将标点符号放在字符串末尾。例如，`Hello!` 的 pig Latin 形式是 `ello-Hay!`。假设文本包含以下标点符号：`,`（逗号）、`.`（句号）、`?`（问号）、`;`（分号）和 `:`（冒号）。（你的程序可以将输出存储在文件中。）

- 4. 编写程序，提示用户输入一个字符串。然后程序使用函数 `substr` 从字符串中删除所有元音字母。例如，如果 `str = "There"`，则删除所有元音字母后，`str = "Thr"`。删除所有元音字母后，输出该字符串。你的程序必须包含一个删除所有元音字母的函数，以及一个判断字符是否为元音字母的函数。

- 5. 编写一个可用于计算联邦税的程序。税额计算如下：对于单身人士，标准免税额为 $4,000；对于已婚人士，标准免税额为 $7,000。个人还可以将其总收入的最高 6% 存入养老金计划。税率如下：如果应税收入为：
  - 在 $0 到 $15,000 之间，税率为 15%。
  - 在 $15,001 到 $40,000 之间，税额为 $2,250 加上超过 $15,000 的应税收入的 25%。
  - 超过 $40,000，税额为 $8,460 加上超过 $40,000 的应税收入的 35%。

  提示用户输入以下信息：

  - 婚姻状况
  - 如果婚姻状况为“已婚”，询问 14 岁以下子女的数量
  - 总工资（如果婚姻状况为“已婚”且配偶双方都有收入，请输入合并工资。）
  - 向养老基金缴纳的总收入百分比

  你的程序必须至少包含以下函数：

  - a. 函数 `getData`：该函数要求用户输入相关数据。
  - b. 函数 `taxAmount`：该函数计算并返回应缴税额。

  要计算应税收入，减去标准免税额、向养老金计划缴纳的金额以及个人免税额（每人 $1,500）之和。（注意，如果一对已婚夫妇有两个 14 岁以下子女，则个人免税额为 $1,500 × 4 = $6,000。）

- 6. 编写一个程序，使用随机数生成器生成一个两位正整数，并允许用户执行以下一项或多项操作：
  - a. 将数字加倍。
  - b. 反转数字的各位。
  - c. 将数字提高到 2、3 或 4 次幂。
  - d. 求数字各位之和。
  - e. 如果该数字是两位数，则将第一位数字提高到第二位数字的幂。
  - f. 如果该数字是三位数且最后一位数字小于或等于 4，则将前两位数字提高到末位数字的幂。

  执行操作后，如果数字小于 10，则给数字加 10。此外，每次操作后判断该数字是否为素数。

  每个后续操作都应基于上一次操作生成的数字执行。你的程序不应包含任何全局变量，并且这些操作中的每一个都必须由单独的函数实现。此外，你的程序应由菜单驱动。

- 7. **（分数计算器）** 编写一个程序，让用户对分数执行算术运算。分数形式为 *a/b*，其中 *a* 和 *b* 是整数，且 *b ≠ 0*。你的程序必须由菜单驱动，允许用户选择运算（+、-、* 或 /），并输入每个分数的分子和分母。此外，你的程序必须至少包含以下函数：
  - a. **函数 menu：** 该函数向用户说明程序用途，解释如何输入数据，并允许用户选择运算。
  - b. **函数 addFractions：** 该函数接受四个整数作为输入，分别表示两个分数的分子和分母，将分数相加，并返回结果的分子和分母。（注意，该函数总共有六个参数。）
  - c. **函数 subtractFractions：** 该函数接受四个整数作为输入，分别表示两个分数的分子和分母，将分数相减，并返回结果的分子和分母。（注意，该函数总共有六个参数。）
  - d. **函数 multiplyFractions：** 该函数接受四个整数作为输入，分别表示两个分数的分子和分母，将分数相乘，并返回结果的分子和分母。（注意，该函数总共有六个参数。）

![](img/b217c421655b51e7494cf3b89bb5432d_568_0.png)

