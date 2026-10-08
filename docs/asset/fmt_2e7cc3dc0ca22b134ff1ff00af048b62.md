
```cpp
struct employeeType {
    string firstName;
    string middlename;
    string lastname;
    string empID;
    string address1;
    string address2;
    string city;
    string state;
    string zip;
    int hiremonth;
    int hiredday;
    int hireyear;
    int quitmonth;
    int quitday;
    int quityear;
    string phone;
    string cellphone;
    string fax;
    string pager;
    string email;
    string deptID;
    double salary;
};
```

你可以看到，很多信息被封装在一个结构体中。这个结构体有22个成员。该结构体的某些成员访问频率比其他成员更高，某些成员之间的关系更紧密。此外，某些成员具有相同的底层结构。例如，入职日期和离职日期类型都是 `int` 类型。让我们重新组织这个结构体：

```cpp
struct nameType {
    string first;
    string middle;
    string last;
};
```

```cpp
struct addressType {
    string address1;
    string address2;
    string city;
    string state;
    string zip;
};
```

```cpp
struct dataType {
    int month;
    int day;
    int year;
};
```

```cpp
struct contactType {
    string phone;
    string cellphone;
    string fax;
    string pager;
    string email;
};
```

我们把员工的名字、地址和联系类型分到了子类中。此外，我们定义了一个 `dataType` 结构体。让我们如下重新构建员工记录：

```cpp
struct employeeType {
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

这个员工结构体中的信息比之前的更容易管理。该结构体的某些部分可以被复用以构建另一个结构体。例如，假设你想定义一个客户记录。每位客户都有名字、姓氏和中间名，以及地址和联系方式。因此，你可以使用 `nameType`、`addressType` 和 `contactType` 结构体来组合出一个客户记录。接下来，让我们声明一个 `employeeType` 类型的变量并讨论如何访问它的成员。考虑以下语句：

```cpp
employeeType newEmployee;
```

该语句声明 `newEmployee` 为 `employeeType` 类型的结构体变量（见图 9-8）。

![](img/d998292a174f7bfd8a26bfbada3d454e_676_0)

语句：

`newEmployee.salary = 45678.00;`

将 `newEmployee` 的工资设置为 45678.00。语句：

`newEmployee.name.first = "Mary";`

`newEmployee.name.middle = "Beth";`

`newEmployee.name.last = "Simmons";`

将 `newEmployee` 的名字、中间名和姓氏分别设置为 "Mary"、Beth" 和 "Simmons"。注意 `newEmployee` 是一个结构体。通过点运算符访问此成员。注意 `newEmployee` 有三个成员。我们应用规则来访问特定成员。

# 编程示例：销售分析

公司有六名销售人员。他们每月外出推销产品。每月，每位销售人员的销售总额及其月份会记录在一个文件中。年底，经理希望以以下表格格式查看此报告：

年度销售报告

| ID | QT1 | QT2 | QT3 | QT4 | Total |
|---|---|---|---|---|---|
| 12345 | 1892.00 | 0.00 | 494.00 | 322.00 | 2708.00 |
| 32214 | 343.00 | 892.00 | 9023.00 | 0.00 | 10258.00 |
| 23422 | 1395.00 | 1901.00 | 0.00 | 0.00 | 3296.00 |
| 57373 | 893.00 | 892.00 | 8834.00 | 0.00 | 10619.00 |
| 35864 | 2882.00 | 1221.00 | 0.00 | 1223.00 | 5326.00 |
| 54654 | 893.00 | 0.00 | 392.00 | 3420.00 | 4705.00 |
| Total | 8298.00 | 4906.00 | 18743.00 | 4965.00 | 000.00 |

在本报告中，`QT1` 代表第一季度（第 1 到 3 月），`QT2` 代表第二季度（第 4 到 6 月），`QT3` 代表第三季度（第 7 到 9 月），而 `QT4` 代表第四季度（第 10 到 12 月）。

销售人员的 ID 存储在一个文件中；销售数据存储在另一个文件中。

销售数据按以下格式存储：

```
salesPersonID month saleAmount
```

此外，销售数据没有特定的特定的顺序；它们不是按 ID 排序的。

示例销售数据如下：

```
12345 1 893
32214 1 343
23422 3 903
57373 2 893
```

让我们写一个程序来按指定的格式生成输出。

**输入** 一个包含每个销售人员 ID 的文件和另一个包含大量销售数据的文件。

**输出** 一个包含上述格式的年度销售报告的文件。

根据问题要求，很明显，每个销售人员的主要组件是销售人员 ID、季度销售额和年度总销售额。由于这些组件的类型不同，我们可以借助结构体将它们分组，其定义如下：

```cpp
struct salesPersonRec
{
    string ID;               //销售人员的 ID
    double saleByQuarter[4];  //用于存储每个季度
                             //总销售额的数组
    double totalSale;        //销售人员的年度销售额
};
```

由于有六位销售人员，我们使用结构体数组，其中每个组件的类型均为 `salesPersonRec`，其定义如下：

`salesPersonRec salesPersonList[NO_OF_SALES_PERSON];`

其中 `NO_OF_SALES_PERSON` 的值为 6。

# 第 9 章：记录（结构体）

由于程序要求我们找到公司每个季度的总销售额，我们需要一个包含四个组件的数组来存储数据。注意，这些数据将用于确定确定销售额最高的季度。因此，程序还需要以下数组：

`double totalSaleByQuarter[4];`

回想在 C++ 中，数组索引从 0 开始。因此，`totalSaleByQuarter[0]` 存储第一季度的数据，`totalSaleByQuarter[1]` 存储第二季度的数据，以此此类推。

在整个讨论中，我们将引用这些变量。

数组 `salesPersonList` 如图 9-9 所示。

| salesPersonList | ID | saleByQuarter | totalSale |
|---|---|---|---|
| salesPersonList[0] |  |  |  |
| salesPersonList[1] |  |  |  |
| salesPersonList[2] |  |  |  |
| salesPersonList[3] |  |  |  |
| salesPersonList[4] |  |  |  |
| salesPersonList[5] |  |  |  |

图 9-9 数组 salesPersonList

程序的的第一步是将销售人员的 ID 读取到数组 `salesPersonList` 中，并将每个人的季度销售额和总销售额初始化为 0。在完成这一步后，数组 `salesPersonList` 如图 9-10 所示。

| salesPersonList | ID | saleByQuarter | totalSale |
|---|---|---|---|---|---|---|
| salesPersonList[0] | 12345 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| salesPersonList[1] | 32214 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| salesPersonList[2] | 23422 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| salesPersonList[3] | 57373 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| salesPersonList[4] | 35864 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| salesPersonList[5] | 54654 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |

图 9-10 初始化后的数组 salesPersonList

下一步是处理销售数据。处理销售数据非常直观。对于包含销售数据文件的中的每个条目：

1. 读取销售人员的 ID、月份以及该月的销售额。
2. 搜索数组 `salesPersonList` 以找到对应此销售人员的组件。
3. 确定月份对应的季度。
4. 通过加上该月的销售额来更新该季度的销售额。

一旦处理了销售文件：

1. 计算每个销售人员的总销售额。
2. 计算每个季度的总销售额。
3. 打印报告。

这些讨论转化为以下算法：

1. 初始化数组 `salesPersonList`。
2. 处理销售数据。
3. 计算每个季度的总销售额。
4. 计算每个销售人员的总销售额。
5. 打印报告。
6. 计算并打印每个销售人员的最大销售额。
7. 计算并打印每个季度的最大销售额。

为了降低主程序的复杂度，让我们为这些步骤中的每一个单独编写函数。函数 `initialize` 从文件中读取销售人员的 ID，并将每个人的季度销售额和总销售额初始化为 0。该函数的定义如下：

```cpp
void initialize(ifstream& indata, salesPersonRec list[], int listSize)
{
    for (int index = 0; index < listSize; index++) {
        indata >> list[index].ID; //销售人员的 ID
        for (int quarter = 0; quarter < 4; quarter++)
            list[index].saleByQuarter[quarter] = 0.0;
        list[index].totalSale = 0.0;
    }
}
```

函数 `getData` 从文件中读取销售数据并存储在数组中。该函数的算法如下：

1. 读取销售人员的 ID、月份以及该月的销售额。
2. 搜索数组 `salesPersonList` 以找到对应此销售人员的组件（因为销售人员不是排序的，我们将对数组进行顺序搜索）。
3. 确定月份对应的季度。
4. 通过加上该月的销售额来更新该季度的销售额。

假设条目是 `57373 2 350`。这里，ID 57373 对应数组组件 `salesPersonList[3]`，月份 2 对应第一季度。数组 `salesPersonList` 如图 9-11 所示。

# 编程示例：销售数据

| salesPersonList | ID | saleByQuarter | totalSale |
|---|---|---|---|
| salesPersonList[0] | 12345 | 0.0 | 0.0 |
| salesPersonList[1] | 32214 | 0.0 | 0.0 |
| salesPersonList[2] | 23422 | 0.0 | 0.0 |
| salesPersonList[3] | 57373 | 0.0 | 0.0 |
| salesPersonList[4] | 35864 | 0.0 | 0.0 |
| salesPersonList[5] | 54654 | 0.0 | 0.0 |

图 9-11 数组 salesPersonList

现在将 350 加上 354.80 以得到新金额 704.80。处理此条目后，数组 `salesPersonList` 如图 9-12 所示。

![](img/d9982a174f7bdd8a26bfada3d454e_682_0.png)

图 9-12 处理条目后的数组 salesPersonList

函数 `getData` 的定义为：

```cpp
void getData(ifstream& infile, salesPersonRec list[], int listSize)
{
    int index;
    int quarter;
    string SID;
    int month;
    double amount;

    infile >> SID; //获取销售人员的 ID

    while (infile)
    {
        infile >> month >> amount; //获取销售月份和
        //销售额

        for (index = 0; index < listSize; index++) {
            if (SID == list[index].ID)
                break;
        }

        if (1 <= month && month <= 3)
            quarter = 0;
        else if (4 <= month && month <= 6)
            quarter = 1;
        else if (7 <= month && month <= 9)
            quarter = 2;
        else
            quarter = 3;

        if (index < listSize)
            list[index].saleByQuarter[quarter] += amount;
        else
            cout << "Invalid salesperson's ID." << endl;

        infile >> SID;
    }
} //结束 getData
```

函数查找公司每个季度的总销售额。为了找到每个季度的总销售额，我们累加每个销售人员在该季度的金额。显然，此函数必须访问 `salesPersonList` 数组和 `totalSaleByQuarter` 数组。该函数还需要知道每个数组的行数。因此，该函数有三个参数。该函数的定义为：

```cpp
## 编程示例：销售数据分析 | 635
```

```cpp
void saleByQuarter(salesPersonRec list[], int listSize,
    double totalByQuarter[])
{
    for (int quarter = 0; quarter < 4; quarter++)
        totalByQuarter[quarter] = 0.0;
    for (int quarter = 0; quarter < 4; quarter++)
        for (int index = 0; index < listSize; index++)
            totalByQuarter[quarter] +=
                list[index].salesByQuarter[quarter];
} //end saleByQuarter
```

函数：此函数查找销售人员的年度总额。为了找到个人人员的年度销售总额，我们将该员工四个季度的销售额相加。显然，此函数必须访问数组 `salesPersonList`。此函数还需要知道数组的大小。此函数有两个参数。

该函数的定义为：

```cpp
void totalByPerson(salesPersonRec list[], int listSize)
{
    for (int index = 0; index < listSize; index++)
        for (int quarter = 0; quarter < 4; quarter++)
            list[index].totalSale +=
                list[index].salesByQuarter[quarter];
} //end totalByPerson
```
