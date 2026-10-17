
你不能将 `GradedActivity` 的地址赋值给 `FinalExam` 指针。这是因为 `FinalExam` 拥有超出 `GradedActivity` 的功能。有趣的是，C++ 编译器允许你进行转换，如下所示：

```cpp
// 创建一个 GradedActivity 对象。
GradedActivity *gaPointer = new GradedActivity(88.0);
```

```cpp
// 这可行，但有限制。
FinalExam *fePointer = static_cast<FinalExam*>(gaPointer);
```

在执行此代码后，派生类指针 `fePointer` 将指向一个基类对象。我们可以使用指针访问成员，但只能访问存在的成员。以下代码演示了：

```cpp
// 这可行。对象有 getScore 函数。
cout << fePointer->getScore() << endl;
```

```cpp
// 这可行。对象有 getLetterGrade 函数。
cout << fePointer->getLetterGrade() << endl;
```

```cpp
// 这可以通过编译，但在运行时会发生错误。
// 对象没有 getPointsEach
cout << fePointer->getPointsEach() << endl;
```

在此代码中，`fePointer` 是一个 `FinalExam` 指针，它指向一个 `GradedActivity` 对象。前两个代码语句有效，因为 `GradedActivity` 对象有 `getScore` 和 `getLetterGrade` 成员函数。最后一条会导致错误，因为它调用了 `getPointsEach` 成员函数。

# 重定义与覆盖

之前你学过派生类可以重定义基类函数。当一个类重定义一个虚拟函数时，说该类覆盖了该函数。在 C++ 中，重定义和覆盖的区别在于，覆盖是动态绑定的，而重定义是静态绑定的。只有虚拟函数可以被覆盖。

# 虚拟析构函数

当你编写带有析构函数的类时，且该类可能成为基类时，你应该始终将析构函数声明为虚拟。这是因为如果不声明为虚拟，编译器将对析构函数执行静态绑定。当基类指针或引用变量引用派生对象时，这会导致问题。

## 15.6 多态与虚成员函数

派生类有自己的析构函数，当对象被销毁或超出范围时，该析构函数不会执行。只有基类的析构函数会执行。程序 15-15 展示了这一点。

### 程序 15-15

```cpp
1 #include <iostream>
2 using namespace std;
3
4 // Animal 是一个基类。
5 class Animal
6 {
7 public:
8 // 构造函数
9 Animal()
10 { cout << "Animal constructor executing.\n"; }
11
12 // 析构函数
13 ~Animal()
14 { cout << "Animal destructor executing.\n"; }
15 };
16
17 // Dog 类派自 Animal
18 class Dog : public Animal
19 {
20 public:
21 // 构造函数
22 Dog() : Animal()
23 { cout << "Dog constructor executing.\n"; }
24
25 // 析构函数
26 ~Dog()
27 { cout << "Dog destructor executing.\n"; }
28 };
29
30 //***************************************************
31 /* main 函数
32 /***************************************************
33
34 int main()
35 {
36 // 创建一个 Dog 对象，由一个
37 // Animal 指针引用。
38 Animal *myAnimal = new Dog;
39
40 // 删除 dog 对象。
41 delete myAnimal;
42 return 0;
43 }
```

程序输出：
```
Animal constructor executing.
Dog constructor executing.
Animal destructor executing.
```

该程序声明了两个类：`Animal` 和 `Dog`。`Animal` 是基类，`Dog` 是派生类。每个类都有它们自己的构造函数和析构函数。在第 38 行，创建了一个 `Dog` 对象，并将其地址存储在 `Animal` 指针中。`Animal` 和 `Dog` 的构造函数都执行了。在第 41 行，该对象被删除了。然而，当该语句执行时，只有 `Animal` 的析构函数执行了。`Dog` 的析构函数没有执行，因为该对象是通过 `Animal` 指针引用的。我们可以通过将 `Animal` 析构函数声明为虚函数来解决这个问题，如程序 15-16 所示。

### 程序 15-16

```cpp
#include <iostream>
using namespace std;

// Animal 是一个基类。
class Animal {
public:
    // 构造函数
    Animal() {
        cout << "Animal constructor executing.\n";
    }
    // 析构函数
    virtual ~Animal() {
        cout << "Animal destructor executing.\n";
    }
};

// Dog 类派自 Animal
class Dog : public Animal {
public:
    // 构造函数
    Dog() : Animal() {
        cout << "Dog constructor executing.\n";
    }
    // 析构函数
    ~Dog() {
        cout << "Dog destructor executing.\n";
    }
};
********************************
// main 函数
**********************************
int main() {
    // 创建一个 Dog 对象，由一个
    Animal *myAnimal = new Dog;
    // 删除 dog 对象。
    delete myAnimal;
    return 0;
}
```

程序输出：
```
Animal constructor executing.
Dog constructor executing.
Dog destructor executing.
Animal destructor executing.
```

此程序中唯一变化的地方是在第 13 行将 `Animal` 类的析构函数声明为虚函数。因此，析构函数在运行时动态绑定。当 `Dog` 对象被销毁时，`Animal` 和 `Dog` 的析构函数都执行了。

良好的编程习惯是，任何具有虚函数的类都应该也具有虚析构函数。如果类不需要析构函数，它也应该有一个不执行任何语句的虚析构函数。记住，当基类函数被声明为虚函数时，派生类中该函数的所有覆盖版本会自动变成虚函数。在基类中包含虚析构函数（即使是空的），将确保任何派生类的析构函数也是虚函数。

## C++ 11 的 override 和 final 关键字

C++ 11 引入了 `override` 关键字以帮助防止覆盖虚函数时出现细微错误。例如，你能找到程序 15-17 中的错误吗？

### 程序 15-17

```cpp
1 // 此程序在虚函数中有一个细微错误。
2 #include <iostream>
3 using namespace std;
4
5 class Base
6 {
7 public:
8 virtual void functionA(int arg) const
9   { cout << "This is Base::functionA" << endl; }
10 };
11
12 class Derived : public Base
13 {
14 public:
15 virtual void functionA(long arg) const
16   { cout << "This is Derived::functionA" << endl; }
17 };
18
19 int main ()
20 {
21   // 分配 Derived 类的实例。
22   Base *b = new Derived();
23   Derived *d = new Derived();
24
25   // 使用两个指针调用 functionA。
26   b->functionA(99);
                   // (程序继续)
```

### 程序 15-17（续）

```cpp
27   d->functionA(99);
28   return 0;
29
30 }
```

程序输出：
```
This is Base::functionA
This is Base::functionA
```

此程序在虚函数中有一个细微错误。输出显示，即使使用派生类指针 `d`，调用的也是基类版本的 `functionA`。当我们在第 26 行和 27 行调用 `functionA` 时，人们可能期望调用派生类的版本。然而，由于派生类的参数是 `long` 而基类的参数是 `int`，它并没有真正覆盖该函数。为了修复这个问题，我们可以在派生类中使用 `override` 关键字。

### 程序 15-18

```cpp
1 // 此程序演示了 override 关键字。
2 #include <iostream>
3 using namespace std;
4
5 class Base
6 {
7 public:
8 virtual void functionA(int arg) const
9   { cout << "This is Base::functionA" << endl; }
10 };
11
12 class Derived : public Base
13 {
14 public:
15 void functionA(int arg) const override
16   { cout << "This is Derived::functionA" << endl; }
17 };
```

## 15.7 抽象基类与纯虚函数

- 概念：抽象基类不能实例化，但其他类派生自它。纯虚函数是基类中必须被覆盖的成员函数。当一个类包含一个纯虚函数作为成员时，该类就变成了抽象基类。

有时从抽象基类开始类层次结构是有帮助的。抽象基类不实例化，但作为其他类的基类。抽象基类代表了所有派自它的类的通用或抽象形式。

例如，考虑一个制造飞机的工厂。该工厂不制造通用飞机，而是制造三种飞机：两种型号的驱动飞机和一种支线飞机模型。分类飞机的计算机软件可以使用一个名为 `Airplane` 的抽象基类。该类具有表示所有飞机的共同特征的成员。此外，它为工厂制造的三种特定飞机模型各有一个类。这些类具有表示每种类型飞机的独特特性。

当一个类的一个或多个成员函数是纯虚拟函数时，该类就变成抽象基类。纯虚拟函数是以类似于以下方式声明的成员函数：

```cpp
virtual void showInfo() = 0;
```

`= 0` 表示 `showInfo` 是一个纯虚拟函数。纯虚拟函数在基类中没有体或定义。它们必须在派生类中被重写。此外，类中存在纯虚拟函数会阻止程序实例化该类。如果你尝试定义抽象基类的对象，编译器将生成错误。

例如，查看下面的抽象基类 `Student`。它持有所有学生共有的数据，但不包含特定专业学生所需的所有数据。

### Student.h 的内容

```cpp
// Student 类的规范文件
#ifndef STUDENT_STUDENT_H
#define STUDENT_STUDENT_H
#include <string>
using namespace std;

class Student {
protected:
    string name;                // 学生姓名
    string idNumber;            // 学生 ID
    int yearAdmitted;           // 学生入学年份
public:
    // 默认构造函数
    Student() { 
        name = "";
        idNumber = "";
        yearAdmitted = 0; 
    }
    // 构造函数
    Student(string n, string id, int year) { 
        set(n, id, year); 
    }
    // set 函数设置属性数据。
    void set(string n, string id, int year) { 
        name = n;                // 分配姓名
        idNumber = id;             // 分配 ID
        yearAdmitted = year;      // 分配年份
    }
    // 访问函数
    const string getName() const { return name; }
    const string getIdNum() const { return idNumber; }
    int getYearAdmitted() const { return yearAdmitted; }
    // 纯虚拟函数
    virtual int getRemainingHours() const = 0;
};
#endif
```

`Student` 类包含了用于存储学生姓名、ID 号和入学年份的成员。它还拥有构造函数以及用于设置 `idNumber` 和 `yearAdmitted` 成员值的修改函数。提供了访问函数来返回 `name`、`idNumber` 和 `yearAdmitted` 成员中的值。还声明了一个名为 `getRemainingHours` 的纯虚拟函数。

纯虚拟函数必须在派自 `Student` 的类中被重写。它被设为纯虚拟函数是因为该类旨在作为特定专业学生类的基类。例如，`CsStudent` 可能持有计算机学生的数据，而 `BiologyStudent` 可能持有生物学生的数据。计算机科学学生修的课程与生物学生不同。因此，`CsStudent` 计算学时的方式将与 `BiologyStudent` 类不同。

让我们来看 `CsStudent` 类的示例。

### CsStudent.h 的内容

```cpp
// CsStudent 类的规范文件
#ifndef CSSTUDENT_H
#define CSSTUDENT_H
#include "Student.h"
// 所需学时的常量
const int MATH_HOURS = 20; // 数学学时
const int CS_HOURS = 40; // 计算机科学学时
const int GEN_ED_HOURS = 60; // 通用教育学时

class CsStudent : public Student {
private:
    int mathHours; // 修过的数学学时
    int csHours; // 修过的计算机科学学时
    int genEdHours; // 修过的通用教育学时
public:
    // 默认构造函数
    CsStudent() : Student() { 
        mathHours = 0;
        csHours = 0;
        genEdHours = 0; 
    }
    // 构造函数
    CsStudent(string n, string id, int year) :
        Student(n, id, year)
    { 
        mathHours = 0;
        csHours = 0;
        genEdHours = 0; 
    }
    // 修改函数
    void setMathHours(int mh) { mathHours = mh; }
    void setCsHours(int csh) { csHours = csh; }
    void setGenEdHours(int geh) { genEdHours = geh; }
    // 重写的 getRemainingHours 函数，
    // 定义在 CsStudent.cpp 中
    virtual int getRemainingHours() const override;
};
#endif
```
