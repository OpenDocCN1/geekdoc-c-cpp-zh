
默认构造函数将`private`成员变量初始化为默认值。注意，由于`private`成员变量`coursesEnrolled`的类型为`courseType`且是一个数组，`class` `courseType`的默认构造函数会自动执行，整个数组都会被初始化。

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

函数`print`打印成绩报告。参数`outF`指定输出设备。如果学生已支付学费，则显示成绩和GPA。否则，将打印三个星号代替每个成绩，不显示GPA，并显示一条消息指明成绩因未支付学费而被暂扣，同时显示应缴金额。该函数包含以下步骤：

- 1. 输出学生姓名。
- 2. 输出学生ID。
- 3. 输出学生注册的课程数量。
- 4. 输出标题：
  `Course No  Course Name  Credits  Grade`
- 5. 打印每门课程的信息。
  对于每门课程，打印：
  - a. 课程编号、课程名称、学分
  - b. `if isTuitionPaid is true`
    输出成绩
    `else`
    输出三个星号。
- 6. 输出总学分。
- 7. 要以固定小数格式输出GPA和账单金额，并带小数点与尾随零，请设置必要的标志。同时，将精度设置为两位小数。
- 8. `if isTuitionPaid is true`
  输出GPA
  `else`
  输出账单金额以及关于暂扣成绩的消息。

函数`print`的定义如下：

```cpp
void studentType::print(ostream& outF, double tuitionRate)
{
    int i;

    outF << "Student Name: " << getFirstName()
         << " " << getLastName() << endl;             //Step 1

    outF << "Student ID: " << sId << endl;             //Step 2

    outF << "Number of courses enrolled: "
         << numberOfCourses << endl;                    //Step 3
    outF << endl;

    outF << left;
    outF << "Course No" << setw(15) << "  Course Name"
         << setw(8) << "Credits"
         << setw(6) << "Grade" << endl;                //Step 4

    outF << right;
    for (i = 0; i < numberOfCourses; i++)               //Step 5
    {
        coursesEnrolled[i].print(outF);                 //Step 5a

        if (isTuitionPaid)                               //Step 5b
            outF << setw(4) << coursesGrade[i] << endl;
        else
            outF << setw(4) << "***" << endl;
    }
    outF << endl;

    outF << "Total number of credit hours: "
         << getHoursEnrolled() << endl;                  //Step 6

    outF << fixed << showpoint << setprecision(2);       //Step 7

    if (isTuitionPaid)                                   //Step 8
        outF << "Mid-Semester GPA: " << getGpa()
             << endl;
    else
    {
        outF << "*** Grades are being held for not paying "
             << "the tuition. ***" << endl;
        outF << "Amount Due: $" << billingAmount(tuitionRate)
             << endl;
    }

    outF << "*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
         << "*-*-*-*-*-*-*-*" << endl;
}
//end print
```

> **注意：**
>
> 让我们看一下函数`print`的形参。形参`outF`是`class` `ostream`的一个对象。我们可以使用此函数将输出发送到标准输出设备（屏幕）或文件。如函数定义所示，如果实参是`cout`，则输出显示在屏幕上。如果实参是`outfile`（一个`class` `ofstream`的对象），则输出被发送到`outfile`指示的设备。
>
> 如“C++流层次结构”一节所述，`class` `ofstream`派生自`class` `ostream`。因此，`class` `ostream`是基类。在C++中，如果形参引用类型为`ostream`，它可以引用`class` `ofstream`的对象。
>
> 一般来说，C++允许基类类型的形参引用引用派生类的对象。当然，对于用户自定义的类，要使此机制正常工作还需要考虑其他一些问题，我们将在第14章（“继承、指针和虚函数”一节）中讨论。

函数`getHoursEnrolled`计算并返回学生正在修读的总学分。这些学分在计算GPA和账单金额时都需要。总学分通过将学生注册的每门课程的学分相加得到。由于课程的学分数存储在`courseType`类型对象的`private`成员变量中，我们使用`class` `courseType`的成员函数`getCredits`来获取学分。该函数的定义如下：

```cpp
int studentType::getHoursEnrolled()
{
    int totalCredits = 0;
    int i;

    for (i = 0; i < numberOfCourses; i++)
        totalCredits += coursesEnrolled[i].getCredits();

    return totalCredits;
} //end getHoursEnrolled
```

如果学生未支付学费，函数`billingAmount`将根据注册的学分数计算并返回应缴金额。该函数的定义如下：

```cpp
double studentType::billingAmount(double tuitionRate)
{
    return tuitionRate * getHoursEnrolled();
} //end billingAmount
```

```cpp
for (i = 0; i < numberOfCourses - 1; i++)
{
    minIndex = i;

    for (j = i + 1; j < numberOfCourses; j++)
    {
        //get the course numbers
        course1 =
            coursesEnrolled[minIndex].getCourseNumber();
        course2 = coursesEnrolled[j].getCourseNumber();

        if (course1 > course2)
            minIndex = j;
    }//end for

    temp = coursesEnrolled[minIndex];
    coursesEnrolled[minIndex] = coursesEnrolled[i];
    coursesEnrolled[i] = temp;

    tempGrade = coursesGrade[minIndex];
    coursesGrade[minIndex] = coursesGrade[i];
    coursesGrade[i] = tempGrade;
} //end for
} //end sortCourses
```

## 主程序

现在我们已经设计了`courseType`和`studentType`类，我们将使用这些类来完成该程序。

我们将程序限制为最多处理10名学生。请注意，该程序可以轻松增强以处理任意数量的学生。

由于类的`print`函数会执行必要的计算来打印最终成绩报告，主程序几乎没有什么工作要做。事实上，主程序剩下的工作就是声明用于保存学生数据的对象，将数据加载到这些对象中，然后打印成绩报告。由于输入来自文件，输出也将发送到文件，我们需要声明流变量来访问输入和输出文件。本质上，程序的主算法是：

- 1. 声明变量。
- 2. 打开输入文件。
- 3. 如果输入文件不存在，则退出程序。
- 4. 打开输出文件。
- 5. 获取注册学生人数和学费费率。
- 6. 加载学生数据。
- 7. 打印成绩报告。

### 变量

该程序最多处理10名学生。因此，我们必须声明一个包含10个`studentType`类型组件的数组来保存学生数据。我们还需要存储注册学生人数和学费费率。由于数据将从文件读取，输出也会发送到文件，我们需要两个流变量来访问输入和输出文件。因此，我们需要以下变量：

```cpp
studentType studentList[MAX_NO_OF_STUDENTS];  //array to store
                                               //the students’ data

int noOfStudents;    //variable to store the number of students
double tuitionRate;  //variable to store the tuition rate

ifstream infile;     //input stream variable
ofstream outfile;    //output stream variable
```

### getStudentData函数

该函数有三个参数：一个用于访问输入文件的参数，一个用于访问数组`studentList`的参数，以及一个用于获知注册学生人数的参数。其定义的伪代码如下：

- 对于大学中的每个学生，
  - 1. 获取名、姓、学生ID和`isPaid`。
  - 2. 如果`isPaid`为‘Y’：
    - 将`isTuitionPaid`设置为`true`
    - 否则将`isTuitionPaid`设置为`false`
  - 3. 获取该学生正在修读的课程数量。
  - 4. 对于每门课程：
    - 获取课程名称、课程编号、学分和成绩。
    - 将课程信息加载到`courseType`对象中。
  - 5. 将数据加载到`studentType`对象中。

我们需要声明几个局部变量来读取和存储数据。函数`getStudentData`的定义如下：

```cpp
void getStudentData(ifstream& infile,
                    studentType studentList[],
                    int numberOfStudents)
{
        //local variables
        string fName;       //variable to store the first name
        string lName;       //variable to store the last name
        int ID;              //variable to store the student ID
        int noOfCourses;     //variable to store the number of courses
        char isPaid;         //variable to store Y/N, that is
                             //is tuition paid
        bool isTuitionPaid;  //variable to store true/false
}
```

