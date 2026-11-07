
接下来，我们讨论实现 `class studentType` 操作的相关函数定义。

函数 `setInfo` 首先将 `private` 成员变量初始化为传入的参数值。然后，该函数调用函数 `sortCourses`，按课程编号对数组 `coursesEnrolled` 进行排序。`class studentType` 派生自 `class personType`，用于存储名和姓的变量是该类的 `private` 成员变量。因此，我们调用 `class personType` 的成员函数 `setName`，传入适当的变量来设置名和姓。

函数 `setInfo` 的定义如下：

```cpp
void studentType::setInfo(string fName, string lName, int ID,
                           int nOfCourses, bool isTPaid,
                           courseType courses[], char cGrades[])
{
    setName(fName, lName);                 //set the name

    sId = ID;                               //set the student ID
    isTuitionPaid = isTPaid;               //set isTuitionPaid
    numberOfCourses = nOfCourses;          //set the number of courses

          //set the course information
    for (int i = 0; i < numberOfCourses; i++)
    {
        coursesEnrolled[i] = courses[i];
        coursesGrade[i] = cGrades[i];
    }

    sortCourses();   //sort the array coursesEnrolled
} //end setInfo
```

默认构造函数将 `private` 成员变量初始化为默认值。请注意，由于 `private` 成员变量 `coursesEnrolled` 是 `courseType` 类型的数组，`class courseType` 的默认构造函数会自动执行，整个数组会被初始化。

```cpp
studentType::studentType()
{
    numberOfCourses = 0;
    sId = 0;
    isTuitionPaid = false;

    for (int i = 0; i < 6; i++)
        coursesGrade[i] = '*';
} //end default constructor
```

函数 `print` 打印成绩报告。参数 `outF` 指定输出设备。如果学生已缴纳学费，则显示成绩和 GPA。否则，每个成绩的位置打印三个星号，不显示 GPA，并显示一条消息说明因未缴纳学费而暂扣成绩，同时显示应付金额。该函数有以下步骤：

- 1. 输出学生姓名。
- 2. 输出学生 ID。
- 3. 输出学生注册的课程数量。
- 4. 输出标题：
    ```text
    Course No Course Name Credits Grade
    ```
- 5. 打印每门课程的信息。对于每门课程，打印：
  - a. `Course No, Course Name, Credits`
  - b. `if isTuitionPaid is true`
    输出成绩
    `else`
    输出三个星号。
- 6. 打印总学分时数。
- 7. 要以定点小数格式输出 GPA 和账单金额，并保留小数点和尾随零，请设置必要的标志。同时，将精度设置为两位小数。
- 8. `if isTuitionPaid is true`
  输出 GPA
  `else`
  输出账单金额以及关于暂扣成绩的消息。

函数 print 的定义如下：

```cpp
void studentType::print(ostream& outF, double tuitionRate)
{
    outF << "Student Name: " << getFirstName()
         << " " << getLastName() << endl;        //Step 1

    outF << "Student ID: " << sId << endl;       //Step 2

    outF << "Number of courses enrolled: "
         << numberOfCourses << endl;              //Step 3
    outF << endl;

    outF << left;
    outF << "Course No" << setw(15) << " Course Name"
         << setw(8) << "Credits"
         << setw(6) << "Grade" << endl;           //Step 4

    outF << right;

    for (int i = 0; i < numberOfCourses; i++)          //step 5
    {
        coursesEnrolled[i].print(outF);               //step 5a

        if (isTuitionPaid)                            //step 5b
            outF << setw(4) << coursesGrade[i] << endl;
        else
            outF << setw(4) << "****" << endl;
    }
    outF << endl;

    outF << "Total number of credit hours: "
         << getHoursEnrolled() << endl;                //step 6

    outF << fixed << showpoint << setprecision(2);     //step 7

    if (isTuitionPaid)                                //step 8
        outF << "Mid-Semester GPA: " << getGpa()
             << endl;
    else
    {
        outF << "**** Grades are being held for not paying "
             << "the tuition. ****" << endl;
        outF << "Amount Due: $" << billingAmount(tuitionRate)
             << endl;
    }
    outF << "-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
         << "-*-*-*-*-*" << endl << endl;
} //end print
```

> **注意** 让我们看看函数 `print` 的形式参数。形式参数 `outF` 是类 `ostream` 的对象。我们可以使用此函数将输出发送到标准输出设备（屏幕）或文件。如类定义中所示，如果实际参数是，比如 `cout`，则输出显示在屏幕上。如果实际参数是，比如 `outfile`（类 `ofstream` 的对象），则输出发送到 `outfile` 所指示的设备。正如“C++ 流类”一节所述，类 `ofstream` 派生自类 `ostream`。因此，类 `ostream` 是基类。在 C++ 中，如果形式引用参数的类型是 `ostream`，则它可以引用类 `ostream` 的对象。
> 
> 一般来说，C++ 允许基类类型的形式引用参数引用派生类的对象。当然，对于用户定义的类，要使该机制正常工作，还需要考虑一些其他事项，我们将在第12章（“继承、指针和虚函数”一节）中讨论。

函数 `getHoursEnrolled` 计算并返回学生正在修读的总学分时数。计算 GPA 和账单金额都需要这些学分时数。总学分时数通过将学生所修每门课程的学分时数相加来计算。由于课程的学分时数位于 `courseType` 类型对象的 `private` 成员变量中，我们使用 `class` `courseType` 的成员函数 `getCredits` 来获取学分时数。该函数的定义如下：

```cpp
int studentType::getHoursEnrolled()
{
    int totalCredits = 0;

    for (int i = 0; i < numberOfCourses; i++)
        totalCredits += coursesEnrolled[i].getCredits();

    return totalCredits;
} //end getHoursEnrolled
```

如果学生尚未缴纳学费，函数 `billingAmount` 根据已注册的学分时数计算并返回应付金额。该函数的定义如下：

```cpp
double studentType::billingAmount(double tuitionRate)
{
    return tuitionRate * getHoursEnrolled();
} //end billingAmount
```

现在我们讨论函数 `getGpa`。该函数计算学生的 GPA。为了求出 GPA，我们先求出每个成绩对应的绩点，将绩点相加，然后除以学生正在修读的总学分时数。该函数的定义如下：

```cpp
double studentType::getGpa()
{
    double sum = 0.0;

    for (int i = 0; i < numberOfCourses; i++)
    {
        switch (coursesGrade[i])
        {
        case 'A':
            sum += coursesEnrolled[i].getCredits() * 4;
            break;
        case 'B':
            sum += coursesEnrolled[i].getCredits() * 3;
            break;
        case 'C':
            sum += coursesEnrolled[i].getCredits() * 2;
            break;
        case 'D':
            sum += coursesEnrolled[i].getCredits() * 1;
            break;
        case 'F':
            break;
        default:
            cout << "Invalid Course Grade." << endl;
        }
    }

    return sum / getHoursEnrolled();
} //end getGpa
```

函数 sortCourses 按课程编号对数组 coursesEnrolled 进行排序。为了对该数组排序，我们使用选择排序算法。由于我们将比较课程编号（它们是字符串，并且是类 courseType 的 private 成员变量），我们首先获取课程编号并将其存储在局部变量中。

```cpp
void studentType::sortCourses()
{
    int minIndex;
    courseType temp;       //variable to swap the data
    char tempGrade;        //variable to swap the grades
    string course1;
    string course2;

    for (int i = 0; i < numberOfCourses - 1; i++)
    {
        minIndex = i;

        for (int j = i + 1; j < numberOfCourses; j++)
        {
            //get the course numbers
            course1 = coursesEnrolled[minIndex].getCourseNumber();
            course2 = coursesEnrolled[j].getCourseNumber();

            if (course1 > course2)
                minIndex = j;
        } //end for

        temp = coursesEnrolled[minIndex];
        coursesEnrolled[minIndex] = coursesEnrolled[i];
        coursesEnrolled[i] = temp;

        tempGrade = coursesGrade[minIndex];
        coursesGrade[minIndex] = coursesGrade[i];
        coursesGrade[i] = tempGrade;
    } //end for
} //end sortCourses
```
