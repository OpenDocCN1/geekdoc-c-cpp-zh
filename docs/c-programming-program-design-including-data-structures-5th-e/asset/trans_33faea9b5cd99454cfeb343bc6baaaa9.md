
将**圆柱体**看作一个类——比如**cylinderType**——我们可以从中创建许多具有各种尺寸的圆柱体对象。名词**尺寸**、**表面积**和**体积**是**圆柱体**的特征，因此很难将它们视为类。

在确定一个类之后，下一步是确定三类信息：

- 该类型的对象可以执行的操作
- 可以对该类型的对象执行的操作
- 该类型的对象必须维护的信息

从问题描述中识别出的动词列表里，我们选择该类的对象可以执行或已经对自身执行的一组可能操作。例如，从圆柱体问题描述的动词列表——**写入**、**输入**、**计算**和**打印**——中，圆柱体对象可能执行的操作是**输入**、**计算**和**打印**。

对于类**cylinderType**，尺寸表示数据。底面的**中心**、底面的**半径**以及圆柱体的**高度**是尺寸的特征。你可以通过构造函数或修改器函数向对象输入数据。

动词**计算**适用于确定体积和表面积。由此，你可以推断出操作：**cylinderVolume**和**cylinderSurfaceArea**。类似地，动词**打印**适用于在输出设备上显示体积和表面积。在本章末尾的编程练习5中，要求你设计一个类来实现圆柱体的特征。

通过问题描述中的名词和动词来识别类并不是唯一可行的技术。文献中还有其他几种面向对象设计（OOD）技术。不过，对于本书中的编程练习，这种技术已经足够。

### 编程示例：成绩报告

本编程示例进一步说明了继承和组合的概念。

你所在当地大学的期中时间即将到来。注册办公室希望在学生的成绩录入后尽快准备成绩报告。然而，一些已注册的学生尚未缴纳学费。

- 1. 如果学生已缴纳学费，则成绩会连同平均绩点（GPA）一起显示在成绩报告上。
- 2. 如果学生未缴纳学费，则不打印成绩。对于这些学生，成绩报告中包含一条消息，说明由于未缴纳学费，成绩已被暂缓公布。成绩报告还会显示账单金额。

注册办公室和财务办公室希望你帮助编写一个程序，该程序能够分析学生数据并打印相应的成绩报告。数据以如下形式存储在文件中：

```text
15000 345
studentName studentID isTuitionPaid numberOfCourses
courseName courseNumber creditHours grade
courseName courseNumber creditHours grade
.
.
.
studentName studentID isTuitionPaid numberOfCourses
courseName courseNumber creditHours grade
courseName courseNumber creditHours grade
.
.
.
```

第一行表示已注册的学生人数以及每学分时的学费率。之后给出学生的数据。

一个示例输入文件如下：

```text
3 345
Lisa Miller 890238 Y 4
Mathematics MTH345 4 A
Physics PHY357 3 B
ComputerSci CSC478 3 B
History HIS356 3 A
.
.
.
```

第一行表示输入文件包含三个学生的数据，学费率为每学分时345美元。接下来给出学生Lisa Miller的课程数据：Lisa Miller的ID是890238，她已缴纳学费，并且她正在修读四门课程。她所修读的数学课程的课程编号是MTH345，该课程有四个学分时，她的期中成绩是A，依此类推。

每个学生的期望输出形式如下：

学生姓名：Lisa Miller  
学生ID：890238  
已注册课程数：4  

| 课程编号 | 课程名称 | 学分 | 成绩 |
| --- | --- | ---: | --- |
| CSC478 | 计算机科学 | 3 | B |
| HIS356 | 历史 | 3 | A |
| MTH345 | 数学 | 4 | A |
| PHY357 | 物理 | 3 | B |

总学分数：13  
期中GPA：3.54

从这个输出可以明显看出，课程必须按课程编号排序。为了计算GPA，我们假设成绩A相当于4分，B相当于3分，C相当于2分，D相当于1分，F相当于0分。

**输入** 一个包含前述形式数据的文件。为便于参考，我们假设输入文件名为`data.txt`。

**输出** 一个包含前述形式输出的文件。

## 问题分析与算法设计

我们必须首先确定程序的主要组成部分。大学有学生，每个学生都要修读课程。因此，两个主要组成部分是学生和课程。

让我们首先描述课程组件。

### 课程

课程的主要特征是课程名称、课程编号和学分时数。

需要对课程类型对象执行的一些基本操作包括：

- 1. 设置课程信息。
- 2. 打印课程信息。
- 3. 显示学分时数。
- 4. 显示课程编号。

下面的类将课程定义为ADT：

```cpp
class courseType
{
public:
    void setCourseInfo(string cName, string cNo, int credits);
        //Function to set the course information.
        //The course information is set according to the
        //parameters.
        //Postcondition: courseName = cName; courseNo = cNo;
        //               courseCredits = credits;
        //

    void print(ostream& out);
        //Function to print the course information.
        //This function sends the course information to the
        //output device specified by the parameter out. If the
        //actual parameter to this function is the object cout,
        //then the output is shown on the standard output device.
        //If the actual parameter is an ofstream variable, say
        //outFile, then the output goes to the file specified by
        //outFile.

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

private:
    string courseName;      //variable to store the course name
    string courseNo;        //variable to store the course number
    int courseCredits;      //variable to store the credit hours
};
```

图12-9显示了类`courseType`的UML类图。

![](img/f97f778697507bb6fdd80c5991210cba_754_0.png)

**图12-9** 类`courseType`的UML类图

接下来，我们讨论实现类`courseType`操作的函数定义。这些定义相当直接且易于理解。

函数`setCourseInfo`根据参数值设置`private`成员变量的值。其定义如下：

```cpp
void courseType::setCourseInfo(string cName, string cNo,
                                int credits)
{
    courseName = cName;
    courseNo = cNo;
    courseCredits = credits;
} //end setCourseInfo
```

函数`print`打印课程信息。参数`outF`指定输出设备。此外，我们以左对齐而非右对齐（默认）方式打印课程名称和课程编号。因此，需要设置`left`操纵符。在打印学分时数之前，将操纵符设置为右对齐。以下步骤描述该函数：

- 1. 设置左对齐操纵符。
- 2. 打印课程编号。
- 3. 打印课程名称。
- 4. 设置右对齐操纵符。
- 5. 打印学分时数。

函数`print`的定义如下：

```cpp
void courseType::print(ostream& outF)
{
    outF << left;                         //Step 1
    outF << setw(8) << courseNo << "  ";  //Step 2
    outF << setw(15) << courseName;        //Step 3
    outF << right;                         //Step 4
    outF << setw(3) << courseCredits << "  "; //Step 5
} //end print
```

构造函数使用默认值声明。如果在声明`courseType`对象时未指定任何值，则构造函数使用默认值初始化该对象。使用默认值时，对象的成员变量按如下方式初始化：`courseNo`为空白，`courseName`为空白，`courseCredits`为0。否则，使用对象声明中指定的值初始化对象。其定义如下：

```cpp
courseType::courseType(string cName, string cNo, int credits)
{
    courseName = cName;
    courseNo = cNo;
    courseCredits = credits;
} //end default constructor
```

