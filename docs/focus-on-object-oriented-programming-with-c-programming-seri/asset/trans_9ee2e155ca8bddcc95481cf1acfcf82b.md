

```cpp
#include <iostream>
#define FLOORS 10

using namespace std;

struct elevator {
    int floorSelected;
    int floorNumber;
    void initialize();
    void selectFloor(int floor);
    void go();
};

void elevator::initialize() {
    floorSelected = 0;
    floorNumber = 0;
}

void elevator::selectFloor(int floor) {
    if (floor < 0 || floor >= FLOORS)
        return;
    floorSelected = floor;
}

void elevator::go() {
    if (floorNumber < floorSelected)
        while (++floorNumber < floorSelected)
            cout << "floor: " << floorNumber << " going up!" << endl;
    else if (floorNumber > floorSelected)
        while (--floorNumber > floorSelected)
            cout << "floor: " << floorNumber << " going down!" << endl;
    cout << "floor: " << floorNumber << " stopping." << endl;
}

int main() {
    elevator A;
    A.initialize();
    A.selectFloor(7);
    A.go();
}
```

```cpp
// elevator.c

#include <stdio.h>
#define FLOORS 10

typedef struct elev {
    int floorSelected;
    int floorNumber;
} elevator;

/* Functions to work with elevator variables. We have no choice but to
use pointers. */

void initialize(elevator * E) {
    E->floorSelected = 0;
    E->floorNumber = 0;
}

void selectFloor(elevator * E, int floor) {
    if (floor < 0 || floor >= FLOORS)
        return;

    E->floorSelected = floor;
}

void go(elevator * E) {
    if (E->floorNumber < E->floorSelected)
        while (++E->floorNumber < E->floorSelected)
            printf("floor: %d; going up!\n", E->floorNumber);
    else if (E->floorNumber > E->floorSelected)
        while (--E->floorNumber > E->floorSelected)
            printf("floor: %d; going down!\n", E->floorNumber);
    printf("floor: %d; stopping.\n", E->floorNumber);
}

int main() {
    elevator A,B;

    initialize(&B);        /* User forced to work with addresses */
    select(&B, 7);         /* and pointers.                    */
    A.floorNumber = 8;     /* User chooses to access elements  */
    A.floorSelected = 1;   /* directly, inviting errors        */
    go(&A);
    go(&B);
}
```

```cpp
// array1.cpp
// note: this program will compile, but it won't link without the
// set() definition

#include <iostream>
#define SIZE 10

using namespace std;

struct intArray {
public:
    int a[SIZE];
    void set(int index, int value);
    void print();
};

void intArray::print() {
    for(int i = 0; i < SIZE; i++)
        cout << "a[" << i << "] = " << a[i] << endl;
}

int main() {
    intArray num;
    for(int i = 0; i < SIZE; i++)
        num.set(i,i);
    num.print();
}
```

```cpp
// farray1.cpp - friend function
// note: this program will compile, but it won't link without
// the set() definition
#include <iostream>
#define SIZE 10
using namespace std;
struct intArray {
    private:
        int a[SIZE];
    public:
        void set(int index, int value);
        friend void print(intArray);
    };
void print(intArray x) {
    for(int i = 0; i < SIZE; i++)
        cout << "a[" << i << "] = " << x.a[i] << endl;
}
int main() {
    intArray num;
    for(int i = 0; i < SIZE; i++)
        num.set(i,i);
    print(num);
}
```

```cpp
// employee.cpp - entire structs can be friends
struct employee {
    private:
        int salary;
        int benefitLevel;
    public:
        void initialize(int startingPay);
        void raise(float percent);
        friend struct accountant;
};
int main() {
}
```

## 第 4 章 类

- C++ 类
- 预处理器命令
- 距离对象
- 类实验室（扑克）

## C 结构体

传统的 C 编程技术往往会让程序员比必要的工作更努力。例如，考虑你如何表示日期和时间，这是大多数程序都需要完成的典型任务。

在 C 中，你可以像这样声明一个结构体：

```cpp
struct Time {
    int month;
    int day;
    int year;
    int hour;
    int min;
    int sec;
};
```

Time 结构体的成员存储单个日期和时间的分量值。

有了这个结构体，你可以声明一个 Time 变量，例如：

```cpp
struct Time appt;
```

你可以使用诸如下面的语句为 appt 的成员赋值：

```cpp
appt.month = 9;
appt.day = 23;
appt.year = 2012;
appt.hour = 8;
appt.min = 30;
appt.sec = 0;
```

## 使用 C 结构体

使用大量 `Time` 结构体的程序可能需要以下函数：

- 显示时间和日期
- 更新结构体成员
- 比较两个日期

在 C 中，你可以编写这样的显示函数：

```cpp
void display(struct Time *tp) {
    printf("Date: %02d / %02d / %04d\n", tp->month, tp->day, tp->year);
    printf("Time: %02d : %02d : %02d\n", tp->hour, tp->min, tp->sec);
}
```

要显示日期和时间，语句可以将 `Time` 结构体的地址传递给 `display()`，例如：

```cpp
display(&appt);
```

到目前为止，一切顺利！！

## C 结构体的问题

考虑一下代码中可能出现的一些问题。

在设计了类似 `Time` 的 `struct` 并编写了大量 `date()` 和 `time()` 函数后，你发现了一种存储日期和时间的更优方法，这将大大提高程序的运行时间（无论是更快的执行时间还是更好的内存利用率）。

例如，你可以使用一个 `long int`，表示从固定日期开始的秒数。此更改还使得可以使用识别以这种方式存储的日期和时间的日期和时间库函数。

真遗憾你没有更早想到这个绝妙主意！要在此时更改程序的表示方式，你必须：

- 修改 `Time` 结构体，删除当前成员并添加一个新的 `long int` 数据成员……或者你可能干脆决定不使用 `struct`。
- 修改所有声明 Time 参数或返回 Time 结构体或指针的函数，例如 display()。
- 查找并修改在 Time 结构体中分配或使用分量值的语句。这些语句必须修改为使用新的日期和时间格式。

在拥有数千行代码的大型程序中，追踪每一个 Time 的使用情况的前景令人沮丧。对数据结构的更改迫使你修改已经过测试的代码，从而需要新的调试会议并浪费宝贵的开发时间。

经验法则是：“让数据结构决定代码”。

然而，在现实世界中，数据规范在程序开发过程中很可能会发生变化，给程序员带来额外工作。使用传统编程时，你在程序开发早期选择的数据表示方式会限制你日后做出更改的自由。

我们将看到，使用面向对象编程时，数据可能会改变，但对代码的影响有限。C++ 类可以限制程序对内部数据存储细节的访问。因此，对数据表示的更改不一定会影响该信息的每个使用位置。

## C++ 类

C++ 类是一种将数据和函数封装在方便包中的结构。下面我们将 C 的 Time 结构体重写为 C++ 类，并封装数据和函数：

```cpp
// time1.cpp

#include <iostream>

using namespace std;

class Time1 {
  public:
    int month;
    int day;
    int year;
    int hour;
    int min;
    int sec;
    void display();
};

void Time1::display() {
  cout << (month < 10 ? "0" : "") << month << "/"
       << (day < 10 ? "0" : "") << day << "/"
       << year << " ";

  cout << (hour == 0 || hour == 12 ? 12 : hour % 12) << ":"
       << (min < 10 ? "0" : "") << min << ":"
       << (sec < 10 ? "0" : "") << sec
       << (hour < 12 ? " AM" : " PM") << endl;
}

int main() {
  Time1 appt;

  appt.month = 9;
  appt.day = 23;
  appt.year = 2012;
  appt.hour = 8;
  appt.min = 30;
  appt.sec = 0;

  cout << "Appointment = ";
  appt.display();
}
```

这个类与 Time 结构体非常相似，只是以 class 关键字开头。

## C++ 类与 C 结构体

请记住，C++ 类和 C 结构体有很多共同点。事实上，C 结构体支持的所有功能都由 C++ 类支持：

- 类对象可以传递给函数
- 类对象可以由函数返回
- 可以使用指针访问类对象
- 类可以用作数组类型
- 类可以嵌套
- 可以为类对象动态分配内存

但请记住，类比 C 结构体强大得多：

- 类通过 public、private、protected 和 friend 声明提供信息隐藏功能
- 类可以将函数作为成员
- 类使用称为构造函数和析构函数的特殊功能来初始化和清理对象
- 类使用派生类和虚函数来支持继承

## 类数据成员

类中的数据成员与 C 结构体中的数据成员完全相同。它们可以是：

- 变量
- 指针
- 引用
- 数组
- 结构体
- 类对象

但是，类数据成员不能使用存储类说明符：

- auto
- extern
- register

