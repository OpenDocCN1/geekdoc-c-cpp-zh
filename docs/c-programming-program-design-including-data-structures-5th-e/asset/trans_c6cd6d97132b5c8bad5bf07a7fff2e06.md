
具有相同的底层结构。例如，入职日期和离职日期都是 `int` 数据类型。让我们按如下方式重新组织这个 `struct`：

```c
struct nameType
{
    string first;
    string middle;
    string last;
};
```

```c
struct addressType
{
    string address1;
    string address2;
    string city;
    string state;
    string zip;
};
```

```c
struct dateType
{
    int month;
    int day;
    int year;
};
```

```c
struct contactType
{
    string phone;
    string cellphone;
    string fax;
    string pager;
    string email;
};
```

我们将员工的姓名、地址和联系方式分成了子类别。此外，我们定义了一个 `struct` dateType。让我们按如下方式重建员工记录：

```c
struct employeeType
{
    nameType name;
    string empID;
    addressType address;
    dateType hireDate;
    dateType quitDate;
    contactType contact;
    string deptID;
    double salary;
};
```

这个员工 `struct` 中的信息比之前的更容易管理。这个 `struct` 中的一部分可以复用来构建另一个 `struct`。例如，假设你想定义客户记录。每个客户都有名、姓和中间名，以及地址和联系方式。因此，你可以使用结构体 `nameType`、`addressType`、`contactType` 以及客户特有的成员，快速组合出客户记录。

接下来，让我们声明一个 employeeType 类型的变量，并讨论如何访问其成员。

考虑以下语句：

```c
employeeType newEmployee;
```

这条语句将 newEmployee 声明为 employeeType 类型的结构体变量（见图 10–8）。

![](img/f97f778697507bb6fdd80c5991210cba_619_0.png)

**图 10–8** 结构体变量 newEmployee

## 编程示例：销售数据分析

一家公司有六名销售人员。每个月，他们都会踏上公路旅程去销售公司的产品。每月月底，每位销售人员的总销售额连同该销售人员的 ID 和月份一起记录在一个文件中。每年年底，公司经理希望看到采用以下表格格式的报告：

**年度销售报告**

| ID | QT1 | QT2 | QT3 | QT4 | 总计 |
|---:|---:|---:|---:|---:|---:|
| 12345 | 1892.00 | 0.00 | 494.00 | 322.00 | 2708.00 |
| 32214 | 343.00 | 892.00 | 9023.00 | 0.00 | 10258.00 |
| 23422 | 1395.00 | 1901.00 | 0.00 | 0.00 | 3296.00 |
| 57373 | 893.00 | 892.00 | 8834.00 | 0.00 | 10619.00 |
| 35864 | 2882.00 | 1221.00 | 0.00 | 1223.00 | 5326.00 |
| 54654 | 893.00 | 0.00 | 392.00 | 3420.00 | 4705.00 |
| **总计** | **8298.00** | **4906.00** | **18743.00** | **4965.00** |  |

销售人员最高销售额：ID = 57373，金额 = $10619.00

季度最高销售额：季度 = 3，金额 = $18743.00

在此报告中，QT1 代表第 1 季度（第 1 至 3 月），QT2 代表第 2 季度（第 4 至 6 月），QT3 代表第 3 季度（第 7 至 9 月），QT4 代表第 4 季度（第 10 至 12 月）。

销售人员的 ID 存储在一个文件中；销售数据存储在另一个文件中。销售数据采用以下形式：

```
salesPersonID  month  saleAmount
.
.
.
```

此外，销售数据没有特定顺序；它不是按 ID 排序的。

销售数据示例如下：

```
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
| **输入** | 一个文件，包含每个销售人员的 ID；第二个文件包含销售数据。 |
| **输出** | 一个文件，包含上述格式的年度销售报告。 |

### 问题分析与算法设计

根据问题需求，很明显每位销售人员的主要组成部分是销售人员的 ID、各季度销售金额和年度总销售金额。由于这些组成部分类型不同，我们可以借助 `struct` 将它们分组，定义如下：

```c
struct salesPersonRec
{
    string ID;       //salesperson's ID
    double saleByQuarter[4];    //array to store the total
                                 //sales for each quarter
    double totalSale;  //salesperson's yearly sales amount
};
```

由于有六名销售人员，我们使用一个包含六个分量的数组，其中每个分量的类型都是 salesPersonRec，定义如下：

```c
salesPersonRec salesPersonList[NO_OF_SALES_PERSON];
```

其中 NO_OF_SALES_PERSON 的值为 6。

由于程序要求我们找出公司每个季度的总销售额，我们需要一个包含四个分量的数组来存储数据。注意，这些数据将用于确定销售额最高的季度。因此，程序还需要以下数组：

```c
double totalSaleByQuarter[4];
```

回想一下，在 C++ 中，数组索引从 0 开始。因此，totalSaleByQuarter[0] 存储第 1 季度的数据，totalSaleByQuarter[1] 存储第 2 季度的数据，依此类推。

我们将在整个讨论中引用这些变量。

数组 salesPersonList 如图 10-9 所示。

![](img/f97f778697507bb6fdd80c5991210cba_623_0.png)

**图 10-9** 数组 `salesPersonList`

程序的第一步是将销售人员的 ID 读入数组 salesPersonList，并将每位销售人员的各季度销售额和总销售额初始化为 0。完成这一步后，数组 salesPersonList 如图 10-10 所示。

![](img/f97f778697507bb6fdd80c5991210cba_623_1.png)

**图 10-10** 初始化后的数组 `salesPersonList`

下一步是处理销售数据。处理销售数据相当直接。对于包含销售数据的文件中的每个条目：

- 1. 读取销售人员的 ID、月份以及该月的销售金额。
- 2. 搜索数组 `salesPersonList`，定位与该销售人员对应的分量。
- 3. 确定该月份对应的季度。
- 4. 通过加上该月的销售金额来更新该季度的销售额。

处理完销售数据文件后：

- 1. 计算每位销售人员的总销售额。
- 2. 计算每个季度的总销售额。
- 3. 打印报告。

上述讨论转化为以下算法：

- 1. 初始化数组 `salesPersonList`。
- 2. 处理销售数据。
- 3. 计算每个季度的总销售额。
- 4. 计算每位销售人员的总销售额。
- 5. 打印报告。
- 6. 计算并打印每位销售人员的最高销售额。
- 7. 计算并打印每个季度的最高销售额。

为了降低主程序的复杂性，让我们为这七个步骤分别编写一个单独的函数。

### 函数 initialize

该函数从输入文件中读取销售人员的 ID，并将销售人员的 ID 存储在数组 `salesPersonList` 中。它还将每位销售人员的季度销售金额和总销售金额初始化为 0。该函数的定义是：

```c
void initialize(ifstream& indata, salesPersonRec list[],
                 int listSize)
{
    int index;
    int quarter;

    for (index = 0; index < listSize; index++)
    {
        indata >> list[index].ID; //get salesperson's ID

        for (quarter = 0; quarter < 4; quarter++)
            list[index].saleByQuarter[quarter] = 0.0;

        list[index].totalSale = 0.0;
    }
} //end initialize
```

### 函数 `getData`

该函数从输入文件中读取销售数据，并将相应信息存储在数组 `salesPersonList` 中。该函数的算法是：

- 1. 读取销售人员的 ID、月份以及该月的销售金额。
- 2. 搜索数组 `salesPersonList`，定位与该销售人员对应的分量。（由于销售人员的 ID 未排序，我们将使用顺序搜索来搜索该数组。）
- 3. 确定该月份对应的季度。
- 4. 通过加上该月的销售金额来更新该季度的销售额。

假设读取到的条目是：

```
57373 2 350
```

这里，销售人员的 ID 为 57373，月份为 2，销售金额为 350。假设数组 `salesPersonList` 如图 10-11 所示。

![](img/f97f778697507bb6fdd80c5991210cba_625_0.png)

**图 10-11** 数组 `salesPersonList`

现在，ID 57373 对应数组分量 `salesPersonList[3]`，月份 2 对应第 1 季度。因此，将 350 加到 354.80 上，得到新金额 704.80。处理该条目后，数组 `salesPersonList` 如图 10-12 所示。
