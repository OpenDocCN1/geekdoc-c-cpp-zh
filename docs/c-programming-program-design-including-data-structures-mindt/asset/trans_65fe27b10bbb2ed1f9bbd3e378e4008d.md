
```cpp
void print(ostream& outF);
//Function to print the course information.
//This function sends the course information to the
//output device specified by the parameter outF. If the
//actual parameter to this function is the object cout,
//then the output is shown on the standard output device.
//If the actual parameter is an ostream variable, say
//outfile, then the output goes to the file specified by
//outfile.

int getCredits();
//Function to return the credit hours.
//Postcondition: The value of courseCredits is returned.

string getCourseNumber();
//Function to return the course number.
//Postcondition: The value of courseNo is returned.

string getCourseName();
//Function to return the course name.
//Postcondition: The value of courseName is returned.

courseType(string cName = "", string cNo = "",
           int credits = 0);
//Constructor
//The object is initialized according to the parameters.
//Postcondition: courseName = cName; courseNo = cNo;
//              courseCredits = credits;
//

private:
    string courseName;   //variable to store the course name
    string courseNo;     //variable to store the course number
    int courseCredits;   //variable to store the credit hours
};
```

图 11-9 显示了 `courseType` 类的 UML 类图。

![](img/b217c421655b51e7494cf3b89bb5432d_833_0.png)

**图 11-9** `courseType` 类的 UML 类图

实现 `class courseType` 各操作的函数定义非常直观，易于理解。

函数 `setCourseInfo` 根据参数值设置 `private` 成员变量的值。其定义如下：

```cpp
void courseType::setCourseInfo(string cName, string cNo,
                               int credits)
{
    courseName = cName;
    courseNo = cNo;
    courseCredits = credits;
} //end setCourseInfo
```

函数 `print` 打印课程信息。参数 `outF` 指定输出设备。另外，我们以左对齐方式而不是右对齐方式（默认方式）打印课程名称和课程编号。因此，需要设置左对齐操纵符。在打印学分时之前，将操纵符设置为右对齐。以下步骤描述该函数：

- 1. 设置左对齐操纵符。
- 2. 打印课程编号。
- 3. 打印课程名称。
- 4. 设置右对齐操纵符。
- 5. 打印学分时。

函数 `print` 的定义如下：

```cpp
void courseType::print(ostream& outF)
{
    outF << left;                         //Step 1
    outF << setw(8) << courseNo << "  ";  //Step 2
    outF << setw(15) << courseName;       //Step 3
    outF << right;                        //Step 4
    outF << setw(3) << courseCredits << "  "; //Step 5
} //end print
```

![](img/b217c421655b51e7494cf3b89bb5432d_834_0.png)

构造函数声明时带有默认值。如果在声明 `courseType` 对象时未指定任何值，则构造函数使用默认值按如下方式初始化对象：`courseNo` 为空，`courseName` 为空，`courseCredits` 为 0。否则，使用对象声明中指定的值来初始化对象。其定义如下：

```cpp
courseType::courseType(string cName, string cNo, int credits)
{
    courseName = cName;
    courseNo = cNo;
    courseCredits = credits;
} //end constructor
```

其余函数的定义如下：

```cpp
int courseType::getCredits()
{
    return courseCredits;
} //end getCredits

string courseType::getCourseNumber()
{
    return courseNo;
} //end getCourseNumber

string courseType::getCourseName()
{
    return courseName;
} //end getCourseName
```

接下来，我们讨论学生组件。

> **注意** 请注意，在类 `courseType` 的定义中，成员函数（如 `print` 和 `getCredits`）是访问器函数。该类还有其他访问器函数。如第 10 章所述，我们通常将访问器函数定义为在其头部末尾带有关键字 `const`。我们将其留作练习，让你重新定义该类，使访问器函数声明为常量函数。（参见本章末尾的编程练习 12。）

## 学生

学生的主要特征包括学生姓名、学生 ID、已注册课程数、已注册课程以及每门课程的成绩。由于每个学生都必须缴纳学费，我们还包括一个成员，用于指示该学生是否已缴纳学费。

每个学生都是一个人，并且每个学生都要修读课程。我们已经设计了一个类 `personType` 来处理一个人的名和姓。我们还设计了一个类来处理课程信息。因此，我们可以看到，可以从类 `personType` 派生出类 `studentType` 来记录学生信息，并且该类的一个成员的类型为 `courseType`。我们可以根据需要添加更多成员。

对 `studentType` 类型对象执行的基本操作如下：

- 1. 设置学生信息。
- 2. 打印学生信息。
- 3. 计算已修学分时数。
- 4. 计算 GPA。
- 5. 计算计费金额。
- 6. 由于成绩报告将按升序打印课程，因此按课程编号对课程排序。

下面的类将 `studentType` 定义为 ADT。我们假设一个学生每学期最多修读六门课程，因此我们将课程信息存储在一个包含六个课程对象的数组中。

```cpp
class studentType: public personType
{
public:
    void setInfo(string fName, string lName, int ID,
                 int nOfCourses, bool isTPaid,
                 courseType courses[], char courseGrades[]);
    //Function to set the student's information
    //Postcondition: The member variables are set
    //              according to the parameters.

    void print(ostream& outF, double tuitionRate);
    //Function to print the student's grade report.
    //If the member variable isTuitionPaid is true, the grades
    //are shown, otherwise those stars are printed. If the
    //actual parameter corresponding to outF is the object
    //cout, then the output is shown on the standard output
    //device. If the actual parameter corresponding to outF
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
    //Postcondition: The GPA is calculated and returned.

    double billingAmount(double tuitionRate);
    //Function to return the tuition fees.
    //Postcondition: The billing amount is calculated
    //and returned.

private:
    void sortCourses();
    //Function to sort the courses.
    //Postcondition: The array coursesEnrolled is sorted.
    //              For each course, its grade is stored in
    //              the array coursesGrade. Therefore, when
    //              the array coursesEnrolled is sorted, the
    //              corresponding entries in the array
    //              coursesGrade are adjusted.

    int sId;                 //variable to store the student ID
    int numberOfCourses;     //variable to store the number
                             //of courses
    bool isTuitionPaid;      //variable to indicate whether the
                             //tuition is paid
    courseType coursesEnrolled[6]; //array to store the courses
    char coursesGrade[6];    //array to store the courses grades
};
```

图 11-10 显示了 `studentType` 类的 UML 类图，以及继承和组合（聚合）关系。

![](img/b217c421655b51e7494cf3b89bb5432d_837_0.png)

**图 11-10** `studentType` 类的 UML 类图，以及继承和组合（聚合）关系。

在编写类 `studentType` 的成员函数定义之前，我们作如下说明。

> **注意** 请注意，在类 `studentType` 的定义中，成员函数（如 `print` 和 `getGpa`）是访问器函数。该类还有其他访问器函数。如第 10 章所述，我们通常将访问器函数定义为在其头部末尾带有关键字 `const`。我们将其留作练习，让你重新定义该类，使访问器函数声明为常量函数。（参见本章末尾的编程练习 12。）

注意，用于对数组 `coursesEnrolled` 排序的成员函数 `sortCourses` 是类 `studentType` 的私有成员。这是因为该函数是内部数据处理所需要的，而该类的用户不需要访问此成员。

