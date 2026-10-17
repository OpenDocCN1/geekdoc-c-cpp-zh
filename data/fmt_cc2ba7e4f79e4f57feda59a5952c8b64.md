
```cpp
    if (!infile) {
        cout << "Cannot open input file." << endl;
        return 1;
    }
    cout << "Enter output file name: ";
    cin >> outputFile;
    cout << endl;

    outfile.open(outputFile.c_str());
    outfile << fixed << showpoint << setprecision(2);

    getData(infile, salesPersonList, NO_OF_SALES_PERSON);
    saleByQuarter(salesPersonList, NO_OF_SALES_PERSON, totalByQuarter);
    totalSaleByPerson(salesPersonList, NO_OF_SALES_PERSON);
    printReport(outfile, salesPersonList, NO_OF_SALES_PERSON, totalByQuarter);
    maxSaleByPerson(outfile, salesPersonList, NO_OF_SALES_PERSON);
    maxSaleByQuarter(outfile, totalByQuarter);

    infile.close();
    outfile.close();

    return 0;
}
```
示例运行: 在此示例中，输入如下。
Enter salesperson ID name: `Ch11_ID.txt`
Enter sales data file name: `Ch11_SalesData.txt`
Enter output file name: `Ch11_SalesAnalysis.txt`

# 681 | 输入文件：销售人员 ID
12345
32214
23422
57373
54654

# 输入文件：销售人员数据
12345 1 893
32214 1 343
23422 2 903
57373 5 329
35864 9 392
54654 2 999
12345 2 999
32214 4 892
23422 4 895
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

# 年度销售报告

| ID | QT1 | QT2 | QT3 | QT4 | Total |
|---|---|---|---|---|---|
| 12345 | 1892.00 | 0.00 | 494.00 | 322.00 | 2708.00 |
| 32214 | 343.00 | 892.00 | 9023.00 | 0.00 | 10258.00 |
| 23422 | 1395.00 | 1901.00 | 0.00 | 0.00 | 3296.00 |
| 57373 | 893.00 | 892.00 | 8834.00 | 0.00 | 10619.00 |
| 35864 | 2882.00 | 1221.00 | 0.00 | 1223.00 | 5326.00 |
| 54654 | 893.00 | 0.00 | 392.00 | 3420.00 | 4705.00 |
| Total | 8298.00 | 4906.00 | 18743.00 | 4965.00 | |

## 快速回顾

- 1. 结构体（`struct`）是固定数量组件的集合。
- 2. 结构体的组件可以是不同的类型。
- 3. 定义结构体的语法如下：
```cpp
struct structName
{
  dataType identifier1;
  dataType identifier2;
  ...
  dataType identifiern;
}
```
- 4. 在 C++ 中，`struct` 是一种定义；在声明结构体时不会分配内存。
- 5. 在 C++ 中，`struct` 是一种定义；在声明结构体变量时，会为结构体变量分配内存。
- 6. 结构体的组件被称为结构体的成员（members）。
- 7. 结构体的组件通过名称进行访问。
- 8. 在 C++ 中，点运算符 (`.`) 用于访问成员访问运算符。
- 9. 使用点运算符 (`.`) 通过名称访问结构体的成员变量。例如，如果 `employeeType` 是一个结构体，`employee` 是一个 `employeeType` 类型的变量，那么表达式 `employeeType.name` 访问的是成员 name。也就是说，`employee.name` 是一个变量，可以被其他变量操作。
- 10. 结构体的内置操作是赋值和成员访问操作。
- 11. 结构体不允许进行算术运算或关系运算。
- 12. 作为函数的参数，结构体既可以按值传递，也可以按引用传递。
- 13. 函数可以返回 `struct` 类型的值。
- 14. 结构体可以是另一个结构体的成员。

# 练习题

- 1. 判断以下陈述的对错（true 或 false）。
  a. 结构体的所有成员都必须是不同的类型。
  b. 函数不能返回 `struct` 类型的值。
  c. 结构体的成员可以是另一个结构体。
  d. 结构体上允许的操作仅限于赋值和成员选择。
  e. 数组可以是结构体的成员。
  f. 在 C++ 中，允许对结构体进行某些聚合操作。
  g. 因为结构体具有有限数量的组件，所以允许对结构体进行关系运算。

- 2. 定义结构体 `checkingAccount`，用于存储支票账户的数据：持户人姓名（`string`）、账号（`int`）、余额（`double`）和利率（`double`）。

- 3. 假设练习 2 的定义。声明一个 `checkingAccount` 变量，并编写 C++ 语句存储以下信息：持户人姓名—Jason Miller，账号—17328910，余额—24476.38，利率—2.5%。

- 4. 定义结构体 `movieType`，用于存储电影的数据：电影名称（`string`）、导演（`string`）、制片人（`string`）、上映年份（`int`）以及库存数量。

- 5. 假设练习 4 的定义。声明一个 `movieType` 类型的变量来存储数据：电影名称—Summer Vacation，导演—Tom Blair，制片人—Rajiv Merchant，上映年份—2005，数量—34。

- 6. 考虑以下语句：

```cpp
struct nameType {
    struct dataType {
        struct personalInfoType {
            string first; int month;
            string last; int day;
            int year; int pID;
            dateType dob;
        };
        personalInfoType person;
        personalInfoType classList[100];
    };
    nameType student;
}
```

判断以下陈述是有效（valid）还是无效（invalid）。如果陈述无效，请解释原因。

a. `person.name.first = "William";`
b. `cout << person.name << endl;`
c. `classList[1] = person;`
d. `classList[20].pID = 00001100;`
e. `person = classList[20];`
f. `student = person.name;`
g. `cin >> student;`
h. `for (int j = 0; j < 100; j++)`
    `classList[j].pID = 00000000;`
i. `classList.dob.day = 1;`
j. `student = name;`

- 7. 考虑以下语句（`nameType` 如练习 6 中定义）：

```cpp
struct employeeType
{
    nameType name;
    int performanceRating;
    int pID;
    string dept;
    double salary;
}
```

a. `newEmployee.name = "John Smith";`
b. `cout << newEmployee.name;`
c. `employees[35] = newEmployee;`
d. `if (employees[45].pID == 555334444)`
    `employees[45].performanceRating = 1;`
e. `employees.salary = 0;`

- 8. 假设练习 6 和 7 的声明。为以下内容编写 C++ 语句：

a. 在 `newEmployee` 中存储以下信息：
    name: Mickey Doe
    pID: 111111111
    performanceRating: 2
    dept: ACCT
    salary: 34567
b. 将 `employees` 数组中的每个 `performanceRating` 初始化为 0。
c. 将 `employees` 中的第 20 个元素拷贝到 `newEmployee`。
d. 更新 `employees` 中第 50 个元素的 `salary`，增加 35。

- 9. 假设有如下结构体定义：

```cpp
struct partsType
{
    string partName;
    int partNum;
    double price;
    int quantitiesStock;
}
```

声明一个包含 100 个 `partsType` 组件的数组 `inventory`。

- 10. 假设定义 9。
  a. 编写 C++ 代码初始化 `inventory`：`partName` 为空字符串，`partNum` 为 -1，`price` 为 0.0，`quantitiesStock` 为 0。
  b. 编写使用循环输出数据的 C++ 代码。

- 11. 假设定义和声明。编写一个可以向 `inventory` 输入数据的 void 函数。

- 12. 假设你有如下定义：

```cpp
struct timeType
{
    int hr;
    int min;
    int sec;
    string cityName;
}
```

a. 声明一个 `timeType` 变量。
b. 编写 C++ 语句输出：`cityName`—Chicago，550 英里，`travelTime`—9 小 30 分钟。
c. 编写输出 `timeType` 变量数据的函数定义。
d. 编写一个返回值的函数输入数据。
e. 编写一个带有 `timeType` 参数的 void 函数输入数据。

# 编程题

- 1. 假设练习 4 的定义，编写一个声明 `movieType` 变量、提示用户输入数据并输出电影数据的程序。

- 2. 编写一个读取学生姓名及其成绩的程序。程序应输出每个学生的姓名和等级。它还需要找到最高分以及获得最高分的学生姓名。学生数据应存储在结构体 `studentType` 中，该结构体包含四个组件：`string firstName`、`lastName`、`int testScore`（0-100）和 `char grade`。假设班有 20 个学生。使用一个包含 20 个 `studentType` 组件的数组。你的程序至少包含以下函数：

  a. 将学生数据读入数组。
  b. 为每个学生分配相应的等级。
  c. 寻找最高分的函数。
  d. 打印最高分学生姓名的函数。你的程序必须以这种格式输出姓名：姓、逗号、空格、名；姓名必须左对齐。此外，除了声明变量和打开输入输出文件外，`main` 函数应该只是函数的集合。

- 3. 定义结构体 `menuItem`，包含两个组件：`string` 自己的 `menuName` 和 `double` 自己的 `menuPrice`。

- 4. 编写一个程序帮助当地餐厅自动化其账单系统。程序应执行以下操作：

  a. 向顾客展示餐厅不同的项目。
  b. 允许客户从菜单中选择多个项目。
  c. 计算并打印账单。

假设餐厅提供以下早餐（每个项目的价格在右侧）：

| 项目 | 价格 |
| :--- | :--- |
| 普通煎蛋 | $1.45 |
| 培根蛋 | $2.45 |
| 麦芬 | $0.99 |
| 法式吐司 | $1.99 |
| 水果篮 | $2.49 |
| 麦片 | $0.69 |
| 咖啡 | $0.50 |
| 茶 | $0.75 |

使用编程题 2 中定义的 `menuItemType` 类型数组 `menuList`。你的程序至少包含以下函数：

* `getData`: 该函数将数据加载到数组中。
* `showMenu`: 该函数显示餐厅提供的不同项目并告诉用户如何选择项目。

# 编程练习题 | 647

- 函数 `printCheck`：此函数计算并打印账单。
（注意，账金额应包含 5% 的税费。）示例输出如下：

```
Welcome to Johnny's Restaurant
Bacon and Egg $2.45
Muffin $0.99
Coffee $0.50
Tax $0.20
Amount Due $4.14
```

输出格式保留两位小数。输出中每个项的名称必须左对齐。你可以假设用户只选择特定类型中的某一项。

- 重新做第 4 题，使用户可以选择特定类型的多个项。在这种情况下，示例输出如下：

```
Welcome to Johnny's Restaurant
Bacon and Egg $2.45
Muffin $1.98
Coffee $0.50
Tax $0.25
Amount Due $5.18
```

- 编写一个程序，其 `main` 函数仅作为变量声明和函数调用的集合。该程序读取文本并输出字母及其计数，如 `printResult` 函数中解释的那样。（不能有全局变量！所有信息必须在函数之间传递。使用结构体（`struct`）来存储信息。）你的程序必须至少包含以下函数：

- 函数 `FunctionFile`：打开输入和输出文件。你必须将文件流作为参数传递（当然是通过引用传递）。如果文件不存在，程序应打印适当的消息并退出。程序必须询问用户输入和输出文件的名称。

- 函数 `count`：统计 `FunctionFile` 中打开的文本文件中，每个大写字母 A-Z 和小写字母 a-z 的出现次数。这些信息必须存入一个结构体数组中。该数组必须作为参数传递，文件标识符也必须作为参数传递。

- 函数 `printResult`：打印大写字母和小写字母的数量，以及每个字母 A-Z 的大写百分比和每个字母 a-z 的小写百分比。百分比格式应为：“25%”。这些信息必须来自结构体数组，该数组必须作为参数传递。

- 7. 编写一个程序，声明一个 `struct` 来存储棒球球员的数据（球员姓名、全垒数和击打数）。声明一个包含 10 个元素的数组来存储 10 名棒球球员的数据。你的程序必须包含一个输入数据的函数和一个输出数据的函数。添加函数来搜索数组以找到特定球员的索引，并更新球员的数据。（你可以假设输入数据存储在文件中。）在程序终止之前，给用户保存数据到文件的选项。你的程序应该是菜单驱动的，为用户提供各种选择。

# 第 12 章
# 类与数据抽象

在本章中，你将：

- 学习类（`classes`）
- 学习类的私有（`private`）、保护（`protected`）和公共（`public`）成员
- 探索类的实现方式
- 研究构造函数和析构函数
- 学习抽象数据类型（ADT）
- 探索如何使用类来实现 ADT
- 学习信息隐藏
- 探索在 C++ 中如何实现信息隐藏
- 学习类的静态成员

在第 11 章中，你学习了如何使用 `struct` 对一组不同类型的数据项进行分组。第 11 章给出的 `struct` 定义与类的定义相似。然而，C++ `struct` 的成员既可以是数据项，也可以是函数。C++ 提供了另一种结构化数据类型——类，它被专门设计用于分组数据和函数。本章首先介绍了类，并解释了如何使用它们，然后讨论了 `struct` 和类之间的相似之处和区别。

> 第 11 章是本章的先知识。事实上，正如本章“`struct` 与类”节节讨论的，`struct` 和类具有相似的能力。

## 类

第 1 章引入了称为面向对象设计（OOD）的问题解决方法。在 OOD 中，第一步是识别组件，称为“对象”。对象将数据和对该数据的操作组合在一个单一单元中。在 C++ 中，允许你将数据和对数据的操作组合在单一单元中的机制被称为类。现在你已经知道如何在计算机内存中存储和操作数据，以及如何构建自己的函数，你准备好学习对象是如何构造的。本章及后续章节将使用 OOD 开发并实现程序。本章首先解释了如何定义一个类并在程序中使用它。

类是固定数量组件的集合。类的组件被称为类的成员。

定义类的通用语法如下：

```
class Identifier
{
    classMembersList
};
```
