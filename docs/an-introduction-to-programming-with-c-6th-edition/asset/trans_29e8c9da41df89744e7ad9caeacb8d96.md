

# 第 12 章小型测验答案

## 小型测验 12-1
- 1. b. int quantities[4][2] = {0};
- 2. 20
- 3. quantities[0][0]
- 4. quantities[3][1]
- 5. quantities[0][1] = 5;

## 小型测验 12-2
- 1. d. total += purchases[1][0];
- 2. c. if (scores[2][3] > 25)
- 3. bonus = sales[0][1] * .15;
- 4. a. if (row >= 0 && row < 10)

# 第 12 章实验答案

## 实验 12-1 停止与分析
- 1. 34000
- 2. 二月份的总销售额可以通过将 company[0][1] 元素的内容加上 company[1][1] 元素的内容来计算。
- 3. company 数组中最高的行下标是 1。最高的列下标是 5。
- 4. 一月份国际商店存储在 company[1][0] 元素中。

```cpp
int location = 0;
while (location < 2)
  for (int month = 0; month < 6; month += 1)
    companySales += company[location][month];
  //end for
  location += 1;
//end while
```

# 附录 A 小型测验与实验答案

- 6. 赋值语句需要更改为 company_Sales = company[month - 1];
- 7. 无需回答。
- 8.

```cpp
//Lab12-1.cpp - 计算国内总销售额、
//国际总销售额以及公司总销售额
// 创建/修订于 <your name> 于 <current date>

#include <iostream>
using namespace std;

int main()
{
    //声明数组和变量
    int company[2][6] = {{12000, 45000, 32000, 67000, 24000, 55000}, {100000, 56000, 42000, 23000, 12000, 34000}};

    int companySales = 0;
    int domesticSales = 0;
    int internationalSales = 0;

    //累加销售额
    for (int month = 0; month < 6; month += 1) {
        domesticSales += company[0][month];
        internationalSales += company[1][month];
    }
    companySales = domesticSales + internationalSales;

    //显示总销售额
    cout << "Domestic sales: $" << domesticSales << endl;
    cout << "International sales: $" << internationalSales << endl;
    cout << "Company sales: $" << companySales << endl;

    system("pause");
    return 0;
}//end of main function
```

- 9.

```cpp
//Lab12-1.cpp - 计算国内总销售额、
//国际总销售额以及公司总销售额
// 创建/修订于 <your name> 于 <current date>

#include <iostream>
using namespace std;

int main()
{
    //声明数组和变量
    int company[2][6] = {{12000, 45000, 32000,
67000, 24000, 55000,
100000, 56000, 42000,
23000, 12000, 34000}};

    int monthSales[6] = {0};
    int companySales = 0;
    int domesticSales = 0;
    int internationalSales = 0;

    //累加销售额
    for (int month = 0; month < 6; month += 1)
    {
        domesticSales += company[0][month];
        internationalSales += company[1][month];
        monthSales[month] = company[0][month] + company[1][month];
    } //end for
    companySales = domesticSales + internationalSales;

    //显示总销售额
    cout << "Domestic sales: " << domesticSales << endl;
    cout << "International sales: " << internationalSales << endl;

    cout << "Company sales: " << companySales << endl;

    //显示每月销售额
    for (int x = 0; x < 6; x += 1)
    {
        cout << "Month " << x + 1 << " sales: $";
        cout << monthSales[x] << endl;
    } //end
    system("pause");
    return 0;
}//end of main function
```

## 实验 12-2 计划与创建
无需回答。

## 实验 12-3 修改
```cpp
//Lab12-3.cpp - 显示运费
// 创建/修订于 <your name> 于 <current date>

#include <iostream>
using namespace std;

int main()
{
    //声明数组和变量
    int shipCharges[3][2] = {{101, 0},
    {51, 10},
    {1, 20}};

    int numOrdered = 0;
    int rowSub = 0;
    char found = 'N';

    //输入数量
    cout << "Number ordered ";
    cout << "(negative number or 0 to end): ";
    cin >> numOrdered;

    while (numOrdered > 0 && numOrdered <= 999)
    {
        //搜索数组
        rowSub = 0;
        while (rowSub < 3 && found == 'N')
            if (numOrdered >= shipCharges[rowSub][0])
                found = 'Y';
            else
                rowSub += 1;
        //end while

        //显示运费
        cout << "Shipping charge for quantity of "
        << numOrdered << " is $"
        << shipCharges[rowSub][1] << endl;

        //输入数量
        cout << "Number ordered ";
        cout << "(negative number or 0 to end): ";
        cin >> numOrdered;
        found = 'N';
    } //end while

    system("pause");
    return 0;
}//end of main function
```

## 实验 12-4 检查
| sales[0][0] | sales[0][1] |
|---|---|
| 90.0 | 88.0 |
| sales[1][0] | sales[1][1] |
|---|---|
| 100.0 | 68.0 |

![](img/d64a28a6f49d61137bf2f3170ac4ad_698_0.png)

| sales[2][0] | sales[2][1] |
|---|---|
| 66 | 78.0 |
| total | book |
| 66 | 6 |
| 1200.38 | # |
| 8551.6 | 8 |
| 7225.66 | 3 |
| 9654.93 | @ |
| 10435.6 | # |
| 1781.9 | 2 |

## 实验 12-5 调试
要调试此程序，将第一个循环中的 `numbers[row][0] = counter * counter;` 更改为 `numbers[row][1] = counter * counter;`，然后在 `numbers[row][1] = counter * counter;` 语句下方输入 `counter += 1;`（或 `counter = counter + 1;`）。

# 第 13 章小型测验答案

## 小型测验 13-1
- 1. c. const string FIRST_PRES = "George Washington";
- 2. b. string country = "";
- 3. a. getline(cin, streetAddress, '\n');
- 4. c. cin.ignore(10, '\n');

## 小型测验 13-2
- 1. a. while (employee.length() > 20)
- 2. c. if (code.length() == 7)
- 3. d. both a and b
- 4. cout << college.substr(college.length() - 1);

## 小型测验 13-3
- 1. location = cityState.find(",", 0);
- 2. 13
- 3. d. all of the above

## 小型测验 13-4
- 1. d. none of the above
- 2. sentence = sentence + temp.assign(4, '!');
- 3. b. areaCode = "(" + areaCode + ")";

# 第 13 章实验答案
![](img/d64a28a6f49d61137bf2f3170ac4ad_700_0.png)

## 实验 13-1 停止与分析
- 1. 循环目的是逐个访问 `phone` 变量中的每个字符，以便删除任何括号或连字符。
- 2. 第 26 行的语句将 `phone` 变量中的当前字符赋值给 `currentChar` 变量。
- 3. 第 27 行的选择结构将 `phone` 中的当前字符与括号进行比较。如果当前字符是括号或连字符，第 31 行的语句从 `phone` 变量中删除该字符。第 32 行的语句从 `numChars` 变量中减 1，用于跟踪 `phone` 变量中字符的数量。如果当前字符不是括号或连字符，第 35 行的语句将下标变量 `subscript` 的计数加 1，从而访问 `phone` 中的下一个字符。
- 4. 在处理程序循环之前，第 21 行的语句将存储在 `phone` 中的中的字符数量赋值给 `numChars`。如果 `phone` 包含 111-2222 这八个字符，该语句将 8 赋值给 `numChars`。当第 31 行语句从 `phone` 中删除一个字符时，变量包含的字符会减少一个。例如，如果第 31 行从 `phone` 中的 111-2222 删除一个字符，该变量将包含七个字符而不是八个。
- 5. 假设 `phone` 变量为 `(500)333-4444`。第 26 行的语句将下标为 0 的左括号赋值给 `currentChar` 变量。当第 31 行删除左括号时，`phone` 变成了变量中的第一个字符，因此下标变为 0。换句话说，当你从变量中删除字符时，下一个字符会获得相同的下标。然而，当你没有从变量中删除字符时，你需要更新下标以访问变量中的下一个字符。
- 6. 无需回答。
- 7. 将第 31 行的 `phone.erase(subscript, 1);` 语句更改为 `phone.replace(subscript, 1, "");`

## 实验 13-2 计划与创建
![](img/d64a28a6f49d6113bf2f3170ac4ad_701_0.png)
无需回答。

## 实验 13-3 修改
```cpp
//Lab13-3.cpp - 模拟挂索游戏
// 创建/修订于 <your name> 于 <current date>
#include <iostream>
#include <string>
using namespace std;

int main()
{
    //声明变量
    string origWord = "";
    string letter = "";
    char dashReplaced = 'N';
    char gameOver = 'N';
    int numIncorrect = 0;
    string displayWord = "";
    int numChars = 0;

    //获取原始单词
    cout << "Enter a word in uppercase: ";
    getline(cin, origWord);
    numChars = origWord.length();
    displayWord.assign(numChars, '--');
}
```

