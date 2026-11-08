
为本实验提供的数据文件包含输入语句和必要的变量声明。你需要使用循环检查数组中的所有项，并测试是否匹配。你还需要在匹配时设置一个标志，然后测试该标志变量，以确定是否应打印“未找到区号。”消息。代码中的注释会告诉你应在哪里编写语句。你可以使用本章中的邮购程序作为指南。

- 1. 使用记事本或你选择的文本编辑器打开名为 `AreaCodes.cpp` 的源代码文件。
- 2. 研究预先编写的代码，确保你理解它。
- 3. 编写一个循环语句，检查数组中存储的区号。
- 4. 编写测试是否匹配的代码。
- 5. 编写代码，在适当的时候打印消息“未找到区号。”
- 6. 将此源代码文件保存到你选择的目录中，然后使该目录成为你的工作目录。
- 7. 编译源代码文件 `AreaCodes.cpp`。
- 8. 使用以下内容作为输入执行程序：
  - 269
  - 512
  - 312
  - 708

## 并行数组

正如你在*《程序设计逻辑与设计（第五版）》*中所学，你使用并行数组来存储值，并维护数组中存储项之间的关系。图 6-5 显示，存储在 `stuID[0]` 中的学生 ID 号和存储在 `grades[0]` 中的成绩是相关的——学生 56 获得了 99 分。

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_118_0.png)

> **注意**
>
> 并行数组具有相同数量的元素，但它们不一定存储相同数据类型的项。

这种关系通过在访问每个数组时使用相同的下标值来建立。请注意，作为程序员，你必须始终使用相同的下标在代码中维护这种关系。C++ 不会创建或维护这种关系。

*《程序设计逻辑与设计（第五版）》*中讨论的一个程序，是本章前面“在数组中搜索精确匹配”一节中讨论的邮购程序的扩展版本。在这个扩展程序中，你想确定所订购商品的价格，将该价格乘以订购数量，并打印账单。你使用并行数组来帮助组织程序的数据。一个数组 `valid_item` 包含六个有效商品编号。另一个数组 `valid_item_price` 包含六个有效价格。每个价格与其他数组中对应商品编号处于相同位置。当顾客订购商品时，你在 `valid_item` 数组中搜索顾客的商品编号。找到商品编号后，你使用存储在 `valid_item_price` 数组同一位置的价格来计算顾客的账单。完整的 C++ 程序存储在名为 `MailOrder2.cpp` 的文件中。搜索 `valid_item` 数组并使用 `valid_item_price` 数组中的价格计算顾客账单的伪代码和 C++ 代码如图 6-6 所示。

```text
start
  string name
  string address
  num item
  num quantity
  num price
  num SIZE = 6
  num VALID_ITEM[SIZE] = 106, 108, 307, 405, 457, 688
  num VALID_ITEM_PRICE[SIZE] = 0.59, 0.99, 4.50, 15.99, 17.50, 39.00
  num sub
  string foundIt = "N"
  string MSG_YES = "Item available"
  string MSG_NO = "Item not found"
  get name, address, item, quantity
  sub = 0
  while sub < SIZE
    if item = VALID_ITEM[sub] then
      foundIt = "Y"
      price = VALID_ITEM_PRICE[sub]
    endif
    sub = sub + 1
  endwhile
  if foundIt = "Y"
    print MSG_YES
    print quantity, " at ", price, " each"
    print "Total ", quantity * price
  else
    print MSG_NO
  endif
stop
```

**图 6-6** 扩展邮购程序的伪代码和 C++ 代码

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    // Declare variables
    const int STR_LENGTH = 80;
    char name[STR_LENGTH], address[STR_LENGTH];
    int item, quantity;
    double price = 0.0;
    const int SIZE = 6;
    int valid_item[] = {106, 108, 307, 405, 457, 688};
    double valid_item_price[] = {0.59, 0.99, 4.50, 15.99, 17.50, 39.00};
    int sub;
    bool foundIt = false;
    const string MSG_YES = "Item Available";
    const string MSG_NO = "Item not found";

    // Get user input
    cout << "Enter name: ";
    cin.getline(name, STR_LENGTH);
    cout << "Enter address: ";
    cin.getline(address, STR_LENGTH);
    cout << "Enter item number: ";
    cin >> item;
    cout << "Enter quantity: ";
    cin >> quantity;
    // Initialize loop index to 0
    sub = 0;
    // loop through array
    while (sub < SIZE)
    {
        // Test to see if this item is a valid item
        if(item == valid_item[sub])
        {
            foundIt = true; // Set flag to true
            price = valid_item_price[sub]; // Get price from parallel array
        }
        sub += 1;                         // Increment loop index
    }
    // Test value of foundIt
    if(foundIt == true)
    {
        cout << MSG_YES << endl;
        cout << quantity << " at " << price << " each" << endl;
        cout << "Total " << quantity * price << endl;
    }
    else
        cout << MSG_NO << endl;

    return 0;
}
```

### 练习 6-3：并行数组

使用你学到的并行数组知识评估以下代码，然后回答问题：

```cpp
string cities[] = "Batavia", "Gary", "Westmont", "Plano";
int populations[] = 239000, 102700, 24300, 5700;
const int MAX_CITIES = 4;
int saveIt;
int i, x;
string inCity;
cout << "Enter city name: ";
cin >> inCity;

for(i = 0; i = MAX_CITIES; ++i)
{
    if(inCity == cities[i])
    {
        saveIt = i;
    }
}
cout << "Population for " << cities[saveIt] <<
     " is " << populations[saveIt] << endl;
```

- 1. 数组的声明和初始化正确吗？如果不正确，如何修复？
- 2. `for` 循环写得正确吗？如果不正确，如何修复？
- 3. 按照现在的写法，`for` 循环将执行多少次？
- 4. 你会如何描述语句 `saveIt = i;` 的目的？

### 实验 6-3：并行数组

在本实验中，你使用学到的并行数组知识来完成一个部分完成的 C++ 程序。该程序在*《程序设计逻辑与设计（第五版）》*第 6 章练习 6 中描述。该程序应打印比利山羊快餐店某快餐食品的名称和价格，或者打印消息“抱歉，我们不供应那种商品。”

开始之前请仔细阅读问题描述。为本实验提供的数据文件包含必要的变量声明和输入语句。你需要编写程序的一部分，该部分搜索食品名称，并打印其名称和价格，或者在未找到该商品时打印错误消息。代码中的注释会告诉你应在哪里编写语句。你可以使用图 6-6 中所示的扩展邮购程序作为指南。

- 1. 使用记事本或你选择的文本编辑器打开名为 `BillyGoat.cpp` 的源代码文件。
- 2. 研究预先编写的代码，确保你理解它。
- 3. 编写代码，在数组中搜索顾客订购的食品名称。
- 4. 编写代码，打印该食品的名称和价格，或打印错误消息。
- 5. 将此源代码文件保存到你选择的目录中，然后使该目录成为你的工作目录。
- 6. 编译源代码文件 `BillyGoat.cpp`。

> 请记住，C++ 区分大小写，这意味着它会区分大写字母和小写字母。

- 7. 使用以下数据执行程序并记录输出：

| 顾客编号 | 订购商品 |
|---|---|
| 123 | 薯条 |
| 234 | 百事可乐 |
| 345 | 咖啡 |
| 456 | 薯片 |
| 567 | 洋葱圈 |
| 678 | 可乐 |
| 789 | 汉堡 |

