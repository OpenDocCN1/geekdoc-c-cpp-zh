

```cpp
string cName;    //变量存储课程名称
string cNo;      //变量存储课程编号
int credits;     //变量存储学分数

int count;       //循环控制变量
int i;           //循环控制变量

courseType courses[6];        //对象数组，用于存储
                              //课程信息
char cGrades[6];              //数组，用于存储课程成绩

for (count = 0; count < numberOfStudents; count++)
{
    infile >> fName >> lName >> ID >> isPaid;    //步骤1

    if (isPaid == 'Y')                           //步骤2
        isTuitionPaid = true;
    else
        isTuitionPaid = false;

    infile >> noOfCourses;                       //步骤3

    for (i = 0; i < noOfCourses; i++)            //步骤4
    {
        infile >> cName >> cNo >> credits
               >> cGrades[i];                    //步骤4.a
        courses[i].setCourseInfo(cName, cNo,
                                  credits);       //步骤4.b
    }
    studentList[count].setInfo(fName, lName, ID,
                               noOfCourses,
                               isTuitionPaid,
                               courses, cGrades); //步骤5
} //end for
} //end getStudentData
```

**函数 `printGradeReports`**

该函数用于打印成绩报告。对于每个学生，它调用类 `studentType` 的成员函数 `print` 来打印成绩报告。函数 `printGradeReports` 的定义如下：

```cpp
void printGradeReports(ofstream& outfile,
                       studentType studentList[],
                       int numberOfStudents,
                       double tuitionRate)
{
    int count;
    for (count = 0; count < numberOfStudents; count++)
        studentList[count].print(outfile, tuitionRate);
} //end printGradeReports
```

## 程序清单

```cpp
//***************************************************************
// 作者：D. S. Malik
//
// 类 courseType
// 该类指定成员以实现课程的信息。
//***************************************************************

#ifndef H_courseType
#define H_courseType

#include <fstream>
#include <string>

using namespace std;

//类 courseType 的定义在此处。
.
.
.
#endif
```

```cpp
//***************************************************************
// 作者：D. S. Malik
//
// 实现文件 courseTypeImp.cpp
// 该文件包含实现类 courseType 操作的函数定义。
//***************************************************************

#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>
#include "courseType.h"

using namespace std;

//类 courseType 的成员函数的定义
//在此处。
.
.
.
```

```cpp
//***************************************************************
// 作者：D. S. Malik
//
// 类 personType
// 该类指定成员以实现个人的名和姓。
//***************************************************************

#ifndef H_personType
#define H_personType

#include <string>

using namespace std;

//类 personType 的定义在此处。
.
.
.
#endif
```

```cpp
//***************************************************************
// 作者：D. S. Malik
//
// 实现文件 personTypeImp.cpp
// 该文件包含实现类 personType 操作的函数定义。
//***************************************************************

#include <iostream>
#include <string>
#include "personType.h"

using namespace std;

//类 personType 的成员函数的定义
//在此处。
.
.
.
```

```cpp
//***************************************************************
// 作者：D. S. Malik
//
// 类 studentType
// 该类指定成员以实现学生的信息。
//***************************************************************
```

## 示例运行

学生姓名：Lisa Miller  
学生ID：890238  
注册课程数：4  

| 课程编号 | 课程名称 | 学分 | 成绩 |
|---|---|---|---|
| CSC478 | 计算机科学 | 3 | B |
| HIS356 | 历史 | 3 | A |
| MTH345 | 数学 | 4 | A |
| PHY357 | 物理 | 3 | B |

总学分数：13  
期中GPA：3.54  
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-

学生姓名：Bill Wilton  
学生ID：798324  
注册课程数：5  

| 课程编号 | 课程名称 | 学分 | 成绩 |
|---|---|---|---|
| BIO234 | 生物 | 4 | *** |
| CHM256 | 化学 | 4 | *** |
| ENG378 | 英语 | 3 | *** |
| MTH346 | 数学 | 3 | *** |
| PHL534 | 哲学 | 3 | *** |

总学分数：17  
*** 因未缴纳学费，成绩暂被扣留。 ***  
应缴金额：$5865.00  
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-

学生姓名：Dandy Goat  
学生ID：746333  
注册课程数：6  

| 课程编号 | 课程名称 | 学分 | 成绩 |
|---|---|---|---|
| BUS128 | 商务 | 3 | C |
| CHM348 | 化学 | 4 | B |
| CSC201 | 计算机科学 | 3 | B |
| ENG328 | 英语 | 3 | B |
| HIS101 | 历史 | 3 | A |
| MTH137 | 数学 | 3 | A |

总学分数：19  
期中GPA：3.16  
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-

## 输入文件

```text
3 345
Lisa Miller 890238 Y 4
Mathematics MTH345 4 A
Physics PHY357 3 B
ComputerSci CSC478 3 B
History HIS356 3 A

Bill Wilton 798324 N 5
English ENG378 3 B
Philosophy PHL534 3 A
Chemistry CHM256 4 C
Biology BIO234 4 C
Mathematics MTH346 3 C

Dandy Goat 746333 Y 6
History HIS101 3 A
English ENG328 3 B
Mathematics MTH137 3 A
Chemistry CHM348 4 B
ComputerSci CSC201 3 B
Business BUS128 3 C
```

## 快速回顾

1. 继承和组合（聚合）是关联两个或更多类的有意义的方式。
2. 继承是“是一种”（is-a）关系。
3. 组合（聚合）是“有一个”（has-a）关系。
4. 在单一继承中，派生类仅从现有的一个类（称为基类）派生而来。
5. 在多重继承中，派生类从多个基类派生而来。
6. 基类的**私有**成员对于基类来说是**私有**的。派生类不能直接访问它们。
7. 基类的**公有**成员可以被派生类以**公有**或**私有**方式继承。
8. 派生类可以重新定义基类的成员函数，但这种重新定义仅适用于派生类的对象。
9. 对基类构造函数（带参数）的调用在派生类构造函数定义的头部指定。
10. 如果在派生类构造函数定义的头部未指定对基类构造函数（带参数）的调用，则在派生类对象声明和初始化期间，将执行基类的默认构造函数（如果有的话）。
11. 在初始化派生类对象时，首先执行基类的构造函数。
12. 复习本章给出的继承规则。
13. 在组合（聚合）中，类的成员是另一个类的对象。
14. 在组合（聚合）中，对成员对象构造函数的调用在类的构造函数定义的头部指定。
15. 面向对象设计的三个基本原则是封装、继承和多态。
16. 识别类、对象和操作的一种简单方法是用英语描述问题，然后找出所有的名词和动词。从名词列表中选择类（对象），从动词列表中选择操作。

## 练习

1. 判断下列陈述为真或假。

   a. 派生类的构造函数可以在函数定义的头部指定对基类构造函数的调用。

   b. 派生类的构造函数可以使用类的名称指定对基类构造函数的调用。

   c. 假设x和y是类，x的某个成员变量是y类型的对象，并且两个类都有构造函数。x的构造函数通过使用y类型的对象名来指定对y构造函数的调用。

2. 绘制一个类层次结构，其中多个类从单个基类派生。

3. 假设类employeeType是从类personType派生的（参见第12章示例12-9）。给出可以添加到类employeeType中的成员（数据和函数）的示例。

4. 考虑以下语句：

   ```cpp
   class dog: public animal
   {
       ...
   } ;
   ```

   在此声明中，哪个类是基类，哪个类是派生类？

