
答：上述程序的输出如下：

```text
val == 50
&val == 0x0012ff68
ptr_val == 0x0012ff68
*ptr_val == 50
```

### Q11. 以下程序的输出是什么？

```cpp
#include<iostream.h>
int main()
{
    int *a = new int[5];
    int *b=new int[10];
    cout << "b=" << b << endl;
    *(a+5)=9;
    cout << "a[5]=" << *(a+5) << endl;
    delete [] a;
    delete b;
    return 0;
}
```

答：上述程序的输出如下：

```text
b=10
a[5]=9
```

### Q12. 以下程序的输出是什么？

```cpp
#include<iostream.h>
int main()
{
    int fvalue, svalue;
    int * ptr;
    ptr = &fvalue;
    *ptr = 10;
    ptr = &svalue;
    *ptr = 20;
    cout << "firstvalue is " << fvalue << endl;
    cout << "secondvalue is " << svalue << endl;
    return 0;
}
```

答：上述程序的输出如下：

```text
firstvalue is 10
secondvalue is 20
```

`float`、`char` 和 `double`。在 C++ 中创建结构体，需要遵循两个过程。它们是：

- 1. 声明一个结构体，包含结构体名称以及可以存储在结构体中的不同类型的数据成员。
- 2. 定义结构体变量以访问结构体的数据成员。

可以使用 `struct` 关键字定义结构体，如下面的代码片段所示：

```cpp
struct employee          // structure declaration
{
    char name[20];       // an array of characters
    int age;             // an int age member
    float salary;        // a float salary member
    char designation[20]; // an array of characters
};
```

在前面的代码片段中，使用多种不同数据类型的变量（如 `int` 和 `float`）定义了结构体 employee。结构体名称 employee 前面有关键字 `struct`。employee 结构体以左花括号（`{`）开始，以右花括号（`}`）结束。需要注意的是，在右花括号结束后必须跟分号（`;`）。结构体的所有数据成员都指定在这些花括号之间。

定义结构体之后，下一步是声明结构体变量。结构体变量可以声明为全局变量或局部变量。以下代码片段展示了如何声明结构体的全局变量：

```cpp
struct employee
{
    char name[20];
    int age;
    float salary;
    char designation[20];
} employee_one, employee_two;
```

在前面的代码片段中，employee 是结构体名称；employee_one 和 employee_two 是 employee 类型的变量。此外，employee_one 和 employee_two 变量的作用域是全局的，因此它们可以在整个程序中的任何位置使用。

现在，让我们声明结构体的局部变量，如下面的代码片段所示：

```cpp
struct employee
{
    char name[20];
    int age;
    float salary;
    char designation[20];
};

int main()
{
    employee employee_one, employee_two;
    return 0;
}
```

在前面的代码片段中，employee 是一个结构体；employee_one 和 employee_two 是 main() 函数中 employee 类型的变量。然而，employee_one 和 employee_two 变量的作用域是局部的，这意味着这些变量只能在 main() 函数内访问。

清单 1 展示了如何使用 struct 关键字声明结构体，并在 main() 函数中使用结构体实例初始化结构体变量（你可以在光盘的 code\chapter5 文件夹中找到 MyStructure.cpp 文件）。

### 清单 1：声明和定义结构体变量

```cpp
#include<iostream.h>
#include<stdio.h>

struct employee
{
    char name[20];
    int age;
    float salary;
    char designation[20];
};

int main()
{
    employee employee_one;

    cout<<"Enter employee name :";
    gets(employee_one.name);

    cout<<"Enter employee age :";
    cin>>employee_one.age;

    cout<<"Enter employee salary :";
    cin>>employee_one.salary;

    cout<<"Enter employee designation :";
    gets(employee_one.designation);

    cout<<"The information of an employee are: "<<endl;
    cout<<employee_one.name<<endl;
    cout<<employee_one.age<<endl;
    cout<<employee_one.salary<<endl;
    cout<<employee_one.designation<<endl;
    return 0;
}
```

**输出：**

```text
Enter employee name :Mahtab Alam
Enter employee age :25
Enter employee salary :6000
Enter employee designation :Technical Writer
The information of an employee are:
Mahtab Alam
25
6000
Technical Writer
```

在清单 1 中，结构体 employee 在 main() 函数外部声明。该结构体的成员通过在 main() 函数中声明该结构体的变量 employee_one 来访问。访问和初始化结构体元素的过程将在下一节中说明。

## 访问和初始化结构体元素

每个结构体都有一些元素，称为结构体成员，它们声明在结构体的左花括号和右花括号之间（称为结构体主体）。定义结构体时，必须为结构体变量提供一个名称，以便在 C++ 程序中访问它。你可以在结构体变量名和结构体元素（结构体成员）之间使用点（.）运算符来访问和初始化结构体元素。访问结构体元素的语法如下：

```cpp
structure_variable_name.structure_element;
```

在以下代码片段中，employee 结构体的结构体元素（name）通过结构体变量名（employee_one）进行访问：

```cpp
employee_one.name;
```

同样，你可以使用点运算符（.）初始化结构体元素，如下面的代码片段所示：

```cpp
employee_one.name = "Mohan";
employee_one.age = 22;
```

清单 2 展示了如何访问和初始化结构体成员（你可以在光盘的 code\chapter5 文件夹中找到 HeightStructure.cpp 文件）：

### 清单 2：访问和初始化结构体成员

```cpp
#include <iostream.h>
#include <stdio.h>

struct length
{
    int feet;
    int inch;
};

int main()
{
    length height;

    height.feet = 5;
    height.inch = 10;

    cout<<"Your height is : ";
    cout<<height.feet<<" feet ";
    cout<<height.inch<<" inch";

    return 0;
}
```

**输出：**

```text
Your height is : 5 feet 10 inch
```

在清单 2 中，声明了结构体 length，它包含两个整数元素 feet 和 inch。然后，在 main() 函数中声明了结构体 length 的变量（height）。该对象用于通过点（.）运算符访问结构体 length 的元素。

## 测试你的知识

### Q1. 使用结构体创建一个程序，接受学生 ID 和学生姓名，并将它们显示在屏幕上。

答：

```cpp
#include <iostream.h>

struct Student
{
    char name[20];
    int ID;
};

int main()
{
    cout<<"Enter the record of the student"<<"\n";
    cout<<"------------------------------"<<"\n";
    Student s;
    cout<<"Enter Name of the Student: ";
    cin>>s.name;
    cout<<"Enter Student ID: ";
    cin>>s.ID;

    cout<<endl<<"Displaying the record of the student, you have entered so far\n";
    cout<<"Student Name: "<<s.name <<"\n";
    cout<<"Student ID: "<<s.ID<<"\n";

    getch();
    return 0;
}
```

**输出：**

```text
Enter the record of the student
-------------------------------
Enter Name of the Student: Student123
Enter Student ID: 1256

Displaying the record of the student, you have entered so far
Student Name: Student123
Student ID: 1256
```

### Q2. 编写一个程序，使用结构体显示矩形的面积，其尺寸在运行时提供。

答：

```cpp
#include <iostream.h>

struct rectangle
{
    float length;
    float breadth;
};

int main()
{
    rectangle r1;
    cout<<"Enter the length of the rectangle: ";
    cin>>r1.length;
    cout<<"Enter the breadth of the rectangle: ";
    cin>>r1.breadth;
    cout<<"Area of the rectangle: " ;
    cout<<(r1.length * r1.breadth);
    return 0;
}
```

