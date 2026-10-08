
分配的内存足够存储 `style`、`numberOfBedrooms`、`numberOfBathrooms`、`numberOfCarsGarage`、`yearBuilt`、`finishedSquareFootage`、`price` 和 `tax`（见图 9-1）。

![](img/d998292a174f7bfd8a26bfbada354e662_0)

图 9-1 `newHouse`

所有版权 © 2018 Cengage 保留。未经许可不得复制、扫描或复印。

# 第 9 章：记录（结构体）

## 注意

你也可以在定义 `struct` 时声明变量。例如，考虑以下语句：

```cpp
struct houseType {
    string style;
    int numberOfBedrooms;
    int numberOfBathrooms;
    int numberOfCarsGarage;
    int yearBuilt;
    int finishedSquareFootage;
    double price;
    double tax;
};
```

这些语句定义了 `houseType` 结构体。通常，在程序中，定义 `struct` 之前会声明变量。在定义 `struct` 时，你也会声明一个 `struct` 变量，这样该 `struct` 就可以程序中随处使用。

## 访问 struct 成员

在数组中，你通过索引访问元素。在 `struct` 中，你使用点运算符（`.`）访问成员。`struct` 的语法如下：

```
structVariableName.memberName
```

`struct` 成员就像你通常对变量操作的那样。在 C++ 中，点被称为访问运算符。考虑以下语句：

```cpp
struct studentType {
    string firstName;
    string lastName;
    char courseGrade;
    int testScore;
    int programmingScore;
    double GPA;
};

studentType newStudent;
```

假设你想将 `newStudent` 的 `GPA` 初始化为 0.0。以下语句实现了：

```cpp
newStudent.GPA = 0.0;
```

同样，语句：

```cpp
newStudent.firstName = "John";
newStudent.lastName = "Brown";
```

将 `"John"` 存入 `newStudent` 的 `firstName`，将 `"Brown"` 存入 `lastName`。执行这些语句后，`newStudent` 所示如图 9-2。

![](img/d998292a174f7bfd8a26bfbada354e662_0)

图 9-2 `newStudent`

语句：

```cpp
cin >> newStudent.firstName;
```

从标准输入读取新字符串并存入 `newStudent.firstName`。

语句：

```cpp
cin >> newStudent.testScore >> newStudent.programmingScore;
```

从键盘读取两个整数值分别存入 `newStudent.testScore` 和 `newStudent.programmingScore`。假设 `score` 是 `int` 类型变量。语句：

```cpp
score = (newStudent.testScore + newStudent.programmingScore) / 2;
```

将 `newStudent.testScore` 和 `newStudent.programmingScore` 的平均值赋给 `score`。以下语句确定 `own` 并存入 `newStudent.courseGrade`：

```cpp
if (score >= 90)
newStudent.courseGrade = 'A';
else if (score >= 80)
newStudent.courseGrade = 'B';
else if (score >= 70)
newStudent.courseGrade = 'C';
else if (score >= 60)
newStudent.courseGrade = 'D';
else
newStudent.courseGrade = 'F';
```

## 示例 9-1

考虑上一节中的 `struct` 定义以及以下语句：

```cpp
houseType ryanHouse;
houseType anitaHouse;
ryanHouse.style = "Colonial";
ryanHouse.numOfBedrooms = 3;
ryanHouse.numOfBaths = 2;
ryanHouse.numOfCarsGarage = 2;
ryanHouse.yearBuilt = 2005;
ryanHouse.finishedSquareFootage = 2250;
ryanHouse.price = 290000;
ryanHouse.tax = 5000.50;
```

前两个语句声明 `ryanHouse` 和 `anitaHouse` 为 `houseType` 变量。接下来的八条语句将字符串 `"Colonial"` 存入 `ryanHouse.style`，`3` 存入 `ryanHouse.numOfBedrooms`，`2` 存入 `ryanHouse.numOfBaths`，以此此类推。

接下来，考虑以下语句：

```cpp
cin >> anitaHouse.numOfBedrooms >> anitaHouse.price;
```

如果输入是：

Ranch 4 350000

那么字符串 `"Ranch"` 被存储在 `anitaHouse.style` 中，`4` 被存储在 `anitaHouse.numOfBedrooms` 中，`350000` 被存储在 `anitaHouse.price` 中。

## 赋值

我们可以使用赋值语句将一个结构体变量的值赋予另一个相同类型的结构体变量。假设 `newStudent` 如图 9-3 所示。

| newStudent | |

|---|---|

| firstName | Lisa |

| lastName | Robinson |

| courseGrade | A |

| testScore | 95 |

| programmingScore | 98 |

| GPA | 3.9 |

图 9-3 结构体 `newStudent`

语句：

```
student = newStudent;
```

将 `newStudent` 的内容复制到 `student` 中。在执行此赋值语句后，`student` 的值如图 9-4 所示。

| student | |

|---|---|

| firstName | Lisa |

| lastName | Robinson |

| courseGrade | A |

| testScore | 95 |

| programmingScore | 98 |

| GPA | 3.9 |

图 9-4 `student = newStudent` 后的 `student`

618 | 第 9 章：记录（结构体）

事实上，赋值语句：

```
student = newStudent;
```

等同于下述语句：

```
student.firstName = newStudent.firstName;
student.lastName = newStudent.lastName;
student.courseGrade = newStudent.courseGrade;
student.testScore = newStudent.testScore;
student.programmingScore = newStudent.programmingScore;
student.GPA = newStudent.GPA;
```

## 比较（关系运算符）

要比较结构体变量，需要逐成员地进行比较。与数组一样，结构体上不执行任何聚合关系操作。例如，假设 `newStudent` 和 `student` 如上所示已声明。此外，假设你想检查 `student` 和 `newStudent` 是否指向同一个学生。现在，如果 `newStudent` 和 `student` 具有相同的名字和姓氏，它们就指向同一个学生。要比较这些值，你必须逐成员地比较，如下所示：

```
if (student.firstName == newStudent.firstName &&
student.lastName == newStudent.lastName)
```

...

虽然你可以使用赋值语句将一个结构体的内容复制到另一个相同类型的结构体中，但你不能在结构体变量上使用关系运算符。因此，以下操作是非法的：

```
if (student == newStudent) // 非法
```

...

## 输入/输出

结构体变量不允许进行聚合输入输出操作。结构体变量中的数据必须一次读取一个成员。同样，结构体变量的内容必须一次写入一个成员。

我们已经见过如何将数据读入结构体变量中。现在让我们看看如何输出一个结构体变量。语句：

```
cout << newStudent.firstName << " " << newStudent.lastName
<< " " << newStudent.courseGrade
<< " " << newStudent.testScore
<< " " << newStudent.programmingScore
<< " " << newStudent.GPA << endl;
```

输出结构体变量 `newStudent` 的内容。

## 结构体变量与函数

回想数组仅按引用传递，且函数不能返回数组类型的值。但是：

- 结构体变量可以按值或按引用作为参数传递，
- 函数可以返回结构体类型的值。

以下函数读取并存储学生的姓名、测试成绩、编程分数和 GPA。它还会确定学生的课程成绩并将其存储在成员 `courseGrade` 中。

```
void readIn(studentType& student) {
  int score;

  cin >> student.firstName >> student.lastName;
  cin >> student.testScore >> student.programmingScore;
  cin >> student.GPA;

  if (score >= 90)
    student.courseGrade = 'A';
  else if (score >= 80)
    student.courseGrade = 'B';
  else if (score >= 70)
    student.courseGrade = 'C';
  else if (score >= 60)
    student.courseGrade = 'D';
  else
    student.courseGrade = 'F';
}
```

语句：

```
readIn(newStudent);
```

调用函数。同样，我们可以写一个函数来输出结构体变量。例如，以下函数输出结构体变量的内容：

```cpp
void printStudent(studentType student)
{
    cout << student.firstName << " " << student.lastName
         << " " << student.courseGrade
         << " " << student.testScore
         << " " << student.programmingScore
         << " " << student.GPA << endl;
}
```

`readIn` 在 `newStudent` 中存储信息。

## 数组与结构体

之前的讨论显示了结构体和数组有相似之处也有区别。表 9-1 总结了这些讨论。

表 9-1 数组与结构体

| 聚合操作 | 数组 | 结构体 |

|---|---|---|

| 算术 | 否 | 是 |

| 赋值 | 否 | 是 |

| 输入/输出 | 否（字符串外） | 否 |

| 比较 | 否 | 否 |

| 参数传递 | 仅引用 | 按值或引用 |

| 函数返回 | 否 | 是 |

## 结构体中的数组

列表是相同类型元素的集合。由于都是数组，我们可以定义：

第 9 章：记录（结构体）

622 | 第 9 章：记录（结构体）

接下来，我们编写顺序搜索算法来确定项目是否在列表中。如果 `searchItem` 在列表中，则函数返回其位置；否则，函数返回 -1。

```cpp
int seqSearch(const listType& list, int searchItem) {
  int loc;
  bool found = false;
  for (loc = 0; loc < list.listLength; loc++)
    if (list.listElem[loc] == searchItem)
      {
        found = true;
        break;
      }
  if (found)
    return loc;
  else
    return -1;
}
```

在这个函数中，因为 `length` 是 `list` 的成员，我们可以访问 `list.listLength`。同样，我们访问 `list.listElem[loc]`。

注意 `seqSearch` 的的形式参数是常量引用参数。这意味着 `list` 接收实际参数的地址，但 `list` 不能修改它。

同样，我们可以重写排序和其他列表处理函数。

## 数组中的结构体

假设一家公司有50名全职员工。我们需要打印他们的每月工资单，并跟踪每位员工从年初至今已支付的金额。首先，让我们定义一个员工记录：

```
struct employeeType {
    string firstName;
    string lastName;
    int personID;
    string deptID;
    double yearlySalary;
    double monthlySalary;
    double yearToDatePaid;
    double monthlyBonus;
}
```

每位员工都有以下成员（组件）：名字、姓氏、个人ID、部门ID、年薪、月薪、年初至今已付金额和每月奖金。

由于我们有50名员工，且每位员工的数据类型相同，我们可以使用一个包含50个组件的数组来处理员工数据。`employeeType employees[50];`

该语句声明了一个包含50个 `employeeType` 类型组件的 `employees` 数组（见图 9-7）。`employees` 的每一个元素都是一个结构体。例如，图 9-7 也显示了 `employees[2]`。

![](img/d998292a174f7bfd8a26bfbada3d454e_672_0.png)

图 9-7 员工数组

假设每位员工的初始数据——名字、姓氏、个人ID、部门ID和年薪——都在一个文件中。在讨论中，我们假设每位员工的数据存储在一个文件中：

```
ifstream stream variable
// 假设文件 employee.dat
// 已打开
```

```
for (int counter = 0; counter < 50; counter++)
{
	infile >> employees[counter].firstName;
	infile >> employees[counter].lastName;
	infile >> employees[counter].personID;
	infile >> employees[counter].deptID;
	infile >> employees[counter].yearlySalary;
	employees[counter].monthlySalary = employees[counter].yearlySalary / 12;

	employees[counter].yearToDatePaid = 0.0;
	employees[counter].monthlyBonus = 0.0;
}
```

假设某个月的每月奖金已经存储在每位员工的记录中，我们需要计算每月工资单并更新 `yearToDatePaid` 金额。以下循环计算并打印了员工当月的工资单：

```
double paycheck; // 用于计算工资的变量
for (int counter = 0; counter < 50; counter++)
{
	cout << employees[counter].firstName << " " << employees[counter].lastName << " ";

	paycheck = employees[counter].monthlySalary + employees[counter].monthlyBonus;

	employees[counter].yearToDatePaid = employees[counter].yearToDatePaid + paycheck;

	cout << setprecision(2) << paycheck << endl;
}
```

## 结构体中的结构体

你已经见过如何将 `struct` 和数组数据结构结合起来组织信息。你还见过某些示例，其中 `struct` 的成员是数组，而数组的类型是结构体。在本节中，你将学习在通过另一个结构体在结构体中组织数据更有益的情况。

让我们考虑以下员工记录：
