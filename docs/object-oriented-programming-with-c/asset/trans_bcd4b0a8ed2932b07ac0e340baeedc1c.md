
请注意，每个静态成员变量的类型和作用域都必须在类定义外部定义。这是必要的，因为静态数据成员是单独存储的，而不是作为对象的一部分。由于它们与类本身相关联，而不是与任何类对象相关联，因此它们也被称为类变量。

静态变量 count 在创建对象时被初始化为零。每当数据读入对象时，count 就会递增。由于数据被读入对象三次，变量 count 被递增三次。因为所有三个对象共享唯一的 count 副本，所以三条输出语句都会显示值 3。图5.4显示了对象如何使用静态变量。

**图5.4** *静态数据成员的共享*

静态变量与非内联成员函数类似：它们在类声明中声明，并在源文件中定义。在定义静态变量时，也可以为该变量赋予初始值。例如，下面的定义将 count 的初始值设为 10。

```
int item :: count = 10;
```

## 5.12 静态成员函数

与静态成员变量一样，我们也可以有静态成员函数。声明为 static 的成员函数具有以下性质：

- 静态函数只能访问同一类中声明的其他静态成员（函数或变量）。
- 可以使用类名（而不是对象）来调用静态成员函数，如下所示：

```
class-name :: function-name;
```

程序5.5演示了这些特性的实现。静态函数 show-count() 显示到该时刻为止已创建的对象数量。创建的对象数量由静态变量 count 维护。

函数 showcode() 显示每个对象的代码编号。

## 程序5.5 静态成员函数

```cpp
#include <iostream.h>
using namespace std;
class test
{
int code;
static int count;  // static member variable
public:
void setcode(void)
{
code = ++count;
```

```
void showcode(void)
{
    cout << “object number: “ << code << “\n”;
}
static void showcount(void)  // static member function
{
    cout << “count: “ << count << “\n”;
}
};
int test :: count;
int main()
{
    test t1, t2;

    t1.setcode();
    t2.setcode();
    test :: showcount();  // accessing static function

    test t3;
    t3.setcode();

    test :: showcount();

    t1.showcode();
    t2.showcode();
    t3.showcode();

    return 0;
}
```

程序5.5的输出将是：

```
count: 2
count: 3
object number: 1
```

标识符 employee 是一种用户自定义数据类型，可以用来创建与不同员工类别相关的对象。示例：

```
employee manager[3];  // array of manager
employee foreman[15]; // array of foreman
employee worker[75];  // array of worker
```

数组 manager 包含三个 employee 类类型的对象（经理），即 manager[0]、manager[1] 和 manager[2]。类似地，foreman 数组包含 15 个对象（领班），worker 数组包含 75 个对象（工人）。

由于对象数组的行为与其他任何数组一样，我们可以使用通常的数组访问方法来访问各个元素，然后使用点成员运算符来访问成员函数。例如，语句

```
manager[i].putdata();
```

将显示数组 manager 中第 i 个元素的数据。也就是说，该语句请求对象 manager[i] 调用成员函数 putdata()。

对象数组在内存中的存储方式与多维数组相同。数组 manager 如图5.5所示。请注意，只为对象的数据项创建空间；成员函数单独存储，供所有对象使用。

## 图5.5 对象数组数据项的存储

程序5.6演示了对象数组的用法。

```cpp
#include <iostream.h>
using namespace std;
class employee
{
char name[30]; // string as class member
float age;
public:
void getdata(void);
void putdata(void);
};
void employee :: getdata(void)
{
cout << "Enter name: ";
cin << name;
cout << "Enter age: ";
cin >> age;
}
```

```
void employee :: putdata(void)
{
    cout << “Name: “ << name << “\n”;
    cout << “Age: “ << age << “\n”;
}
const int size = 3;
int main()
{
    employee manager[size];
    for(int i = 0; i<size; i++)
    {
        cout << “\nDetails of manager” << i+1 << “\n”;
        manager[i].getdata();
    }
    cout << “\n”;
    for(i = 0; i<size; i++)
    {
        cout << “\nManager” << i+1 << “\n”;
        manager[i]. putdata();
    }
    return 0;
}
```

由于这是一个交互式程序，输入数据和程序输出如下所示：

```
Interactive input
Details of manager1
Enter name: xxx
Enter age: 45

Details of manager2
name: yyy
Enter age: 37

Details of manager3
```

与任何其他数据类型一样，对象可以用作函数参数。这可以通过两种方式完成：

- 将整个对象的副本传递给函数。
- 只将对象的地址传递给函数。

第一种方法称为按值传递。由于传递给函数的是对象的副本，因此函数内部对对象所做的任何更改都不会影响调用函数时所用的对象。第二种方法称为按引用传递。当传递对象的地址时，被调用函数直接作用于调用中使用的实际对象。这意味着函数内部对对象所做的更改将反映在实际对象上。按引用传递方法更高效，因为它只需要传递对象的地址，而不需要传递整个对象。

程序5.7演示了对象作为函数参数的用法。它以小时和分钟的格式执行时间加法。

## 程序5.7 对象作为参数

```cpp
#include <iostream.h>
using namespace std;
class time
{
int hours;
int minutes;
public:
void gettime(int h, int m)
{ hours = h; minutes = m; }
void puttime(void)
{
    cout << hours << “ hours and “;
    cout << minutes << “ minutes “ << “\n”;
}
void sum(time, time);  // declaration with objects as arguments
};
void time :: sum(time t1, time t2) // t1, t2 are objects
{
minutes = t1.minutes + t2.minutes;
hours = minutes/60;
minutes = minutes%60;
hours = hours + t1.hours + t2.hours;
}
int main()
{
time T1, T2, T3;

T1.gettime(2,45);  // get T1
T2.gettime(3,30);  // get T2
```

```
T3.sum(T1,T2); // T3 = T1+T2

cout << “T1 = “; T1.puttime(); // display T1
cout << “T2 = “; T2.puttime(); // display T2
cout << “T3 = “; T3.puttime(); // display T3
return 0;
}
```

程序5.7的输出将是：

+   T1 = 2小时45分钟
+   T2 = 3小时30分钟
+   T3 = 6小时15分钟

> **注意：** 由于成员函数 sum() 由对象 T3 调用，并以对象 T1 和 T2 作为参数，因此它可以直接访问 T3 的 hours 和 minutes 变量。但是，T1 和 T2 的成员只能通过点运算符（如 T1.hours 和 T1.minutes）访问。因此，在函数 sum() 内部，变量 hours 和 minutes 引用 T3，T1.hours 和 T1.minutes 引用 T1，T2.hours 和 T2.minutes 引用 T2。

**图5.6** *在被调用函数内访问对象成员*

对象也可以作为参数传递给非成员函数。但是，这类函数只能通过作为参数传递给它的对象来访问公有成员函数，而不能访问私有数据成员。
