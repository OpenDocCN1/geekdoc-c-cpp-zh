

## 示例 H-13

```cpp
//STL functions search, sort, and binary_search

#include <iostream>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

int main()
{
    int intList[15] = {12, 34, 56, 34, 34,
                       78, 38, 43, 12, 25,
                       34, 56, 62, 5, 49};          //Line 1

    vector<int> vecList(intList, intList + 15);      //Line 2
    int list[2] = {34, 56};                          //Line 3

    vector<int>::iterator location;                  //Line 4

    ostream_iterator<int> screenOut(cout, " ");      //Line 5

    cout << "Line 6: vecList: ";                     //Line 6
    copy(vecList.begin(), vecList.end(), screenOut); //Line 7
    cout << endl;                                    //Line 8

    cout << "Line 9: list: ";                       //Line 9
    copy(list, list + 2, screenOut);                 //Line 10
    cout << endl;                                    //Line 11

    //search
    location = search(vecList.begin(), vecList.end(),
                      list, list + 2);               //Line 12

    if (location != vecList.end())                   //Line 13
        cout << "Line 14: list is found in vecList. "
             << "The first occurrence of \n "
             << " list in vecList is at position: "
             << (location - vecList.begin())
             << endl;                                //Line 14
    else                                             //Line 15
        cout << "Line 16: list is not in vecList."
             << endl;                                //Line 16

    //sort
    sort(vecList.begin(), vecList.end());            //Line 17

    cout << "Line 18: vecList after sorting:\n"
         << " ";                                    //Line 18
    copy(vecList.begin(), vecList.end(), screenOut); //Line 19
    cout << endl;

    //binary_search
    bool found;

    found = binary_search(vecList.begin(),
                          vecList.end(), 78);

    if (found)
        cout << "Line 24: 43 found in vecList "
             << endl;
    else
        cout << "Line 26: 43 not in vecList" << endl;

    return 0;
}
```

## 示例运行：

```
Line 6: vecList: 12 34 56 34 34 78 38 43 12 25 34 56 62 5 49
Line 9: list: 34 56
Line 14: list found in vecList. The first occurrence of
        list in vecList is at position: 1
Line 18: vecList after sorting:
         5 12 12 25 34 34 34 34 38 43 49 56 56 62 78
Line 24: 43 found in vecList
```

第2行的语句创建一个向量 vecList，并使用第1行创建的数组 intList 对其进行初始化。第3行的语句创建一个包含两个元素的数组 list，并同时初始化 list。第7行的语句输出 vecList。第12行的语句使用 search 函数在 vecList 中搜索 list 作为子序列第一次出现的位置。第13行到第16行的语句输出搜索结果。参见输出中标记为第14行的行。

第17行的语句使用 sort 函数对 vecList 进行排序。第19行的语句输出 vecList。在输出中，标记为第18行的行包含第18行到第20行语句的输出。

第22行的语句使用 binary_search 函数搜索 vecList。第23行到第26行的语句输出搜索结果。

## 第1章

- 1. a. 错误；b. 错误；c. 正确；d. 错误；e. 错误；f. 错误；g. 错误；h. 正确；i. 正确；j. 错误；k. 正确；l. 错误

- 3. 屏幕和打印机。

- 5. 操作系统监控计算机的整体活动并提供服务。其中一些服务包括内存管理、输入/输出活动和存储管理。

- 7. 在机器语言中，程序使用二进制代码编写，而在高级语言中，程序更接近自然语言。为了执行，高级语言程序被翻译成机器语言，而机器语言不需要翻译成任何其他语言。

- 9. 因为计算机不能直接执行用高级语言编写的指令，所以需要编译器将用高级语言编写的程序翻译成机器代码。

- 11. 每台计算机都直接理解自己的机器语言。因此，为了让计算机执行用高级语言编写的程序，必须将高级语言程序翻译成计算机的机器语言。

- 13. 在链接中，目标程序与程序中使用的库中的其他程序相结合，以创建可执行代码。

- 15. 要找到四次测试成绩的加权平均值，首先需要知道每次测试的成绩及其权重。接下来，将每次测试的成绩乘以其权重，然后将这些数字相加得到平均值。因此：
  - 1. 获取 testScore1、weightTestScore1
  - 2. 获取 testScore2、weightTestScore2
  - 3. 获取 testScore3、weightTestScore3
  - 4. 获取 testScore4、weightTestScore4
  - 5. weightedAverage = testScore1 * weightTestScore1 +
    testScore2 * weightTestScore2 +
    testScore3 * weightTestScore3 +
    testScore4 * weightTestScore4;

- 17. 要计算每平方英寸的价格，首先需要求出披萨的面积。然后将披萨的价格除以披萨的面积。设 radius 表示半径，area 表示圆的面积，price 表示披萨的价格。另外，设 pricePerSquareInch 表示每平方英寸的价格。
  - a. 获取 radius
  - b. area = π * radius * radius
  - c. 获取 price
  - d. pricePerSquareInch = price / area

- 19. 要计算一件商品的售价，我们需要知道该商品的原始价格（商店购买商品时的价格）。然后我们可以使用以下公式计算售价。

  ```
  sellingPrice = originalPrice + originalPrice * .60
  ```

  算法如下：

  - a. 获取 originalPrice
  - b. 使用以下公式计算 sellingPrice：

    ```
    sellingPrice = originalPrice + originalPrice * .60
    ```

  计算售价所需的信息是原始价格和加价百分比。

- 21. 假设 numOfPages 表示要传真的页数，billingAmount 表示传真页数的总费用。要计算总费用，你需要知道传真的页数。

  如果 numOfPages 小于或等于 10，则计费金额为服务费 + (numOfPages × 0.20)；否则，计费金额为服务费 + 10 × 0.20 + (numOfPages − 10) × 0.10。即，

  现在可以编写算法如下：

  - a. 获取 numOfPages。
  - b. 使用以下公式计算计费金额：

    ```
    if (numOfPages is less than or equal to 10)
        billingAmount = 3.00 + (numOfPages × 0.20);
    otherwise
        billingAmount = 3.00 + 10 × 0.20 + (numOfPages − 10) × 0.10;
    ```

- 23. 假设 averageTestScore 表示平均测试成绩，highestScore 表示最高测试成绩，testScore 表示测试成绩，sum 表示所有测试成绩的总和，count 表示班级中的学生人数，studentName 表示学生的姓名。

  - a. 首先，设计一个算法来查找平均测试成绩。要找到平均测试成绩，首先需要统计班级中的学生人数，并将每个学生的测试成绩相加。然后将总和除以 count 即可得出平均测试成绩。计算平均测试成绩的算法如下：

    - i. 将 sum 和 count 设置为 0。
    - ii. 对班上的每个学生重复以下步骤。
      - 1. 获取 testScore
      - 2. count 加 1，并将当前 testScore 加到 sum 中，更新 sum 的值。
    - iii. 使用以下公式计算平均测试成绩。

      ```
      if (count is 0)
          averageTestScore = 0;
      otherwise
          averageTestScore = sum / count;
      ```

  - b. 以下算法确定并打印所有测试成绩低于平均测试成绩的学生姓名。

    对班上的每个学生重复以下步骤。

    - i. 获取 studentName 和 testScore
    - ii. 如果（testScore 小于 averageTestScore）
            打印 studentName

  - c. 以下算法确定最高测试成绩。

    - i. 获取第一个学生的测试成绩，并将其称为 highestTestScore。
    - ii. 对班级中其余每个学生重复以下步骤
      - 1. 获取 testScore
      - 2. 如果（testScore 大于 highestTestScore）
              highestTestScore = testScore;

  - d. 要打印所有测试成绩与最高测试成绩相同的学生姓名，请将每个学生的测试成绩与最高测试成绩进行比较，如果相等，则打印姓名。以下算法完成了这一操作。对班上的每个学生重复以下步骤。

    - i. 获取 studentName 和 testScore
    - ii. 如果（testScore 等于 highestTestScore）
            打印 studentName

你可以使用在 a 到 d 部分获得的子问题的解决方案来设计主算法，如下所示：

- 1. 使用 a 部分中的算法查找平均测试成绩。
- 2. 使用 b 部分中的算法打印所有成绩低于平均测试成绩的学生姓名。
- 3. 使用 c 部分中的算法查找最高测试成绩。
- 4. 使用 d 部分中的算法打印所有测试成绩与最高测试成绩相同的学生姓名。

