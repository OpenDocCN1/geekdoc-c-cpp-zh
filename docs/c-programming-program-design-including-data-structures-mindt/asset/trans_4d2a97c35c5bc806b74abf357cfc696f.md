
![](img/b217c421655b51e7494cf3b89bb5432d_676_0.png)

**图 9-8** —— 结构体变量 `newEmployee`

语句：

```cpp
newEmployee.salary = 45678.00;
```

将 `newEmployee` 的工资设置为 45678.00。以下语句：

```cpp
newEmployee.name.first = "Mary";
newEmployee.name.middle = "Beth";
newEmployee.name.last = "Simmons";
```

分别将 `newEmployee` 的名字、中间名和姓氏设置为“Mary”、“Beth”和“Simmons”。注意，`newEmployee` 有一个名为 `name` 的成员。我们通过 `newEmployee.name` 访问这个成员。还要注意，`newEmployee.name` 是一个 `struct`，并且有三个成员。我们应用成员访问规则来访问结构体 `newEmployee.name` 的成员 `first`。因此，`newEmployee.name.first` 是存储名字的成员。

语句：

```cpp
cin >> newEmployee.name.first;
```

读取一个字符串并将其存储到 `newEmployee.name.first` 中。语句：

```cpp
newEmployee.salary = newEmployee.salary * 1.05;
```

更新 `newEmployee` 的工资。

以下语句将 employees 声明为包含 100 个分量的数组，其中每个分量的类型为 `employeeType`：

```cpp
employeeType employees[100];
```

for 循环：

```cpp
for (int j = 0; j < 100; j++)
    cin >> employees[j].name.first >> employees[j].name.middle
        >> employees[j].name.last;
```

读取 100 名员工的姓名，并将它们存储到数组 `employees` 中。因为 `employees` 是一个数组，所以访问某个分量时，我们使用索引。例如，`employees[50]` 是数组 `employees` 的第 51 个分量（回忆一下，数组索引从 0 开始）。因为 `employees[50]` 是一个结构体，所以我们应用成员访问规则来选择特定成员。

## 编程示例：销售数据分析

一家公司有六名销售人员。每月，他们外出销售公司产品。每月月底，每名销售人员的总销售额，连同该销售人员的 ID 和月份，都会记录在一个文件中。每年年底，公司经理希望看到以下表格格式的报告：

-----------年度销售报告-----------

| ID | QT1 | QT2 | QT3 | QT4 | 总计 |
|---|---|---|---|---|---|
| 12345 | 1892.00 | 0.00 | 494.00 | 322.00 | 2708.00 |
| 32214 | 343.00 | 892.00 | 9023.00 | 0.00 | 10258.00 |
| 23422 | 1395.00 | 1901.00 | 0.00 | 0.00 | 3296.00 |
| 57373 | 893.00 | 892.00 | 8834.00 | 0.00 | 10619.00 |
| 35864 | 2882.00 | 1221.00 | 0.00 | 1223.00 | 5326.00 |
| 54654 | 893.00 | 0.00 | 392.00 | 3420.00 | 4705.00 |
| 总计 | 8298.00 | 4906.00 | 18743.00 | 4965.00 | |

销售人员最大销售额：ID = 57373，金额 = $10619.00
季度最大销售额：季度 = 3，金额 = $18743.00

在本报告中，QT1 表示第 1 季度（第 1 至 3 月），QT2 表示第 2 季度（第 4 至 6 月），QT3 表示第 3 季度（第 7 至 9 月），QT4 表示第 4 季度（第 10 至 12 月）。

销售人员的 ID 存储在一个文件中；销售数据存储在另一个文件中。销售数据的形式如下：

```text
salesPersonID month saleAmount
.
.
.
```

此外，销售数据没有特定顺序；它不是按 ID 排序的。

销售数据示例为：

```text
12345 1 893
32214 1 343
23422 3 903
57373 2 893
.
.
.
```

让我们编写一个程序，以指定格式生成输出。

|  |  |
|---|---|
| **输入** | 一个包含每个销售人员 ID 的文件，以及另一个包含销售数据的文件。 |
| **输出** | 一个包含上述格式年度销售报告的文件。 |

## 问题分析与算法设计

根据问题要求，很明显每名销售人员的主要分量是销售人员 ID、季度销售金额和年度总销售金额。因为这些分量具有不同的类型，我们可以借助结构体将它们组合起来，定义如下：

```cpp
struct salesPersonRec
{
    string ID;                  // salesperson’s ID
    double saleByQuarter[4];    // array to store the total
                                // sales for each quarter
    double totalSale;           // salesperson’s yearly sales amount
};
```

因为有六名销售人员，所以我们使用一个包含六个分量的数组，其中每个分量的类型为 `salesPersonRec`，定义如下：

```cpp
salesPersonRec salesPersonList[NO_OF_SALES_PERSON];
```

其中 `NO_OF_SALES_PERSON` 的值为 6。

因为程序要求我们求出公司每个季度的总销售额，所以我们需要一个包含四个分量的数组来存储数据。注意，这些数据将用于确定销售额最高的季度。因此，程序还需要以下数组：

```cpp
double totalSaleByQuarter[4];
```

回忆一下，在 C++ 中，数组索引从 0 开始。因此，`totalSaleByQuarter[0]` 存储第 1 季度的数据，`totalSaleByQuarter[1]` 存储第 2 季度的数据，依此类推。

在整篇讨论中，我们将引用这些变量。

数组 `salesPersonList` 如图 9-9 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_679_0.png)

**图 9-9** 数组 `salesPersonList`

程序的第一步是将销售人员的 ID 读入数组 `salesPersonList`，并将每名销售人员的季度销售额和总销售额初始化为 0。完成这一步后，数组 `salesPersonList` 如图 9-10 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_680_0.png)

**图 9-10** 初始化后的数组 `salesPersonList`

下一步是处理销售数据。处理销售数据相当直接。对于包含销售数据的文件中的每个条目：

- 1. 读取销售人员的 ID、月份以及该月的销售金额。
- 2. 在数组 `salesPersonList` 中搜索，以定位对应该销售人员的分量。
- 3. 确定该月份对应的季度。
- 4. 通过加上该月的销售金额来更新该季度的销售额。

处理完销售数据文件后：

- 1. 计算每个销售人员的总销售额。
- 2. 计算每个季度的总销售额。
- 3. 打印报告。

上述讨论转化为以下算法：

- 1. 初始化数组 `salesPersonList`。
- 2. 处理销售数据。
- 3. 计算每个季度的总销售额。
- 4. 计算每个销售人员的总销售额。
- 5. 打印报告。
- 6. 计算并打印每个销售人员的最大销售额。
- 7. 计算并打印每个季度的最大销售额。

为了降低主程序的复杂性，让我们为这七个步骤分别编写一个单独的函数。

### 函数 `initialize`

该函数从输入文件中读取销售人员的 ID，并将销售人员的 ID 存储到数组 `salesPersonList` 中。它还将每名销售人员的季度销售金额和总销售金额初始化为 0。该函数的定义如下：

```cpp
void initialize(ifstream& indata, salesPersonRec list[],
                int listSize)
{
    for (int index = 0; index < listSize; index++)
    {
        indata >> list[index].ID; //get salesperson’s ID

        for (int quarter = 0; quarter < 4; quarter++)
            list[index].saleByQuarter[quarter] = 0.0;

        list[index].totalSale = 0.0;
    }
} //end initialize
```

### 函数 `getData`

该函数从输入文件中读取销售数据，并将相应信息存储到数组 `salesPersonList` 中。该函数的算法如下：

- 1. 读取销售人员的 ID、月份以及该月的销售金额。
- 2. 在数组 `salesPersonList` 中搜索，以定位对应该销售人员的分量。（因为销售人员的 ID 未排序，所以我们将使用顺序搜索来搜索该数组。）
- 3. 确定该月份对应的季度。
- 4. 通过加上该月的销售金额来更新该季度的销售额。

假设读取到的条目为：

```text
57373 2 350
```

这里，销售人员的 ID 是 57373，月份是 2，销售金额是 350。假设数组 `salesPersonList` 如图 9-11 所示。
