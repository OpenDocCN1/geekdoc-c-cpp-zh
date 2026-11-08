
其余函数的定义如下：

```cpp
int courseType::getCredits()
{
    return courseCredits;
} //end getCredits

string courseType::getCourseNumber()
{
    return courseNo;
}//end getCourseNumber

string courseType::getCourseName()
{
    return courseName;
} //end getCourseName
```

接下来，我们讨论学生组件。

> **注意**
> 请注意，在类 courseType 的定义中，成员函数（如 print 和 getCredits）是访问器函数。该类还有其他访问器函数。正如第 10 章所述，我们通常将访问器函数定义为在其函数头末尾带有关键字 const。我们将重新定义该类，使访问器函数声明为常量函数，作为练习留给你。（参见本章末尾的编程练习 12。）

### 学生

学生的主要特征包括学生姓名、学生 ID、已注册课程数、已注册课程以及每门课程的成绩。由于每个学生都必须缴纳学费，我们还包含一个成员来指示该学生是否已缴纳学费。

每个学生都是一个人，并且每个学生都要修课。我们已经设计了一个类 personType 来处理一个人的名和姓。我们还设计了一个类来处理课程信息。因此，我们可以看到，可以从类 personType 派生类 studentType 来跟踪学生信息，并且该类的一个成员的类型为 courseType。我们可以根据需要添加更多成员。

对 studentType 类型对象执行的基本操作如下：

1. 设置学生信息。
2. 打印学生信息。
3. 计算已修学分时数。
4. 计算 GPA。
5. 计算账单金额。
6. 由于成绩报告将按升序打印课程，因此根据课程编号对课程进行排序。

下面的类将 studentType 定义为 ADT。我们假设每个学生每学期最多修六门课程。

```cpp
class studentType: public personType
{
public:
    void setInfo(string fName, string lName, int ID,
                 int noOfCourses, bool isPTAid,
                 courseType courses[], char courseGrades[]);
        //Function to set the student's information.
        //Postcondition: The member variables are set
        //              according to the parameters.

    void print(ostream& out, double tuitionRate);
        //Function to print the student's grade report.
        //If the member variable isTuitionPaid is true, the grades
        //are shown; otherwise, three stars are printed. If the
        //actual parameter corresponding to out is the object
        //cout, then the output is shown on the standard output
        //device. If the actual parameter corresponding to out
        //is an ofstream object, say outFile, then the output
        //goes to the file specified by outFile.

    studentType();
        //Default constructor
        //The member variables are initialized.

    int getHoursEnrolled();
        //Function to return the credit hours a student is
        //enrolled in.
        //Postcondition: The number of credit hours is
        //              calculated and returned.

    double getGpa();
        //Function to return the grade point average.
        //Postcondition: The gpa is calculated and returned.

    double billingAmount(double tuitionRate);
        //Function to return the tuition fees.
        //Postcondition: The billing amount is calculated
        //and returned.
private:
    void sortCourses();
        //Function to sort the courses.
        //Postcondition: The array coursesEnrolled is sorted.
        //              For each course, its grade is stored in
        //              the array coursesGrade. Therefore, with
        //              the array coursesEnrolled is sorted, the
        //              corresponding entries in the array
        //              coursesGrade are adjusted.

    int sId;                 //variable to store the student ID
    int numberOfCourses;     //variable to store the number
                             //of courses
    bool isTuitionPaid;      //variable to indicate whether the
                             //tuition is paid
    courseType coursesEnrolled[6]; //array to store the courses
    char coursesGrade[6];          //array to store the course grades
};
```

图 11-10 展示了类 `studentType` 的 UML 类图，以及继承与组合（聚合）关系。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_795_0.png)

**图 11-10** 类 `studentType` 的 UML 类图，以及继承与组合（聚合）关系。

在编写类 `studentType` 的成员函数定义之前，我们作如下说明。

默认构造函数将私有成员变量初始化为默认值。请注意，由于私有成员变量 `coursesEnrolled` 的类型为 `courseType` 并且是一个数组，类 `courseType` 的默认构造函数会自动执行，整个数组会被初始化。

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

函数 `print` 打印成绩报告。参数 `outF` 指定输出设备。如果学生已缴纳学费，则显示成绩和 GPA。否则，每个成绩的位置打印三颗星，不显示 GPA，并显示一条消息指出因未缴纳学费而暂不提供成绩，同时显示应付金额。该函数包含以下步骤：

1. 输出学生姓名。
2. 输出学生 ID。
3. 输出学生已注册的课程数。
4. 输出表头：

   | 课程编号 | 课程名称 | 学分 | 成绩 |
   |---|---|---|---|
5. 打印每门课程的信息。

   对于每门课程，打印：

   a. 课程编号、课程名称、学分
   b. 如果 `isTuitionPaid` 为 true

      输出成绩

      `else`

      输出三颗星。
6. 打印总学分时数。
7. 为了以带小数点和尾随零的定点十进制格式输出 GPA 和账单金额，设置必要的标志。同时，将精度设置为两位小数。
8. 如果 `isTuitionPaid` 为 true

   输出 GPA

   `else`

   输出账单金额以及关于暂不提供成绩的消息。

函数 print 的定义如下：

```cpp
void studentType::print(ostream& outF, double tuitionRate)
{
    int i;

    outF << "Student Name: " << getFirstName()
         << " " << getLastName() << endl;                 //Step 1

    outF << "Student ID: " << sId << endl;               //Step 2

    outF << "Number of courses enrolled: "
         << numberOfCourses << endl;                      //Step 3
    outF << endl;

    outF << left;
    outF << "Course No" << setw(15) << " Course Name"
         << setw(8) << "Credits"
         << setw(6) << "Grade" << endl;                  //Step 4

    outF << right;
    for (i = 0; i < numberOfCourses; i++)                 //Step 5
    {
        coursesEnrolled[i].print(outF);                   //Step 5a

        if (isTuitionPaid)                                //Step 5b
            outF << setw(4) << coursesGrade[i] << endl;
        else
            outF << setw(4) << "***" << endl;
    }
    outF << endl;

    outF << "Total number of credit hours: "
         << getHoursEnrolled() << endl;                   //Step 6

    outF << fixed << showpoint << setprecision(2);         //Step 7

    if (isTuitionPaid)                                    //Step 8
        outF << "Mid-Semester GPA: " << getGpa()
             << endl;
    else
    {
        outF << "*** Grades are being held for not paying "
             << "the tuition. ***" << endl;
        outF << "Amount Due: $" << billingAmount(tuitionRate)
             << endl;
    }

    outF << "*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*"
         << "*-*-*-*-*" << endl << endl;
} //end print
```
