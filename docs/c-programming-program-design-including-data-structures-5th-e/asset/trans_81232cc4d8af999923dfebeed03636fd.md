

```cpp
    if (!infile)                                              //Step 11
    {
        cout << "Cannot open the input file."
             << endl;
        return 1;
    }

    cout << "Enter the output file name: ";                   //Step 12
    cin >> outputFile;                                        //Step 13
    cout << endl;

    outfile.open(outputFile.c_str());                         //Step 14
    outfile << fixed << showpoint
            << setprecision(2);                               //Step 15

    getData(infile, salesPersonList,
            NO_OF_SALES_PERSON);                              //Step 16
    saleByQuarter(salesPersonList,
                  NO_OF_SALES_PERSON,
                  totalSaleByQuarter);                        //Step 17
    totalSaleByPerson(salesPersonList,
                      NO_OF_SALES_PERSON);                    //Step 18

    printReport(outfile, salesPersonList,
                NO_OF_SALES_PERSON,
                totalSaleByQuarter);                          //Step 19
    maxSaleByPerson(outfile, salesPersonList,
                    NO_OF_SALES_PERSON);                      //Step 20
    maxSaleByQuarter(outfile, totalSaleByQuarter);            //Step 21

    infile.close();                                           //Step 22
    outfile.close();                                          //Step 22

    return 0;
}

//Place the definitions of the functions initialize,
//getData, saleByQuarter, totalSaleByPerson,
//printReport, maxSaleByPerson, and maxSaleByQuarter here.
```

## 示例运行

在此示例运行中，用户输入以底纹显示。

```text
Enter the salesPerson ID file name: Ch10_SalesManID.txt

Enter the sales data file name: Ch10_SalesData.txt

Enter the output file name: Ch10_SalesDataAnalysis.txt
```

### 输入文件：销售人员的 ID

```text
12345
32214
23422
57373
35864
54654
```

### 输入文件：销售人员的数据

```text
12345 1 893
32214 1 343
23422 3 903
57373 2 893
35864 5 329
54654 9 392
12345 2 999
32214 4 892
23422 4 895
23422 2 492
57373 6 892
35864 10 1223
54654 11 3420
12345 12 322
35864 5 892
54654 3 893
12345 8 494
32214 8 9023
23422 6 223
23422 4 783
57373 8 8834
35864 3 2882
```

### 年度销售报告

| ID | QT1 | QT2 | QT3 | QT4 | 总计 |
|---|---:|---:|---:|---:|---:|
| 12345 | 1892.00 | 0.00 | 494.00 | 322.00 | 2708.00 |
| 32214 | 343.00 | 892.00 | 9023.00 | 0.00 | 10258.00 |
| 23422 | 1395.00 | 1901.00 | 0.00 | 0.00 | 3296.00 |
| 57373 | 893.00 | 892.00 | 8834.00 | 0.00 | 10619.00 |
| 35864 | 2882.00 | 1221.00 | 0.00 | 1223.00 | 5326.00 |
| 54654 | 893.00 | 0.00 | 392.00 | 3420.00 | 4705.00 |
| 总计 | 8298.00 | 4906.00 | 18743.00 | 4965.00 | 36912.00 |

销售人员最高销售额：ID = 57373，金额 = $10619.00
季度最高销售额：季度 = 3，金额 = $18743.00

## 快速回顾

- 1. `struct` 是固定数量组件的集合。
- 2. `struct` 的组件可以具有不同的类型。
- 3. 定义 `struct` 的语法是：

```cpp
struct structName
{
    dataType1 identifier1;
    dataType2 identifier2;
    .
    .
    .
    dataTypen identifiern;
};
```

- 4. 在 C++ 中，`struct` 是保留字。
- 5. 在 C++ 中，`struct` 是一种定义；不会分配内存。只有在声明 `struct` 变量时，才会为其分配内存。
- 6. `struct` 的组件称为 `struct` 的成员。
- 7. `struct` 的组件通过名称访问。
- 8. 在 C++ 中，点（.）运算符称为成员访问运算符。
- 9. `struct` 的成员通过使用点（.）运算符访问。例如，如果 employeeType 是一个 `struct`，employee 是 employeeType 类型的变量，name 是 employee 的成员，那么表达式 employee.name 访问成员 name。也就是说，employee.name 是一个变量，可以像其他变量一样进行操作。
- 10. 对 `struct` 唯一的内置操作是赋值和成员访问操作。
- 11. 不允许对 `struct(s)` 进行算术运算或关系运算。
- 12. 作为函数的参数，`struct` 可以按值传递或按引用传递。
- 13. 函数可以返回 `struct` 类型的值。
- 14. 一个 `struct` 可以是另一个 `struct` 的成员。

## 练习

- 1. 将下列陈述标记为真或假。
    - a. `struct` 的所有成员必须具有不同的类型。
    - b. 函数不能返回 `struct` 类型的值。
    - c. `struct` 的成员可以是另一个 `struct`。
    - d. 对 `struct` 唯一允许的操作是赋值和成员选择。
    - e. 数组可以是 `struct` 的成员。
    - f. 在 C++ 中，允许对 `struct` 进行某些聚合操作。
    - g. 因为 `struct` 具有有限数量的组件，所以允许对 `struct` 进行关系运算。
- 2. 定义一个 `struct` `checkingAccount`，用于存储以下有关支票账户的数据：账户持有人姓名（`string`）、账号（`int`）、余额（`double`）和利率（`double`）。
- 3. 假设采用练习 2 中的定义。声明一个 `checkingAccount` 变量，并编写 C++ 语句来存储以下信息：账户持有人姓名——Jason Miller，账号——17328910，余额——24476.38，利率——2.5%。
- 4. 定义一个 `struct` `movieType`，用于存储以下有关电影的数据：电影名称（`string`）、电影导演（`string`）、制片人（`string`）、电影发行年份（`int`）以及库存副本数量。
- 5. 假设采用练习 4 中的定义。声明一个 `movieType` 类型的变量来存储以下数据：电影名称——Summer Vacation，导演——Tom Blair，制片人——Rajvir Mechant，电影发行年份——2005，库存副本数量——34。
- 6. 考虑以下语句：

```cpp
struct nameType
{
    string first;
    string last;
};

struct dateType
{
    int month;
    int day;
    int year;
};

struct personalInfoType
{
    nameType name;
    int pID;
    dateType dob;
};

personalInfoType person;
personalInfoType classList[100];
nameType student;
```

将下列语句标记为有效或无效。如果语句无效，请解释原因。

    - a. `person.name.first = "William";`
    - b. `cout << person.name << endl;`
    - c. `classList[1] = person;`
    - d. `classList[20].pID = 000011100;`
    - e. `person = classList[20];`
    - f. `student = person.name;`
    - g. `cin >> student;`
    - h. `for (int j = 0; j < 100; j++) classList[j].pID = 00000000;`
    - i. `classList.dob.day = 1;`
    - j. `student = name;`

- 7. 考虑以下语句（nameType 如练习 6 中所定义）：

```cpp
struct employeeType
{
    nameType name;
    int performanceRating;
    int pID;
    string dept;
    double salary;
};
employeeType employees[100];
employeeType newEmployee;
```

将下列语句标记为有效或无效。如果语句无效，请解释原因。

    - a. `newEmployee.name = "John Smith";`
    - b. `cout << newEmployee.name;`
    - c. `employees[35] = newEmployee;`
    - d. 
```cpp
if (employees[45].pID == 55533444)
    employees[45].performanceRating = 1;
```
    - e. `employees.salary = 0;`

- 8. 假设采用练习 6 和练习 7 中的声明。编写 C++ 语句以执行以下操作：
    - a. 将以下信息存储到 `newEmployee` 中：

```text
name: Mickey Doe
pID: 11111111
performanceRating: 2
dept: ACCT
salary: 34567.78
```

    - b. 在数组 `employees` 中，将每个 `performanceRating` 初始化为 0。
    - c. 将数组 `employees` 第 20 个组件的信息复制到 `newEmployee` 中。
    - d. 将数组 `employees` 中第 50 名员工的工资在其先前值上增加 5735.87。

- 9. 假设你有以下 `struct` 的定义。

```cpp
struct partsType
{
    string partName;
    int partNum;
    double price;
    int quantitiesInStock;
};
```

声明一个数组 `inventory`，包含 100 个 `partsType` 类型的组件。

