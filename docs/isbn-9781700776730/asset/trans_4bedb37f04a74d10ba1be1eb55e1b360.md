

## 类成员函数

类成员函数（如 `display()`）被声明为函数原型。实际的函数语句在程序的另一个地方提供。

让我们来看成员函数 `display()` 的实现：

```cpp
void Time::display() {
  cout << (month < 10 ? "0" : "") << month << "/\n"  << (day < 10 ? "0" : "") << day << "/\n"  << year << ":";
  cout << (hour == 0 ? 12 : hour % 12) << ":"
  << (min < 10 ? "0" : "") << min << ":"
  << (sec < 10 ? "0" : "") << sec
  << (hour < 12 ? "AM" : "PM") << endl;
}
```

成员函数的实现与普通函数的实现之间有两个主要区别：

- 成员函数名以类名和作用域解析运算符（::）作为前缀。这告诉编译器 `display()` 是 `Time` 类的成员。由于类名唯一地限定了成员函数的名称，程序可以拥有其他名为 `display()` 的函数或其他类成员函数而不会发生冲突。
- 在成员函数内部，语句可以直接访问类的成员，而不需要指针或传递参数。

## Time 类的 main() 函数

```cpp
int main() {
    Time appt;

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

`main()` 程序使用 `Time` 类的方式就像使用任何其他数据类型一样。

- 它将 `appt` 声明为 `Time` 类型的对象。`Time` 类是一个模板，描述了类成员的格式。你必须创建一个 `Time` 类型的对象（如 `appt`）才能使用该类。
- 它为 `appt` 的数据成员赋值，初始化了一个日期和时间。

注意，我们使用点符号表示法来引用类对象的公共数据成员，这就像你引用结构体变量的成员一样。当此类成员是一个函数时，C++ 会调用该函数，该函数会对类对象的数据执行某些操作。

## 额外的 Time 对象

注意，程序可能还声明了其他 `Time` 对象：

```cpp
Time today;
Time yesterday;
Time tomorrow;
```

这些对象可以被赋值，然后通过以下语句显示：

```cpp
today.display();
tomorrow.display();
yesterday.display();
```

然而，我们的程序并没有做任何防止前面提到的数据表示问题的措施。`Time` 类中的所有数据成员都是公共的，因此可以被程序中的其他语句直接访问。对 `Time` 类数据成员的更改需要修改所有此类语句。

C++ 类与 C++ 结构体（struct）相同，只有一个关键区别：

- `struct` 默认是公共的（public），因此其中的所有数据对程序员都是可用的
- `class` 默认是私有的（private），因此使用类是在 C++ 中隐藏数据的另一种方法。

类是 C++ 中一个重要的概念；如此重要以至于当 Bjarne Stroustrup 创建 C++ 语言时，他称其为“带类的 C”。又过了 3 年，它才被称为 C++！

## Time2 类

我们可以通过在 `Time1` 类中声明一个新的改进后的 `Time2` 类来解决这个问题，该类使用成员函数来访问类对象的数据成员：

```cpp
// time2.cpp

#include <iostream>

using namespace std;

class Time2 {
private:
    int month;
    int day;
    int year;
    int hour;
    int min;
    int sec;
public:
    void display();
    void setTime(int m, int d, int y, int h, int mn, int s);
    void getTime(int& m, int& d, int& y, int& h, int& mn, int s);
};

void Time2::display() {
    cout << (month < 10 ? "0" : "") << month << "/"
         << (day < 10 ? "0" : "") << day << "/"
         << year << " ";
    cout << ((hour == 0 || hour == 12) ? 12 : hour % 12) << ":"
         << (min < 10 ? "0" : "") << min << ":"
         << (sec < 10 ? "0" : "") << sec
         << (hour < 12 ? " AM" : " PM") << endl;
}

void Time2::setTime(int m, int d, int y, int h, int mn, int s) {
    month = m;
    day = d;
    year = y;
    hour = h;
    min = mn;
    sec = s;
}

void Time2::getTime(int& m, int& d, int& y, int& h, int& mn, int s) {
    m = month;
    d = day;
    y = year;
    h = hour;
    mn = min;
    s = sec;
}
```

```cpp
int main() {
  Time2 appt;
  int m, d, y, h, mn, s;

  appt.setTime(7, 23, 2012, 8, 30, 0);
  cout << "Appointment = ";
  appt.display();
  appt.setTime(m, d, y, h, mn, s);
  appt.setTime(m, d, y, ++h, mn, s);
  cout << "Appointment = ";
  appt.display();
}
```

## Time2 类新增

新的 `Time2` 类有 3 个新增：

- 私有（private）访问修饰符使 `int` 类型的数据成员成为类的私有成员。由于这一变化，只有类的成员函数可以直接引用这些数据成员。

> 规则：私有数据成员仅对该类的成员可用。私有成员在类外部是不可见的。

注意：默认情况下，类的成员是私有的。因此，不需要 `private:` 访问修饰符。然而，为了清晰起见，用显访问修饰符标记私有成员是一个好主意。

- `Time2` 的另外两个新增是 `setTime()` 和 `getTime()` 成员函数：

```
setTime() 用于给 appt 类对象赋值
getTime() 将 appt 的数据值复制到局部变量中，并在增加小时后返回给 getTime()。
```

`setTime()` 和 `getTime()` 成员函数通过类名和作用域解析运算符 `::` 告诉编译器这些函数属于 `Time2` 类。在成员函数内部，语句可以直接访问类的成员，而不需要指针或传递参数。`setTime()` 和 `getTime()` 成员函数通过类名和作用域解析运算符 `::` 告诉编译器这些函数属于 `Time2` 类。由于类名唯一地限定了成员函数的名称，程序可以拥有其他名为 `display()` 的函数或其他类成员函数而不会发生冲突。

## 类是否浪费内存？

我们可能留留了这样印象：从类创建的每个对象都包含函数的副本。这可能是一个很好的猜测，因为它强调了对象是完整的实体。

然而，情况并非如此简单。确实每个对象都有自己的数据。但所有对象都使用相同的成员函数，这些函数在定义时只被创建一次。

另一方面，数据项持有不同的值。因此，每个对象都创建了内存空间。

