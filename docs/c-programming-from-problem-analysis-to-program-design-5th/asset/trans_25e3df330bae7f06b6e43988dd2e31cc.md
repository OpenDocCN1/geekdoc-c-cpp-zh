
假设一个 `struct` 有几个需要大量内存来存储数据的数据成员，而你需要按值传递该结构体类型的变量。相应的形参随后会接收该变量数据的一份副本。编译器随后必须为形参分配内存，以便复制实参的值。除了大量存储空间外，此操作可能还需要相当多的计算机时间，才能将实参的值复制到形参中。

另一方面，如果变量按引用传递，形参只接收实参的地址。因此，将变量作为参数传递的一种高效方式是按引用传递。如果变量按引用传递，那么当形参改变时，实参也会改变。然而，有时你并不希望函数能够改变实参的值。在 C++ 中，你可以按引用传递变量，同时仍然防止函数改变其值。这通过在形参声明中使用关键字 `const` 来实现，如函数 `seqSearch` 的定义所示。

同样，我们也可以重写排序、二分查找以及其他列表处理函数。

## 数组中的结构体

假设一家公司有 50 名全职员工。我们需要打印他们的月度工资单，并跟踪年初至今已向每位员工支付了多少钱。首先，让我们定义一名员工的记录：

```cpp
struct employeeType
{
    string firstName;
    string lastName;
    int personID;
    string deptID;
    double yearlySalary;
    double monthlySalary;
    double yearToDatePaid;
    double monthlyBonus;
};
```

每位员工都有以下成员（组成部分）：名字、姓氏、个人 ID、部门 ID、年薪、月薪、年初至今已支付金额和月度奖金。

由于我们有 50 名员工，且每位员工的数据类型相同，我们可以使用一个包含 50 个组成部分的数组来处理员工数据。

```cpp
employeeType employees[50];
```

这条语句声明了数组 employees，它包含 50 个 employeeType 类型的组成部分（见图 11-7）。employees 的每个元素都是一个结构体。例如，图 11-7 还展示了 employees[2]。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_663_0.png)

**图 11-7** 员工数组

假设我们还有以下声明：

```cpp
int counter;
```

此外，假设每位员工的初始数据——名字、姓氏、个人 ID、部门 ID 和年薪——都提供在一个文件中。为便于讨论，我们假设每位员工的数据都存储在一个文件中，例如 employee.dat。以下 C++ 代码将数据加载到 employees 数组中。我们假设最初 yearToDatePaid 为 0，并且月度奖金根据绩效每月确定。

```cpp
ifstream infile; //input stream variable
                 //assume that the file employee.dat has been opened
for (counter = 0; counter < 50; counter++)
{
    infile >> employees[counter].firstName
           >> employees[counter].lastName
           >> employees[counter].personID
           >> employees[counter].deptID
           >> employees[counter].yearlySalary;
    employees[counter].monthlySalary =
           employees[counter].yearlySalary / 12;
    employees[counter].yearToDatePaid = 0.0;
    employees[counter].monthlyBonus = 0.0;
}
```

假设对于某个月份，月度奖金已经存储在每位员工的记录中，而我们需要计算月度工资单并更新 yearToDatePaid 金额。以下循环计算并打印员工当月的工资单：

```cpp
double payCheck; // variable to calculate the paycheck

for (counter = 0; counter < 50; counter++)
{
    cout << employees[counter].firstName << " "
         << employees[counter].lastName << " ";

    payCheck = employees[counter].monthlySalary +
               employees[counter].monthlyBonus;

    employees[counter].yearToDatePaid =
                employees[counter].yearToDatePaid +
                payCheck;

    cout << setprecision(2) << payCheck << endl;
}
```

## 结构体中的结构体

你已经看到结构体和数组数据结构如何组合起来组织信息。你也看到了这样的示例：结构体的一个成员是数组，而数组类型是结构体。在本节中，你将了解在哪些情况下使用另一个结构体来组织结构体中的数据是有益的。

让我们考虑以下员工记录：

```cpp
struct employeeType
{
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
    int hireday;
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

如你所见，大量信息被塞进一个结构体中。这个结构体有 22 个成员。该结构体的一些成员会比其他成员更频繁地被访问，而一些成员之间的联系也比其他成员更紧密。此外，一些成员将具有相同的底层结构。例如，入职日期和离职日期都是 `int` 日期类型。让我们按如下方式重新组织这个 `struct`：

```cpp
struct nameType
{
    string first;
    string middle;
    string last;
};
```

```cpp
struct addressType
{
    string address1;
    string address2;
    string city;
    string state;
    string zip;
};
```

```cpp
struct dateType
{
    int month;
    int day;
    int year;
};
```

```cpp
struct contactType
{
    string phone;
    string cellphone;
    string fax;
    string pager;
    string email;
};
```

我们将员工的姓名、地址和联系方式类型分成了子类别。此外，我们定义了一个 `struct` dateType。让我们按如下方式重建员工记录：

```cpp
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

这个员工 `struct` 中的信息比之前的更容易管理。这个 `struct` 中的一部分可以复用来构建另一个 `struct`。例如，假设你想定义一名客户的记录。每位客户都有名字、姓氏和中间名，以及地址和联系方式。因此，你可以使用结构体 nameType、addressType、contactType 以及客户特有的成员，快速组合出客户记录。

接下来，让我们声明一个 employeeType 类型的变量，并讨论如何访问其成员。

考虑以下语句：

```cpp
employeeType newEmployee;
```

这条语句将 newEmployee 声明为 employeeType 类型的结构体变量（见图 11-8）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_666_0.png)

图 11-8 结构体变量 newEmployee

语句：

```cpp
newEmployee.salary = 45678.00;
```

将 newEmployee 的 salary 设置为 45678.00。以下语句：

```cpp
newEmployee.name.first = "Mary";
newEmployee.name.middle = "Beth";
newEmployee.name.last = "Simmons";
```

分别将 newEmployee 的名字、中间名和姓氏设置为 "Mary"、"Beth" 和 "Simmons"。注意，newEmployee 有一个名为 name 的成员。我们通过 newEmployee.name 访问该成员。还要注意，newEmployee.name 是一个结构体，并且有三个成员。我们应用成员访问规则来访问结构体 newEmployee.name 的成员 first。因此，newEmployee.name.first 就是我们存储名字的成员。

语句：

```cpp
cin >> newEmployee.name.first;
```

读取一个字符串并将其存储到 newEmployee.name.first 中。语句：

```cpp
newEmployee.salary = newEmployee.salary * 1.05;
```

更新 newEmployee 的 salary。

以下语句将 employees 声明为一个包含 100 个组成部分的数组，其中每个组成部分都是 employeeType 类型：

```cpp
employeeType employees[100];
```

for 循环：

```cpp
for (int j = 0; j < 100; j++)
    cin >> employees[j].name.first >> employees[j].name.middle
       >> employees[j].name.last;
```

读取 100 名员工的姓名并将其存储到数组 employees 中。因为 employees 是一个数组，所以要访问某个组成部分，我们使用索引。例如，employees[50] 是数组 employees 的第 51 个组成部分（回想一下，数组索引从 0 开始）。因为 employees[50] 是一个结构体，所以我们应用成员访问规则来选择特定的成员。

