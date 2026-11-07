
```cpp
#include <iostream>
#include <fstream>
#include <string>
#include "studentType.h"

using namespace std;

const int MAX_NO_OF_STUDENTS = 10;

void getStudentData(ifstream& infile,
                    studentType studentList[],
                    int numberOfStudents);

void printGradeReports(ofstream& outfile,
                       studentType studentList[],
                       int numberOfStudents,
                       double tuitionRate);

int main()
{
    studentType studentList[MAX_NO_OF_STUDENTS];

    int noOfStudents;
    double tuitionRate;
    ifstream infile;
    ofstream outfile;

    infile.open("stData.txt");

    if (!infile)
    {
        cout << "The input file does not exist. "
             << "Program terminates." << endl;
        return 1;
    }

    outfile.open("sDataOut.txt");

    infile >> noOfStudents; //get the number of students
    infile >> tuitionRate; //get the tuition rate

    getStudentData(infile, studentList, noOfStudents);
    printGradeReports(outfile, studentList,
                      noOfStudents, tuitionRate);

    return 0;
}

//Place the definitions of the functions getStudentData and
//printGradeReports here.
```

## 示例运行

学生姓名：丽莎·米勒
学生 ID：890238
已选课程数：4

| 课程编号 | 课程名称 | 学分 | 成绩 |
| --- | --- | --- | --- |
| CSC478 | 计算机科学 | 3 | B |
| HIS356 | 历史 | 3 | A |
| MTH345 | 数学 | 4 | A |
| PHY357 | 物理 | 3 | B |

总学分时数：13
期中 GPA：3.54
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-

学生姓名：比尔·威尔顿
学生 ID：798324
已选课程数：5

| 课程编号 | 课程名称 | 学分 | 成绩 |
| --- | --- | --- | --- |
| BIO234 | 生物学 | 4 | *** |
| CHM256 | 化学 | 4 | *** |
| ENG378 | 英语 | 3 | *** |
| MTH346 | 数学 | 3 | *** |
| PHL534 | 哲学 | 3 | *** |

总学分时数：17
*** 因未缴学费，成绩暂缓公布。***
应缴金额：$5865.00
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-

学生姓名：丹迪·戈特
学生 ID：746333
已选课程数：6

| 课程编号 | 课程名称 | 学分 | 成绩 |
| --- | --- | --- | --- |
| BUS128 | 商业 | 3 | C |
| CHM348 | 化学 | 4 | B |
| CSC201 | 计算机科学 | 3 | B |
| ENG328 | 英语 | 3 | B |
| HIS101 | 历史 | 3 | A |
| MTH137 | 数学 | 3 | A |

总学分时数：19
期中 GPA：3.16
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-

## 输入文件

```
3 345
Lisa Miller 890238 Y 4
Mathematics MTH345 4 A
Physics PHY357 3 B
ComputerSci CSC478 3 B
History HIS356 3 A

Bill Wilton 798234 N 5
English ENG378 3 B
Philosophy PHL534 3 A
Chemistry CHM256 4 C
Biology BIO234 4 A
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

- 1. 继承与组合（聚合）是将两个或多个类关联起来的有意义的方式。
- 2. 继承是一种“is-a”（是）关系。
- 3. 组合（聚合）是一种“has-a”（有）关系。
- 4. 在单继承中，派生类仅从一个称为基类的现有类派生。
- 5. 在多继承中，派生类从多个基类派生。
- 6. 基类的私有成员对基类是私有的。派生类不能直接访问它们。
- 7. 基类的公有成员可以由派生类以公有或私有方式继承。
- 8. 派生类可以重定义基类的成员函数，但这种重定义仅适用于派生类的对象。
- 9. 对基类构造函数（带参数）的调用在派生类构造函数定义头部指定。
- 10. 如果在派生类构造函数定义头部未指定对基类构造函数（带参数）的调用，那么在派生类对象声明和初始化期间，将执行基类的默认构造函数（如果有）。
- 11. 初始化派生类对象时，先执行基类的构造函数。
- 12. 复习本章给出的继承规则。
- 13. 在组合（聚合）中，一个类的成员是另一个类的对象。
- 14. 在组合（聚合）中，对成员对象构造函数的调用在类构造函数定义头部指定。
- 15. 面向对象设计（OOD）的三个基本原则是封装、继承和多态。
- 16. 识别类、对象和操作的一种简单方法是用英语描述问题，然后找出所有名词和动词。从名词列表中选择类（对象），从动词列表中选择操作。

## 练习

练习末尾括号中的数字指本章开头列出的学习目标。

- 1. 判断以下陈述为真或假。
  - a. 在单继承中，一个基类只能创建一个派生类。(1)
  - b. 基类的 `public` 成员在派生类中只能作为 `public` 成员继承。(2)
  - c. 要在派生类中重定义（或覆盖）基类的成员函数，相应的成员函数必须具有相同的名称、数量和参数类型。(3)
  - d. 如果派生类没有覆盖基类的 `public` 成员函数，可以通过使用该函数名和适当的参数列表来指定对该 `public` 成员函数的调用。(3)
  - e. 派生类的构造函数可以在函数定义头部指定对基类构造函数的调用。(4)
  - f. 派生类的构造函数可以使用类名指定对基类构造函数的调用。(4)
  - g. 假设 x 和 y 是类，x 的一个成员变量是 y 类型的对象，且两个类都有构造函数。x 的构造函数通过使用 y 类型对象名来指定对 y 的构造函数的调用。(4)
  - h. 当派生类的析构函数执行时，它会自动调用基类的析构函数。(5)

```cpp
double getZ();
double power();
    //returns x to the power of z.

private:
    double z;
};
```

- 10. 假设类 `temp` 的定义如练习 9 所示。考虑以下类定义：(2, 3, 4)

```cpp
class derivedFromTemp: public temp
{
public:
    void print();
        //outputs the values of all the instance variables.
    void set(double);
        //sets the value of z according to the parameter.
    double getZ();
        //returns the value of z.
    double power() const;
        //returns x to the power of z.

    derivedFromTemp();
        //sets the values of instance variables to "",
        //0.0, and 0.0, respectively.
    derivedFromTemp(string, double, double);
        //sets the values of instance variables according
        //to the parameters.
private:
    double z;
};
```

  - a. 指出并改正 `derivedFromTemp` 类定义中的错误（如果有），并给出该类的正确��义。
  - b. 改正 `derivedFromTemp` 类定义中的错误（如果有）后，编写该类成员函数的定义。

- 11. 考虑以下语句：(3)

```cpp
class base                 class derived: public base
{                          {
public:                    public:
    void print() const;       .
    void set(int, int);       .
    void get(int&, int&);     .
    base();                   private:
    base(int, int);               int c;
private:                    };
    int a;
    int b;
};
```

  - a. 假设 `class derived` 覆盖了 `class base` 的函数 `print`。在 `class derived` 中，函数 `print` 的头部是什么？
  - b. 假设该类重载了 `class base` 的函数 `set` 和 `get`。在 `class derived` 中，这些函数的头部是什么？

- 12. 解释在派生类中覆盖和重载基类成员函数之间的区别。(3)
- 13. 假设类 `three` 派生自类 `two`，类 `two` 派生自类 `one`，且每个类都有实例变量。假设类 `three` 的对象进入作用域，因此这些类的构造函数将执行。确定这些类构造函数的执行顺序。(4)
- 14. 考虑以下类定义：(2, 8)

```cpp
class smart
{
public:
    void print() const;
    void set(int, int);
    int sum();
    smart();
    smart(int, int);
private:
    int x;
    int y;
    int secret();
};

class superSmart: public smart
{
public:
    void print() const;
    void set(int, int, int);
    int manipulate();
    superSmart();
    superSmart(int, int, int);
private:
    int z;
};
```

  - a. `smart` 的哪些私有成员（如果有）是 `superSmart` 的公有成员？
  - b. 在 `class superSmart` 中，`class smart` 的哪些成员、函数和/或数据可以直接访问？

- 15. 假设类 `smart` 和 `superSmart` 的定义如练习 14 所示。假设以下语句位于用户程序（客户端代码）中：

```cpp
smart smartObject;
superSmart superSmartObject;
```

判断以下语句是有效还是无效。如果语句无效，请解释原因。(2, 3, 4)

  - a.

```cpp
int smart::sum()
{
    return x + y + z;
}
```
