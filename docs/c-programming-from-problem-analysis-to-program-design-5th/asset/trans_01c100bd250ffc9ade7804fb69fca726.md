
## 编程示例：销售数据分析

一家公司有六名销售人员。每个月，他们都会出差销售公司的产品。每月月底，每名销售人员的总销售额连同该销售人员的 ID 和月份一起记录在一个文件中。每年年底，公司经理希望看到以下表格格式的报告：

| ID | QT1 | QT2 | QT3 | QT4 | 总计 |
|---:|---:|---:|---:|---:|---:|
| 12345 | 1892.00 | 0.00 | 494.00 | 322.00 | 2708.00 |
| 32214 | 343.00 | 892.00 | 9023.00 | 0.00 | 10258.00 |
| 23422 | 1395.00 | 1901.00 | 0.00 | 0.00 | 3296.00 |
| 57373 | 893.00 | 892.00 | 8834.00 | 0.00 | 10619.00 |
| 35864 | 2882.00 | 121.00 | 0.00 | 1223.00 | 5326.00 |
| 54654 | 893.00 | 0.00 | 392.00 | 3420.00 | 4705.00 |
| 总计 | 8298.00 | 4906.00 | 18743.00 | 4965.00 |  |

销售人员最高销售额：ID = 57373，金额 = $10619.00

季度最高销售额：季度 = 3，金额 = $18743.00

在本报告中，QT1 表示第 1 季度（第 1 至 3 月），QT2 表示第 2 季度（第 4 至 6 月），QT3 表示第 3 季度（第 7 至 9 月），QT4 表示第 4 季度（第 10 至 12 月）。

销售人员的 ID 存储在一个文件中；销售数据存储在另一个文件中。销售数据采用以下形式：

```
salesPersonID  month  saleAmount
.
.
.
```

此外，销售数据没有特定顺序；它不是按 ID 排序的。

示例销售数据为：

```
12345 1 893
32214 1 343
23422 3 903
57373 2 893
.
.
.
```

![](img/1fbe55537254baeb2b5b7dbaf64956ae_670_0.png)

**图 11-9** 数组 salesPersonList

程序的第一步是将销售人员的 ID 读入数组 salesPersonList，并将每名销售人员的季度销售额和总销售额初始化为 0。完成这一步后，数组 salesPersonList 如图 11-10 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_670_1.png)

**图 11-10** 初始化后的数组 salesPersonList

下一步是处理销售数据。处理销售数据非常直接。对于包含销售数据的文件中的每条记录：

- 1. 读取销售人员的 ID、月份以及该月的销售额。
- 2. 在数组 salesPersonList 中搜索，定位与该销售人员对应的分量。
- 3. 确定该月份对应的季度。
- 4. 通过加上该月的销售额来更新该季度的销售额。

销售数据文件处理完毕后：

- 1. 计算每名销售人员的总销售额。
- 2. 计算每个季度的总销售额。
- 3. 打印报告。

上述讨论转化为以下算法：

- 1. 初始化数组 salesPersonList。
- 2. 处理销售数据。
- 3. 计算每个季度的总销售额。
- 4. 计算每名销售人员的总销售额。
- 5. 打印报告。
- 6. 计算并打印每名销售人员的最高销售额。
- 7. 计算并打印每个季度的最高销售额。

为降低主程序的复杂性，让我们为这七个步骤分别编写一个单独的函数。

### 函数 initialize

该函数从输入文件中读取销售人员的 ID，并将该销售人员的 ID 存储在数组 salesPersonList 中。它还会将每名销售人员的季度销售额和总销售额初始化为 0。该函数的定义如下：

```cpp
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

该函数从输入文件中读取销售数据，并将相应信息存储在数组 `salesPersonList` 中。该函数的算法如下：

- 1. 读取销售人员的 ID、月份以及该月的销售额。
- 2. 在数组 `salesPersonList` 中搜索，定位与该销售人员对应的分量。（由于销售人员的 ID 未排序，我们将使用顺序搜索来搜索该数组。）
- 3. 确定该月份对应的季度。
- 4. 通过加上该月的销售额来更新该季度的销售额。

假设读取到的记录为：

```
57373 2 350
```

这里，销售人员的 ID 为 57373，月份为 2，销售额为 350。假设数组 `salesPersonList` 如图 11-11 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_672_0.png)

**图 11-11** 数组 `salesPersonList`

现在，ID 57373 对应数组分量 `salesPersonList[3]`，月份 2 对应第 1 季度。因此，将 350 加到 354.80 上，得到新金额 704.80。处理完该记录后，数组 `salesPersonList` 如图 11-12 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_673_0.png)

**图 11-12** 处理记录 57373 2 350 后的数组 `salesPersonList`

函数 getData 的定义如下：

```cpp
void getData(ifstream& infile, salesPersonRec list[],
             int listSize)
{
    int index;
    int quarter;
    string sID;
    int month;
    double amount;

    infile >> sID;        //get salesperson’s ID

    while (infile)
    {
        infile >> month >> amount;  //get the sale month and
                                    //the sale amount

        for (index = 0; index < listSize; index++)
            if (sID == list[index].ID)
                break;

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

        infile >> sID;
    } //end while
} //end getData
```

### 函数 saleByQuarter

该函数计算公司每个季度的总销售额。要计算每个季度的总销售额，我们将每名销售人员在该季度的销售额相加。显然，该函数必须能够访问数组 salesPersonList，以便计算每个 totalSaleByQuarter。该函数还需要知道每个数组的行数。因此，该函数有三个参数。该函数的定义如下：

```cpp
void saleByQuarter(salesPersonRec list[], int listSize,
                   double totalByQuarter[])
{
    int quarter;
    int index;

    for (quarter = 0; quarter < 4; quarter++)
        totalByQuarter[quarter] = 0.0;

    for (quarter = 0; quarter < 4; quarter++)
        for (index = 0; index < listSize; index++)
            totalByQuarter[quarter] +=
                list[index].saleByQuarter[quarter];
} //end saleByQuarter
```

### 函数 totalSaleByPerson

该函数计算每名销售人员的年度销售额。要计算某名员工的年度销售额，我们将该员工四个季度的销售额相加。显然，该函数必须能够访问数组 salesPersonList。该函数还需要知道数组的大小。因此，该函数有两个参数。

该函数的定义如下：

```cpp
void totalSaleByPerson(salesPersonRec list[], int listSize)
{
    int index;
    int quarter;

    for (index = 0; index < listSize; index++)
        for (quarter = 0; quarter < 4; quarter++)
            list[index].totalSale +=
                list[index].saleByQuarter[quarter];
} //end totalSaleByPerson
```

### 函数 printReport

该函数按指定格式打印年度报告。printReport 伪代码中的算法如下：

- 1. 打印标题——即输出的前三行。
- 2. 打印每名销售人员的数据。
- 3. 打印表格的最后一行。

请注意，接下来的两个函数将生成输出的最后两行。

显然，printReport 函数必须能够访问数组 salesPersonList 和数组 totalSaleByQuarter。此外，由于输出将存储在文件中，该函数必须能够访问与输出文件关联的 ofstream 变量。因此，该函数有四个参数：一个对应于数组 salesPersonList 的参数，一个对应于数组 totalSaleByQuarter 的参数，一个指定数组大小的参数，以及一个对应于 ofstream 变量的参数。该函数的定义如下：

```cpp
void printReport (ofstream& outfile, salesPersonRec list[],
                 int listSize, double saleByQuarter[])
{
    int index;
    int quarter;

    outfile << "----------- Annual Sales Report -----------"
            << "----------------" << endl;
    outfile << endl;
    outfile << " ID          QT1          QT2          QT3          "
            << "QT4       Total" << endl;
    outfile << "-----------------------------------------------" << endl;

    for (index = 0; index < listSize; index++)
    {
        outfile << list[index].ID << "  ";

        for (quarter = 0; quarter < 4; quarter++)
            outfile << setw(10)
                    << list[index].saleByQuarter[quarter];

        outfile << setw(10) << list[index].totalSale << endl;
    }
    outfile << "Total  ";
```
