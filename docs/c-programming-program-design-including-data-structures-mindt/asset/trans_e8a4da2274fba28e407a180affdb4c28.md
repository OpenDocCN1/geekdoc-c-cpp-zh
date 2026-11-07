
```
struct studentType
{
    string firstName;
    string lastName;
    char courseGrade;
    int testScore;
    int programmingScore;
    double GPA;
};

//variables
studentType newStudent;
studentType student;
```

假设你想将 `newStudent` 的成员 GPA 初始化为 0.0。下面的语句完成此任务：

```
newStudent.GPA = 0.0;
```

类似地，以下语句：

```
newStudent.firstName = "John";
newStudent.lastName = "Brown";
```

将 "John" 存储到 `newStudent` 的成员 `firstName` 中，将 "Brown" 存储到 `newStudent` 的成员 `lastName` 中。

执行前面三条赋值语句后，`newStudent` 如图 9-2 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_664_0.png)

**图 9-2**  `struct newStudent`

语句：

```
cin >> newStudent.firstName;
```

从标准输入设备读取下一个字符串，并将其存储到：

```
newStudent.firstName
```

语句：

```
cin >> newStudent.testScore >> newStudent.programmingScore;
```

从键盘读取两个整数值，并分别存储到 `newStudent.testScore` 和 `newStudent.programmingScore` 中。

假设 `score` 是一个 `int` 类型的变量。语句：

```
score = (newStudent.testScore + newStudent.programmingScore) / 2;
```

将 `newStudent.testScore` 和 `newStudent.programmingScore` 的平均值赋给 `score`。

以下语句确定课程成绩，并将其存储到 `newStudent.courseGrade` 中：

```
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

考虑上一节给出的 `struct houseType` 的定义以及以下语句：

```
houseType ryanHouse;
houseType anitaHouse;

ryanHouse.style = "Colonial";
ryanHouse.numOfBedrooms = 3;
ryanHouse.numOfBathrooms = 2;
ryanHouse.numOfCarsGarage = 2;
ryanHouse.yearBuilt = 2005;
ryanHouse.finishedSquareFootage = 2250;
ryanHouse.price = 290000;
ryanHouse.tax = 5000.50;
```

前两条语句将 `ryanHouse` 和 `anitaHouse` 声明为 `houseType` 类型的变量。接下来的八条语句将字符串 "Colonial" 存储到 `ryanHouse.style`，将 3 存储到 `ryanHouse.numOfBedrooms`，将 2 存储到 `ryanHouse.numOfBathrooms`，依此类推。

接下来，考虑以下语句：

```
cin >> anitaHouse.style >> anitaHouse.numOfBedrooms
   >> anitaHouse.price;
```

如果输入为：

```
Ranch 4 350000
```

那么字符串 "Ranch" 会存储到 `anitaHouse.style`，4 会存储到 `anitaHouse.numOfBedrooms`，350000 会存储到 `anitaHouse.price`。

## 赋值

我们可以使用赋值语句将一个结构体变量的值赋给另一个同类型的结构体变量。假设 `newStudent` 如图 9-3 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_666_0.png)

**图 9-3**  `struct newStudent`

语句：

```
student = newStudent;
```

将 `newStudent` 的内容复制到 `student`。执行此赋值语句后，`student` 的值如图 9-4 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_666_1.png)

**图 9-4**  执行 `student = newStudent` 后的 `student`

事实上，赋值语句：

```cpp
student = newStudent;
```

等价于以下语句：

```cpp
student.firstName = newStudent.firstName;
student.lastName = newStudent.lastName;
student.courseGrade = newStudent.courseGrade;
student.testScore = newStudent.testScore;
student.programmingScore = newStudent.programmingScore;
student.GPA = newStudent.GPA;
```

## 比较（关系运算符）

要比较 `struct` 变量，需要逐个成员进行比较。与数组一样，不会对 `struct` 执行聚合关系运算。例如，假设 `newStudent` 和 `student` 按前面所示声明。此外，假设你想判断 `student` 和 `newStudent` 是否指同一个学生。现在，如果它们具有相同的名和相同的姓，则 `newStudent` 和 `student` 指同一个学生。要比较 `student` 和 `newStudent` 的值，必须按如下方式逐个成员比较：

```cpp
if (student.firstName == newStudent.firstName &&
    student.lastName == newStudent.lastName)
```

尽管可以使用赋值语句将一个 `struct` 的内容复制到另一个同类型的 `struct`，但不能对 `struct` 变量使用关系运算符。因此，以下写法是非法的：

```cpp
if (student == newStudent)    //illegal
```

## 输入/输出

不允许对 `struct` 变量进行聚合输入/输出操作。`struct` 变量中的数据必须一次读取一个成员。类似地，`struct` 变量的内容必须一次写入一个成员。

我们已经了解如何将数据读入 `struct` 变量。现在来看看如何输出 `struct` 变量。语句：

```cpp
cout << newStudent.firstName << " " << newStudent.lastName
     << " " << newStudent.courseGrade
     << " " << newStudent.testScore
     << " " << newStudent.programmingScore
     << " " << newStudent.GPA << endl;
```

输出 `struct` 变量 `newStudent` 的内容。

## 结构体变量与函数

回顾一下，数组只能按引用传递，并且函数不能返回数组类型的值。但是：

- `struct` 变量既可以按值传递，也可以按引用作为参数传递，并且
- 函数可以返回 `struct` 类型的值。

以下函数读取并存储学生的名、姓、测验成绩、编程成绩和 GPA。它还确定学生的课程成绩，并将其存储到成员 `courseGrade` 中。

```cpp
void readIn(studentType& student)
{
    int score;

    cin >> student.firstName >> student.lastName;
    cin >> student.testScore >> student.programmingScore;
    cin >> student.GPA;

    score = (student.testScore + student.programmingScore) / 2;

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

```cpp
readIn(newStudent);
```

调用函数 `readIn`。函数 `readIn` 将相应信息存储到变量 `newStudent` 中。

类似地，我们可以编写一个函数来打印 `struct` 变量的内容。例如，以下函数在屏幕上输出 `studentType` 类型的 `struct` 变量的内容：

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

## 数组与 `struct`s 的对比

前面的讨论表明，`struct` 和数组既有相似之处，也有不同之处。表 9-1 总结了这些讨论。

**表 9-1** 数组与 `struct`s 的对比

| 聚合操作 | 数组 | `struct` |
|---|---|---|
| 算术 | 否 | 否 |
| 赋值 | 否 | 是 |
| 输入/输出 | 否（字符串除外） | 否 |
| 比较 | 否 | 否 |
| 参数传递 | 仅按引用 | 按值或按引用 |
| 函数返回值 | 否 | 是 |

## `struct` 中的数组

列表是同一类型元素的集合。因此，列表有两个相关属性：值（即元素）和长度。由于值和长度都与列表相关，我们可以定义一个包含这两个项的 `struct`。

```cpp
const int ARRAY_SIZE = 1000;
struct listType
{
    int listElem[ARRAY_SIZE];    // array containing the list
    int listLength;              // length of the list
};
```

以下语句将 `intList` 声明为 `listType` 类型的 `struct` 变量（见图 9-5）：

```cpp
listType intList;
```

