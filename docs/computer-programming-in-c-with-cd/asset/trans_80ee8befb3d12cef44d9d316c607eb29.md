
- **private（私有）：** 使类的成员仅对同一类内的代码可访问或可见。注意，默认情况下，类的成员是私有的。
- **protected（受保护）：** 使类的成员仅在同一类及其派生类内部可访问或可见。
- **public（公有）：** 使类的成员对类内外的代码可访问或可见。

这些访问说明符在类中使用时，为类成员提供不同的可访问性（或可见性）。访问说明符后必须跟冒号（:）符号，如下代码片段所示：

```cpp
#include<iostream.h>

class Student
{
    private:                //Optional to use private: here, as all members are
                            private by default
    char sname[20];
    int s_roll_no, sage, sclass;
    protected:
    char fatherName[20];
    public:
    int ssubject,smarks;
};

int main()
{
    Student object1;
    cout<<"Enter student's Name"<<endl;
    cin>>object1.sname;    //Not Accessible, compiler will give error for it
    cout<<"Enter student's father name"<<endl;
    cin>>object1.fatherName;  //Not Accessible, compiler will give error for it
    cout<<"Enter subject code"<<endl;
    cin>>object1.ssubject;    //Accessible
    cout<<"Enter marks scored by student"<<endl;
    cin>>object1.smarks;      //Accessible
    return 0;
}
```

在前面的代码片段中，Student 类中数据成员的作用域通过使用 public、protected 和 private 关键字受到限制。在 private 关键字（后跟冒号（:））之后声明的数据成员表示这些成员不能在 Student 类边界之外访问。private 关键字是可选的（此处只是为了清晰起见而使用），因为默认情况下类的所有成员都是私有的。在 protected 关键字（后跟冒号（:））之后声明的数据成员表示这些成员不能在 Student 类之外访问，但可以在 Student 类的派生类内访问。在 public 关键字（后跟冒号（:））之后声明的数据成员表示 Student 类的这些成员可以在类结构之外通过 Student 类的对象（在我们的例子中为 object1）访问。

除了数据成员之外，类体内还有成员函数。让我们学习如何在类中创建成员函数。

## 创建成员函数

有时，即使程序员可以获得大型程序的算法，实现它也很困难。你可以通过将这样的程序拆分成多个可独立设计、实现和管理的任务来实现它。将大型程序拆分成小型可管理任务的过程称为模块化编程。在模块化编程中，程序中重复的一组指令可以组织为函数。定义为类的一部分的函数称为类的方法或成员函数。在类中定义方法有两种方式：内部方式和外部方式。在内部方式中，你在类体内定义成员函数。然而，在外部方式中，你使用作用域解析（::）运算符在类体外部定义成员函数。

清单 1 展示了如何在类中定义函数（你可以在 CD 的 code\chapter6 文件夹中的 InFunction.cpp 文件中找到此示例）：

### ▶ 清单 1：在类中定义函数

```cpp
#include<iostream.h>

class Student
{
    private:
    char s_name[20];
    int s_roll_no,s_age, s_class;
    protected:
    char father_name[20];
    public:
    int s_subject,s_marks;

    void inputData()
    {
        cout<<"Enter student's roll number"<<endl;
        cin>>s_roll_no;
        cout<<"Enter student's name"<<endl;
        cin>>s_name;
        cout<<"Enter student's age"<<endl;
        cin>>s_age;
        cout<<"Enter student's class"<<endl;
        cin>>s_class;
        cout<<"Enter subject code"<<endl;
        cin>>s_subject;
        cout<<"Enter marks scored by student"<<endl;
        cin>>s_marks;
    }

    void displayData()
    {
        cout<<"Student's Roll Number:"<<s_roll_no<<endl;
        cout<<"Student's Name:"<<s_name<<endl;
        cout<<"Student's Age:"<<s_age<<endl;
        cout<<"Student's Class:"<<s_class<<endl;
        cout<<"Subject Code:"<<s_subject<<endl;
        cout<<"Student's Marks:"<<s_marks<<endl;
    }
};

int main()
{
    Student object1;
    object1.inputData();
    object1.displayData();
    return 0;
}
```

### 输出：

```text
Enter student's roll number
1001
Enter student's name
Kabir
Enter student's age
12
Enter student's class
7
Enter subject code
104
Enter marks scored by student
87
Student's Roll Number:1001
Student's Name:Kabir
Student's Age:12
Student's Class:7
Subject Code:104
Student's Marks:87
```

在清单 1 中，Student 类有两个成员函数——`inputData()` 和 `displayData()`。这两个函数的返回类型都是 `void`。`inputData()` 方法执行接受学生信息（如学号、姓名和分数）的任务。另一方面，`displayData()` 方法用于显示这些学生的信息。

除了在类定义内部定义方法之外，还有一种外部方式，通过使用作用域解析运算符在类结构外部定义方法体。清单 2 展示了如何使用作用域解析运算符在类结构外部编写成员函数定义（你可以在 CD 的 code\chapter6 文件夹中的 ExFunction.cpp 文件中找到此示例）：

### ▶ 清单 2：使用作用域解析运算符在类外定义函数

```cpp
#include<iostream.h>

class Student
{
    private:
    char sname[20];
    int sage,sclass;
    protected:
    char fatherName[20];
    public:
    int ssubject,smarks;
    void inputData();
    void displayData();
};

void Student::inputData()
{
    cout<<"Enter student's name"<<endl;
    cin>>sname;
    cout<<"Enter student's age"<<endl;
    cin>>sage;
    cout<<"Enter student's class"<<endl;
    cin>>sclass;
    cout<<"Enter subject code"<<endl;
    cin>>ssubject;
    cout<<"Enter marks scored by student"<<endl;
    cin>>smarks;
}

void Student::displayData()
{
    cout<<"Student's Name:"<<sname<<endl;
    cout<<"Student's Age:"<<sage<<endl;
    cout<<"Student's Class:"<<sclass<<endl;
    cout<<"Subject Code:"<<ssubject<<endl;
    cout<<"Student's Marks:"<<smarks<<endl;
}

int main()
{
    Student object1;
    object1.inputData();
    object1.displayData();
    return 0;
}
```

### 输出：

```text
Enter student's roll number
1001
Enter student's name
Kabir
Enter student's age
12
Enter student's class
7
Enter subject code
104
Enter marks scored by student
87
Student's Roll Number:1001
Student's Name:Kabir
Student's Age:12
Student's Class:7
Subject Code:104
Student's Marks:87
```

在清单 2 中，Student 类有两个成员函数 `inputData()` 和 `displayData()` 的声明。没有定义的函数声明也称为函数原型。`inputData()` 和 `displayData()` 函数的返回类型是 `void`。`inputData()` 函数使用作用域解析运算符（`::`）在 Student 类边界之外定义。考虑以下代码片段：

```cpp
void Student::inputData()
{
...
...
...
}
```

在前面的代码片段中，`void` 是 `inputData()` 函数的返回类型。Student 是用户定义类的名称，后面跟作用域解析运算符（`::`），而 `inputData()` 是在 Student 类中声明的函数名称。`inputData()` 函数在 Student 类边界之外定义，用于接受任何学生的信息，例如学号、姓名和分数。

与 `inputData()` 函数类似，`displayData()` 函数也是 Student 类的类成员。`displayData()` 函数也使用作用域解析运算符（`::`）在 Student 类边界之外定义。考虑以下代码片段：

```cpp
void Student::displayData()
{
...
...
...
}
```

在前面的代码片段中，`void` 是 `displayData()` 函数的返回类型，Student 是用户定义类的名称，后面跟作用域解析运算符（`::`）。然而，`displayData()` 函数用于显示学生信息。

在 C++ 中，类中声明的函数默认是私有的。然而，你可以分别使用 private、protected 或 public 关键字，将类中的函数显式设为私有、受保护或公有。类中定义的函数通过使用点（`.`）运算符或类成员访问间接（`->`）运算符来调用。以下代码片段展示了使用点运算符进行函数访问：

```cpp
object1.inputData();
```

在前面的代码片段中，`object1` 是 Student 类对象的名称，`inputData()` 是该类的一个函数。

让我们在类中创建以下函数：

- 一个 const 函数
- 一个嵌套函数

## 创建 const 函数

const 函数不允许修改类中数据成员的值。清单 3 展示了一个 const 函数的示例（你可以在 CD 的 code\chapter6 文件夹中的 ConstFunction.cpp 文件中找到此示例）：

### ▶ 清单 3：在类中创建 const 函数

```cpp
#include<iostream.h>

class ConstFunction
{
    int x,y;
    public:
    void setval();
    void display() const;
    // prototype of a const function
};
```
