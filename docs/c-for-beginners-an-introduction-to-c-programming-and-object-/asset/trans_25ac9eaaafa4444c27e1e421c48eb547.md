

### 构造函数定义：

```cpp
Car :: Car ( int displacement )
{
    cout << endl << endl
         << "Object Created! Setting Displacement as"
         << displacement ;
    Displacement = displacement ;
    cout << endl << endl
         << "Displacement Set: " << Displacement ;
}
```

### 主函数中的对象创建

```cpp
Car c1 (1000), c2 (2000), c3 (3000);
```

如您所见，1000、2000、3000 作为参数传递给构造函数。

### 输出

![](img/cda5b023e23ffd0b87fc37b1da33973d_139_0.png)

类可以有多个构造函数，这得益于构造函数重载机制。当创建对象时，程序会根据参数寻找匹配的构造函数。如果找不到匹配项，编译器将返回错误，程序将无法编译。例如，在上述代码中，只定义了一个构造函数，它只接受一个整数参数。在创建对象时，如果您简单地声明对象而不传递任何参数，比如 – *Car c1, c2, c3;*，程序将寻找一个接受*无参数*的构造函数，该构造函数在我们的代码中显然不存在，因此编译器将返回错误。为避免此问题，最好始终提供一个不接受任何参数和/或不执行任何操作的构造函数。这样的构造函数称为*默认构造函数*或*无操作构造函数*。

## 14.2 构造函数重载

构造函数重载的工作原理与函数重载相同；也就是说，一个类可以有多个具有不同定义的构造函数。构造函数可以基于参数的数量和参数的类型进行重载。函数重载已在 *第9.4节* 中详细讨论过，因此无需单独再讲构造函数重载。不过，我们将看一个示例，在该示例中，我们将回顾 *Car 类*，并为其定义3个不同的构造函数。这三个不同的定义将分别用于处理无参数、1个参数和3个参数的情况。无参数的构造函数是一个*默认构造函数*，在此例中它不做任何重要的事情；带一个参数的构造函数仅设置 *Displacement*；带3个参数的构造函数设置 *Manufacturer、Model 和 Displacement*。

构造函数原型如下：

```cpp
Car ( ); //无参数
Car ( int ); //1个参数
Car ( const char *, const char *, int ); //3个参数
```

### 这是C++程序：

```cpp
#include <iostream>
#include <cstring> //strcpy所需

using namespace std;

//类定义
class Car
{
    //私有数据成员
    char Manufacturer[ ], Model[ ];
    int Displacement;

public:
    static int count;
    //公有成员函数
    void setData ( const char *, const char *, int);
    void displayData ();

    Car ( ); //无参数
    Car ( int ); //1个参数
    Car ( const char *, const char *, int ); //3个参数
};

//构造函数定义 - 无参数 - 默认
Car :: Car ( )
{
    cout << endl
         << "Default Constructor invoked! ";
}

//构造函数定义 - 1个参数
Car :: Car ( int displacement )
{
    <<
    << endl;
Car c2 (     );

cout << endl << endl
     <<       ;

Car c3 (     ,      ,      );

cout << endl << endl ;
return 0;
}
```

### 输出

![](img/cda5b023e23ffd0b87fc37b1da33973d_143_0.png)

从代码和输出可以看出，创建了3个具有不同参数数量的对象，相应的构造函数被正确调用。

## 14.3 析构函数

构造函数在创建对象时被调用，而析构函数在删除对象时被调用。通常在

```cpp
cout << endl <<
    ;
}

Test :: ~Test ()
{
    cout <<
        << endl;
}

main ()
{
    cout << endl <<
        << "...";

    Test t1, t2;
    cout << endl << endl <<
        << endl <<
        << endl <<
        << endl << endl;
    return 0;
}
```

### 输出

![](img/cda5b023e23ffd0b87fc37b1da33973d_145_0.png)

## 15. 继承

继承是面向对象编程中的一个概念，它允许我们通过继承现有类的属性来派生一个新类。属性可以包括数据成员和成员函数。现有类称为*基类*，新类称为*派生类*。这个过程促进了代码的可重用性。我们无需重新编写一个新类，可以使用现有类的属性，只编写需要的额外属性。

考虑一个名为 *Person* 的类，具有公有数据成员 – *FirstName、LastName 和 City*。该类的声明如下：

```cpp
class Person
{
    public:
        char FirstName[20], LastName[20], City[20];
};
```

看起来像这样：

![](img/cda5b023e23ffd0b87fc37b1da33973d_147_0.png)

假设我们想要声明另一个名为 Student 的类，其数据成员为 – *FirstName、LastName、City、School 和 Grade.*

该类的声明如下：

```cpp
class Student
{
    public:
    char FirstName[20], LastName[20], City[20], School[20];
    int Grade;
};
```

Student类看起来像这样：

![](img/cda5b023e23ffd0b87fc37b1da33973d_148_0.png)

从图示和代码片段可以看出，数据成员 *FirstName、LastName 和 City* 在 *Person 类* 和 *Student 类* 中都是共同的。使用继承，我们可以从 *Person 类* 派生 *Student 类*，其中 *Student 类* 将获得 *Person 类* 中存在的自己的数据成员集 – *FirstName、LastName、City*，而我们只需在 *Student 类* 中声明两个数据成员 – *School 和 Grade*。继承的一般语法是：

```
class <派生类名> : <访问类型> <基类名>
{
    //类定义
};
```

只有类的公有和受保护成员可以被继承到另一个类中；私有成员不能被继承。

*访问类型*可以是 *公有、私有或受保护*。如果访问类型是：

- *公有：*
  - 基类的公有类成员被继承并在派生类中变为公有。
  - 基类的受保护类成员被继承并在派生类中变为受保护。
- *受保护：*
  - 基类的公有和受保护类成员被继承并在派生类中变为受保护。
- *私有：*
  - 基类的公有和受保护类成员被继承并在派生类中变为私有。

让我们从 Person 类派生 Student 类：

```cpp
class Student : public Person
{
    public:

    char School [20];

    int Grade;
};
```

从上述代码片段可以看出，使用了 *公有* 继承，因此 *Person 类* 的公有成员将被继承到 *Student 类* 中。Student 类现在拥有 *FirstName、LastName、City、School 和 Grade*。此过程在内部将与下图所示的类似：

![](img/cda5b023e23ffd0b87fc37b1da33973d_151_0.png)

让我们在 *Student* 类中编写两个函数 *setData* 和 *displayData*，并在 main 函数中创建该类的对象来演示这一概念。以下是完整的 C++ 程序：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

//创建类Person
class Person
{
public:
    char FirstName[20], LastName[20], City[20];
};

//从Person类创建Student类
class Student : public Person
{
private:
    char School[20];
    int Grade;
    void setData(const char *, const char *, const char *, const char *, int);
    void displayData();
};

//setData的函数定义
void Student :: setData (const char *firstname,
const char *lastname, const char *city, const char
*school, int grade)
{
    strcpy(FirstName, firstname);
    strcpy(LastName, lastname);
    strcpy(City, city);
    strcpy(School, school);
    Grade = grade;
}

void Student :: displayData ()
{
    cout << endl << endl;
```

