
4. 每创建一个对象时，默认构造函数都会被调用。

5. 在C++中，构造函数不能被声明为虚函数。

6. 它们没有返回类型。

### 代码：使用构造函数和析构函数

```cpp
#include <iostream>
using namespace std;

class Driver
{
    public:
    Driver()
    {
        std::cout << "\nThis is a constructor of class Driver\n" << endl;
    }
};

int main()
{
    Driver d1;
    return 0;
}
```

**输出：**

```text
This is a constructor of class Driver
```

请注意，对象一创建，类的构造函数就会被调用，因为构造函数可以被重载。现在让我们定义各种类型的构造函数。

### C++中构造函数的类型

C++为我们提供了三种类型的构造函数，每种都略有不同。这些类型如下。

### 1. 默认构造函数

它们不接受任何参数，类的所有对象都使用同一组值进行初始化。它们由编译器提供，并且它们将是0或任何整数值。如果程序员忘记在C++中显式定义构造函数，编译器将隐式地提供默认构造函数。默认构造函数的语法如下：

```cpp
class class_name
{
    class_name()
    { //body
    }
};
```

### 代码：使用默认构造函数

```cpp
#include <iostream>
using namespace std;
class People
{
    public:
    People()
    {
        std::cout << "\nThis is a default constructor \n" << endl;
    }

};
int main() {
    People Object1;


    return 0;
}
```

### 输出：

```text
This is a default constructor
```

### 代码：实现参数化构造函数

```cpp
#include <iostream>
using namespace std;
class People
{
    public:
    int x;

};
int main() {
    People Object1;
    cout << "\nWill be provided with any random value: " << Object1.x << endl;
    // Garbage value would be shown as x is not initialized

    return 0;
}
```

### 输出：

```text
Will be provided with any random value: 9015333
```

### 2. 参数化构造函数

在参数化构造函数中，我们可以向成员函数传递一个或多个参数，以便在创建对象时为对象赋不同的初始化值。请记住，调用这种类型的构造函数时，我们必须按照构造函数原型中定义的参数顺序和类型来传递参数。参数化构造函数的语法如下：

```cpp
class class_name
{
    class_name(argument list..)
    {
        // body
    }
};
```

### 代码：使用参数化构造函数

```cpp
#include <iostream>
using namespace std;
class Student
{
    public:
    Student(string n)
    {
        std::cout << "\nThis is a parameterized constructor" << endl;
        std::cout << "\nName is " << n << endl;
    }
};
int main() {
    Student s1("Mary");
    return 0;
}
```

### 输出：

```text
This is a parameterized constructor
Name is Mary
```

### 3. 拷贝构造函数

拷贝构造函数帮助创建某个类对象的副本。副本会复制所有数据成员的值。拷贝构造函数的语法如下：

```cpp
class Class_name
{
    Class_name(argument list..)
    {
    }
    Class_name(const Class_name& obj)
    {
    }
};
```

### 代码：使用拷贝构造函数

```cpp
#include <iostream>
using namespace std;
class Student
{
public:
    string n;
    /*Student()
    {
        std::cout << "\nThis is a default constructor \n" << endl;
    }*/
    Student(string n)
    {
        std::cout << "\nName is " << n << endl;
    }
    Student(const Student& s1)
    {
        std::cout << "\nThis is a copy constructor\n" << endl;
    }
};
int main() {
    //Student s1;
    Student s1("Rio");
    Student s3(s1);

    return 0;
}
```

### 输出：

```text
Name is Rio
This is a copy constructor
```

### 代码：使用构造函数

```cpp
#include <iostream>
using namespace std;
class Student
```

```cpp
class Average {
    private:
        int num1;
        int num2;
        int r;
    public:
        Average (int num1, int num2) {
            this->num1 = num1;
            this->num2 = num2;
        }
        void AvgResult() {
            cout<<"Average of num1 and num2 = "<<(this->num1+this->num2)/2<<endl;
        }
};

int main () {
    Average object1(22, 33);
    object1.AvgResult();
    return 0;
}
```

### 输出：

```text
Average of num1 and num2 = 27
```

## 5.4 类方法

我们已经讨论了类及其成员，以及特殊的类函数——构造函数。现在，让我们考虑类方法。类函数可以在类定义内部或外部定义。这些函数的调用是通过类的对象使用点运算符或选择运算符来完成的。

### 代码：使用类方法

```cpp
#include <iostream>
using namespace std;
class myclass
{
    public :
    static int num1;
    int y=100,r;
    int sum(int x,int y)
```

- 访问静态数据类型的成员

- 用于继承

C++ 提供了一项特性，可以在类中启用内联函数。编译器每次调用内联函数时，都会将函数体的代码复制过来。这样可以产生更快的结果，因此作为程序员，我们不必一遍遍地编写代码。调用内联函数的语法如下：

```
inline returnType function_Name(Argument List...)
{ // function body
}
```

## 5.5 `static` 关键字

你可能多次听说过 `static`。在物理学中，它通常被定义为静止且不发生运动的状态，但在 C++ 中，`static` 关键字将任何变量、数据成员或函数声明为一种常量类型。这些值不能被修改。它只初始化一次，并且在程序整个生命周期中只使用一份副本。

### `static` 关键字的特性

- 1. 在 C++ 程序中，静态变量只初始化一次。

- 2. 静态变量可以在某个特定函数内定义，也可以在函数外定义。

- 3. 静态变量的作用域限于其使用的块。

- 4. 如果程序员没有为静态变量赋值，则默认值为零。

- 5. 静态变量的生命周期持续到程序终止，之后内存空间被释放。

- 6. 静态函数直接通过类名调用。

静态函数和变量的语法如下：

```cpp
static DataType var = 10;  // gives a static variable
static returnType function() // static function declared
{ // body
}
```

### 代码：使用静态函数和变量

```cpp
#include <iostream>
using namespace std;

class myclass
{
    public :
    static int num1;
    static int assign(int x)
    {
        cout << "\nAssigned value to integer= " << x << endl;
    }
};
int myclass::num1 = 4560;
int main()
{
    myclass obj1;
    myclass::assign(87);
    cout << "\nThe static variable value : " << obj1.num1 << endl;
    return 0;
}
```

### 输出：

```text
Assigned value to integer= 87
The static variable value : 4560
```

## 5.6 C++ 中的内存管理和垃圾回收

C++ 还提供了其他有用的运算符，如 `new` 和 `delete`。这些运算符帮助我们增强根据需要分配或释放内存的灵活性，比 `malloc()`、`calloc()` 和 `free()` 等 C 函数更强大。

内存管理在编程中很重要，因为设备中提供的 RAM 空间是有限的。*垃圾回收* 是一种内存管理技术，可以由垃圾回收器手动或自动完成。我们之前已经做过这类工作：所有全局变量和静态变量只存活到程序结束，之后它们不再有用，内存会被释放。函数内部的局部变量也只在函数调用和返回语句之间“存活”。在 C++ 中，所有这些工作都是自动完成的，并且全部在编译时完成。C++ 还具备在运行时为变量分配内存的能力，这被称为*动态内存分配*。这必须手动完成，不像 Java 或 Python 等其他一些编程语言那样，编译器会自动管理内存分配任务。

### 为什么使用动态内存分配？

- 1. 适用于在运行时才知道特定数据类型大小的情况

- 2. 使一组数据类型更灵活，且可由用户修改

- 3. 更加关注用户输入，结果更具个性化

### `new` 运算符

C++ 中的 `new` 运算符用于动态分配内存。我们请求内存空间，如果存在所需数量的内存，则会分配指定数量的内存并返回一个指向它的指针（如果分配失败，则返回空指针）。可以使用 `sizeof` 来计算其大小。该运算符的语法如下：

```cpp
pointerVar = new dataType;
dataType *pointerVar = new dataType[size];
pointerVar = new dataType[int size];
```

### `delete` 运算符

C++ 中的 `delete` 运算符用于动态释放内存。该地址变为无效，内存现在被不同的数据使用，因此它返回 `void`。如果对象是使用 `new` 运算符分配的，那么只能使用 `delete` 运算符来删除它。该运算符确保安全高效的内存使用。`delete` 运算符的语法如下：

```cpp
delete ptr_var;
```

### 代码：使用 `delete` 运算符

```cpp
#include <iostream>
using namespace std;
int main () {
    int *ptr1 = nullptr;
    ptr1 = new int;
    *ptr1 = 28;
    cout << "\nValue of pointer variable 1 : " << *ptr1 << endl;
    delete ptr1;
    return 0;
}
```

### 输出：

```text
Value of pointer variable 1 : 28
```

## 小结

- *类*是一种用户自定义数据类型，其中方法和数据作为成员组合在一起。

- *构造函数*的主要作用是初始化类，并为所有数据成员构造值。

- 三种类型的构造函数是：默认构造函数、参数化构造函数和拷贝构造函数。

- 析构函数有助于释放未使用对象的内存。

- 构造函数和析构函数都与类同名。

- C++ 中的 `this` 指针存储对象或类实例的地址，使成员函数能够更新相应对象的值。

- 类函数既可以在类定义内部定义，也可以在类定义外部定义。

- 调用类函数是通过类的对象并使用点运算符或选择运算符来完成的。

- 在 C++ 中，`static` 关键字可将任何变量、数据成员或函数声明为一种常量类型。这些值不能被修改。

- `::` 是 C++ 中的作用域解析运算符，其主要作用是访问类的静态成员或为其赋值。

- `new` 和 `delete` 运算符用于 C++ 中的内存分配和释放。

## 练习

### 理论题

- 1. 什么是类？请用示例描述声明类的语法。

- 2. 讨论 C++ 中类的创建和声明？

- 3. 在类主体内部定义的成员函数与在类主体外部定义的成员函数有什么区别？

- 4. 解释传递对象参数的不同方法。

- 5. 使用示例讨论 C++ 中的构造函数和析构函数。

- 6. C++ 中如何动态进行内存分配？

- 7. `static` 关键字在 C++ 中可以以几种方式使用？请使用代码示例讨论这一点。

### 实践题

- 1. 编写一个程序，创建一个名为 `Student` 的类，其中包含一个字符串变量 `name` 和一个整型变量 `roll_no`。通过创建 `Student` 类的对象，将 `roll_no` 的值赋为 2，将 `name` 的值赋为 John。

- 2. 编写一个 C++ 程序，演示类的声明和定义以及类成员的访问。

- 3. 编写一个 C++ 程序，演示类的构造函数的调用。

- 4. 编写一个 C++ 程序，演示类的析构函数的调用。

- 5. 编写一个 C++ 程序，使用类的概念实现一个带菜单的简单计算器。

- 6. 编写一个 C++ 程序，演示 `static` 关键字的使用方式。

- 7. 编写一个 C++ 程序，使用 `static` 关键字统计并显示对象被创建的次数。

- 8. 编写一个 C++ 程序，演示 `new` 和 `delete` 运算符的使用。

- 9. 编写一个 C++ 程序，仅使用指针变量实现一个带菜单的简单计算器。

### 选择题

- 1. 关于类，以下哪个语句是正确的？

  - a. 对象是它所属类的一个实例。

  - b. 类是它所属对象的一个实例。

  - c. 对象是该类的数据类型的一个实例。

  - d. A 和 C 都正确。

- 2. 如果在函数中定义了一个局部类，那么对于该类的对象，下列说法正确的是？

  - a. 该对象可以在该函数中局部地访问、声明和使用。

  - b. 该对象必须在任何其他函数中声明。

  - c. 该对象在函数外部可以临时访问。

  - d. 该对象可以在程序中的任何位置调用该类的所有其他成员。

- 3. 以下哪项指的是将数据及其功能封装到单个独立实体中？

  - a. 模块化

  - b. 抽象

  - c. 封装

  - d. 以上都不是

- 4. 当使用 `struct` 而不是关键字 `class` 时，程序中会发生什么？

  - a. 默认访问权限是公有的

  - b. 默认访问权限是私有的

  - c. 默认访问权限是保护的

  - d. 访问被拒绝

- 5. 以下哪个用于在类外部定义类的成员？

  - a. `:`

  - b. `::`

  - c. `#`

  - d. `!!$`

- 6. C++ 中的类包含什么？

  - a. 数据

  - b. 函数

  - c. 数据和函数

  - d. 数组

- 7. 在类中，数据成员也被称为 ________

  - a. 抽象

  - b. 属性

  - c. 特性

  - d. 维度

- 8. C++ 中的一个类中有多少个访问说明符？

  - a. 2

  - b. 1

  - c. 4

  - d. 3

### 选择题答案

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |

| --- | --- | --- | --- | --- | --- | --- | --- |

| (a) | (a) | (c) | (a) | (b) | (c) | (b) | (d) |

## 参考资料

### 书籍

- B. Stroustrup，*C++ 程序设计语言*（第 4 版）（Addison-Wesley Professional，2013 年）。

- K. R. Venugopal，*精通 C++*（第 2 版）（McGraw Hill Education，2017 年 7 月）。
