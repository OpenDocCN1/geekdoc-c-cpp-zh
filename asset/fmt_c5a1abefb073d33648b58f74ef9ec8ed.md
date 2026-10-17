
# 检查点

- 1.1 实例成员变量和静态变量有什么区别？
- 1.2 静态成员变量在类声明中声明。你在哪里编写静态成员变量的语句？
- 1.3 静态成员变量是在其类的实例出现之前、与其同时还是之后进入内存的？
- 1.4 静态成员函数有什么局限性？
- 1.5 静态成员函数可以执行哪些实例成员函数不能执行的操作？
- 1.6 如果类 X 将函数 `f` 声明为朋友，函数 `f` 是否成为类 X 的成员？
- 1.7 类 Y 是类 X 的朋友，`friend` 关键字出现在类 Y 的声明中还是类 X 的声明中？

# 成员级赋值

> 概念：`=` 运算符可以将一个对象的数据赋值给另一个对象，或者用另一个对象的数据初始化一个对象。默认情况下，一个对象的每个成员都会被复制到另一个对象中对应的成员中。

与其他变量（数组除外）一样，对象可以使用 `=` 运算符进行相互赋值。例如，考虑程序 14-5，该程序使用了我们在第 13 章中讨论过的 `Rectangle` 类（版本 4）。回想一下 `Rectangle` 类有两个成员变量：`width` 和 `length`。构造函数接受两个参数：一个用于 `width`，一个用于 `length`。

# 程序 14-5

```cpp
// 此程序演示了成员级赋值。

#include <iostream>
#include "Rectangle.h"

using namespace std;

int main() {
    // 定义两个 Rectangle 对象。
    Rectangle box1(10.0, 10.0); // width = 10.0, length = 10.0
    Rectangle box2(20.0, 20.0); // width = 20.0, length = 20.0

    // 显示每个对象的宽度和长度。
    cout << "box1's width and length: " << box1.getWidth() << endl;
    cout << "box2's width and length: " << box2.getWidth() << endl;
    cout << box2.getLength() << endl << endl;

    // 将 box1 的成员赋值给 box2。
    box2 = box1;

    // 再次显示每个对象的宽度和长度。
    cout << "box1's width and length: " << box1.getWidth() << endl;
    cout << box1.getLength() << endl << endl;
    cout << "box2's width and length: " << box2.getWidth() << endl;
    cout << box2.getLength() << endl << endl;

    return 0;
}
```

# 程序输出

box1's width and length: 10 10
box2's width and length: 20 20

box1's width and length: 10 10
box2's width and length: 10 10

# 14.4 拷贝构造函数

出现在第 19 行的语句将 `box1` 的 `width` 和 `length` 成员变量直接复制到 `box2` 的 `width` 和 `length` 成员变量中：

```cpp
box2 = box1;
```

当用另一个对象的值初始化对象时，也会发生成员级赋值。记住赋值和初始化的区别：赋值发生在两个现有对象之间，而初始化发生在正在创建的对象上。考虑以下代码：

```cpp
// 定义 box1。
Rectangle box1(100.0, 50.0);

// 定义 box2，用 box1 的值初始化
Rectangle box2 = box1;
```

最后一条语句定义了一个 `Rectangle` 对象 `box2`，并将其初始化为存储在 `box1` 中的值。由于发生了成员级赋值，`box2` 对象将包含与 `box1` 对象完全相同的值。

# 14.4 拷贝构造函数

> 概念：拷贝构造函数是一种特殊的构造函数，每创建一个新对象并用另一个对象的数据对其进行初始化时，就会被调用。

有时，C++ 中默认的成员级赋值行为是完全可以的。然而，在许多情况下，无法使用成员级赋值。例如，考虑以下类（该文件可以在 Student Source Folder Chapter 14\StudentTestScores Version 1 中找到）。

# StudentTestScores.h 内容（版本 1）

```cpp
#ifndef STUDENTTESTSCORES_H
#define STUDENTTESTSCORES_H

#include <string>

using namespace std;

const double DEFAULT_SCORE = 0.0;

class StudentTestScores
{
private:
    string studentName; // 学生姓名
    double *testScores; // 指向分数数组的指针
    int numTests; // 分数数量

    // 私有成员函数，用于创建
    // 分数数组。
    void createTestScoresArray(int size);
    // (来自 OCR 的实现细节)
    // numTests = new double[size];
    // for (int i = 0; i < size; i++)
    // testScores[i] = DEFAULT_SCORE;

public:
    // 构造函数
    StudentTestScores(string name, int numScores)
    { 
        studentName = name;
        createTestScoresArray(numScores);
    }

    // 析构函数
    ~StudentTestScores()
    { delete testScores; }

    // setTestScore 函数设置特定的
    // 测试分数值。
    void setTestScore(double score, int index)
    { testScores[index] = score; }

    // 设置学生的姓名。
    void setStudentName(string name)
    { studentName = name; }

    // 获取学生的姓名。
    string getStudentName() const
    { return studentName; }

    // 获取分数的数量。
    int getNumTestScores() const
    { return numTests; }

    // 获取特定的测试分数。
    double getTestScore(int index) const
    { return testScores[index]; }
#endif
```

该类存储了一个学生的姓名和测试分数。让我们仔细观察代码：

- 第 11 行到 13 行声明了类的属性。`studentName` 属性是一个字符串对象，保存着学生的姓名。`testScores` 属性是一个指针。它的目的是指向一个存储测试分数的动态分配数组。`numTests` 属性是一个整数，保存分数的数量。
- `createTestScoresArray` 成员函数（第 17 行到 21 行）创建一个存储测试分数的数组。它接受一个分数数量参数，将此值赋值给 `numTests` 属性（第 18 行），为 `testScores` 属性动态分配一个数组（第 19 行）。第 20 行和 21 行的 `for` 循环将数组的每个元素初始化为默认值 0.0。
- 第 25 行到 27 行的构造函数接受姓名和分数数量。在第 26 行，姓名被赋值给 `studentName` 属性，在第 27 行，分数数量传递给 `createTestScoresArray`。
- 第 30 行和 31 行的析构函数释放内存。
- 第 35 行和 36 行的 `setTestScore` 函数设置 `testScores` 属性中的特定分数。该函数接受分数和分数索引的参数。
- `setStudentName` 函数设置学生的姓名。
- `getStudentName` 函数获取学生的姓名。
- `getNumTestScores` 函数获取分数的数量。
- `getTestScore` 函数获取特定的测试分数。
