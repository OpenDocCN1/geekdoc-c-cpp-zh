
`cout << "d3 = " << d3.showDist();`

`return 0;`

`}`

```
注意这一行：
```

```
d3 = 10.0 + d1;
```

产生了一个编译错误。为什么呢？

在这个程序中，`+`运算符被重载为用于相两个`Distance`类型的对象。这里还有一个单参数构造函数，它可以将`float`类型的值（代表英尺或英尺的小数部分）转换为`Distance`值。也就是说，将10.25英尺转换为10英尺3英寸。当存在这样的构造函数时，你可以在`main()`中编写如下语句：

```
d3 = d1 + 10.0;
```

重载的`+`运算符在左右两侧都在寻找`Distance`类型的对象。但如果右侧的参数类型是`float`，编译器将使用该单参数构造函数将`float`转换为`Distance`值，然后执行加法。

但为什么这行不通呢？

```
d3 = 10.0 + d1;
```

因为重载的`+`运算符所所属的对象必须是运算符左侧的变量。当我们把不同类型的变量或常量放在左侧时，没有对象可以作为该重载`+`运算符的成员，因此没有构造函数可以将`float`类型转换为`Distance`。编译器简单地无法处理这种情况。

友元函数允许我们编写运算符左侧为非成员数据类型的语句。因此我们可以将`Distance`类内部的声明更改为：

```cpp
friend Distance operator+(Distance, Distance);
```

我们现在按照如下重定义`operator+()`函数：

```cpp
Distance operator+(Distance d1, Distance d2) {
int ft = d1.feet + d2.feet;
float in = d1.inches + d2.inches;
if (in >= 12.0) {
  in -= 12.0;
  ++ft;
}
return Distance(ft, in);
}
```

现在我们可以在`main()`内部编写以下内容而不会出现编译错误信息：

```
d3 = d1 + 10.0;
d3 = 10.0 + d1;
```

注意，重载的`+`运算符作为成员函数时接受一个参数，但作为友元函数时接受两个参数。在成员函数中，它操作的对象是它所属的对象，第二个是参数。在友元函数中，两个对象都必须是参数。

友元函数允许一元运算符接受一个参数，二元运算符接受两个参数，而成员函数一元运算符有零个参数，二元运算符有一个参数。这是因为成员函数已经自动处理了一个变量，即它被调用的对象。

### 使用 + 运算符拼接字符串

考虑以下`String`类：

```cpp
const int SIZE = 100;
#include <iostream>
#include <string.h>
using namespace std;
class String {
private:
    char buf[SIZE];
public:
    String() { buf[0] = '\0'; }
    String(const char s[]) { strcpy(buf, s); }
    void display() { cout << buf; }
    String operator+(String s);
};
String String::operator+(String s) {
    if (strlen(buf) + strlen(s.buf) < SIZE) {
        strcat(buf, s.buf);
        return *this;
    } else
        return String();
    }
}
int main() {
    String s1 = "Hello ";
    String s2 = "World!";
    String s3 = s1 + s2;
    s3.display();
    return 0;
}
```

输出：
Hello World!

```cpp
int main() {
    Distance d1, d2;
    cout << "Enter Distance values: ";
    cin >> d1 >> d2;
    cout << "d1 = " << d1 << endl;
    cout << "d2 = " << d2 << endl;
    Distance d3(11, 25);
    cout << "d3 = " << d3 << endl;
    return 0;
}
```

该程序向用户请求两个距离值，然后打印这些值以及程序中初始化的另一个值。请注意，输入和输出运算符分别作为左操作数以引的形式传递给`istream`和`ostream`对象，这允许连续的输入或输出运算符进行级联。例如：

```cpp
cout << "d1 = " << d1 << "d2 = " << d2;
```

在这里，每个括号内的子表达式都将流对象作为最外表达式返回。由于`istream`的设计，输入或输出运算符必须是友函数（friend functions），并以用户定义的类型作为参数以及相同的流对象作为返回值，你可以拥有如下形式的表达式：

```cpp
cout << d1;
```

为什么我们不能将重载运算符定义为`Distance`的成员函数呢？如果这样做，对程序员和程序的读者来说将非常困惑，因为输出运算符的成员函数只声明了一个`ostream`对象。因此，使用友函数会更好。

### 更新后的 Distance 类

```cpp
// dist4.h
#ifndef DIST4
#define DIST4
#include <iostream>
using namespace std;
class Distance {
private:
    int feet;
    float inches;
    void normalize();
public:
    Distance();
    Distance(float f);
    Distance(int ft, float in);
    Distance& operator+=(const Distance& d);
    friend Distance operator+(const Distance& d1, const Distance& d2);
    friend Distance& operator>>(istream& is, Distance& d);
    friend ostream& operator<<(ostream& os, const Distance& d);
};
#endif
```

```cpp
// dist4.cpp
#include <iostream>
#include "dist4.h"
Distance::Distance() {
    feet = 0;
    inches = 0;
}
Distance::Distance(float f) {
    feet = (int)f;
    inches = (f - (int)f) * 100;
}
Distance::Distance(int ft, float in) {
    feet = ft;
    inches = in;
    normalize();
}
void Distance::normalize() {
    while (inches >= 1200) {
        inches -= 1200;
        feet++;
    }
}
Distance& Distance::operator+=(const Distance& d) {
    feet += d.feet;
    inches += d.inches;
    return *this;
}
Distance operator+(const Distance& d1, const Distance& d2) {
    int ft = d1.feet + d2.feet;
    float in = d1.inches + d2.inches;
    return Distance(ft, in);
}
istream& operator>>(istream& is, Distance& d) {
    cout << "Enter feet: ";
    is >> d.feet;
    cout << "Enter inches: ";
    is >> d.inches;
    d.normalize();
    return is;
}
ostream& operator<<(ostream& os, const Distance& d) {
    os << d.feet << "' " << d.inches / 100.0 << "'";
    return os;
}
```

```cpp
// distrv4.cpp
#include <iostream>
#include "dist4.h"
using namespace std;
int main() {
    Distance d1(5, 22), d2(8.25), d3, d4, d5;
    cout << "d1: " << d1 << endl;
    cout << "d2: " << d2 << endl;
    cout << "d3: " << d3 << endl;
    cout << "d4: " << d4 << endl;
    cout << "d5: " << d5 << endl;
    d3 = d1 + d2;
    cout << "d3 = " << d3 << endl;
    d4 = d3 + 10;
    cout << "d4 = " << d4 << endl;
}
```

*(注：由于你提供的文本在后面出现了重复且截断的内容，上述翻译仅针对第一部分完整的逻辑内容)*

```cpp
class PhoneBook {
private:
    int length;
    int count;
    ENTRY *listing;
public:
    PhoneBook(int);
    ~PhoneBook();
    void addEntry(char*, long);
    void displayPhoneBook();
    long operator[](char *); 
    char *operator[](long);
};
#endif
```
// phone.cpp
```cpp
#include <iostream>
#include <iomanip>
#include <string>
#include "phone.h"
```
using namespace std;
```cpp
PhoneBook::PhoneBook(int size) { // 创建指定大小的电话簿
    listing = new ENTRY[size]; 
    length = size;
    count = 0;
}
```
```cpp
PhoneBook::~PhoneBook() {
    for (int i = 0; i < count; i++)
        delete listing[i].name;
    delete []listing;
}
```
```cpp
void PhoneBook::displayPhoneBook() {
    for (int i = 0; i < count; i++)
        cout << setw(10) << listing[i].name;
        cout << setw(10) << listing[i].number << endl;
}
```
```cpp
void PhoneBook::addEntry(char *Name, long Number) {
    listing[count].name = new char[strlen(Name) + 1];
    strcpy(listing[count].name, Name);
    listing[count++].number = Number;
}
```

专注于 C++ 面向对象编程

第 265 页

```cpp
long PhoneBook::operator[](char *Name) { // 查找人员号码
for (int i = 0; i < count; i++)
    if (strcmp(listing[i].name, Name) == 0)
        return (listing[i].number);
return 0;
}
char *PhoneBook::operator[](long Number) { // 根据号码查找姓名
for (int i = 0; i < count; i++)
    if (listing[i].number == Number)
        return (listing[i].name);
return "Person not found.";
}
```
// phonebook.cpp
```cpp
#include <iostream>
#include "phone.h"
```
using namespace std;
```cpp
int main() {
    PhoneBook pb(100);
    long number;
    char *name;
    pb.addEntry("Haley", 486114);
    pb.addEntry("Shari", 493368);
    pb.addEntry("Samantha", 486199);
    cout << "Display phone book:" << endl;
    pb.displayPhoneBook();
    cout << endl;
    number = pb["Shari"];
    cout << "number = " << number << endl;
    name = pb[486199];
    cout << "name = " << name << endl;
    return 0;
}
```

### 运算符重载作业

1. 二元运算符和函数之间的区别是什么？
2. 在重载运算符时，给出选择**成员**函数或友函数的原因。
3. 当重载**输入**和**输出**运算符以处理用户定义的类时，这些运算符通常是成员函数还是友函数？
4. 使用运算符重载来改变整数的行为可能吗？为什么或为什么可能？
5. 哪些运算符不能被重载？
6. 重载以下运算符 `=`、`()`、`[]` 有哪些限制？
7. 为什么我们不能将 `<<` 作为成员运算符？
8. 下面的函数重载了 `+` 运算符并添加两个 Distance 对象。假设 Distance 类包含两个私有数据成员：

```cpp
int feet;
float inches;
```

根据下面的函数，尽可能回答以下问题：

```cpp
Distance operator+(const Distance &a, const Distance &b) {
  Distance sum;
  sum.feet = a.feet + b.feet;
  sum.inches = a.inches + b.inches;
  if (sum.inches >= 12.0) {
    sum.inches -= 12.0;
    sum.feet++;
  }
  return sum;
}
```

- a) 这个函数可能是成员函数、友函数还是普通函数？如何判断？
- b) 参数声明中的 `&` 符号 `a` 和 `b` 意味着什么？
- c) 如果没有 `&`，该函数还能正常工作吗？如果没有，为什么？如果有，为什么？
- d) 返回类型中的 `Distance &` 有什么影响？

运算符重载实验

C 中的构造是高效的，但对于初学者来说是危险的。例如，新手会陷入声明一个 100 元素的数组并尝试访问索引 100 的陷阱。在 C 中这是一个错误，但语言不会警告用户。C++ 允许程序员牺牲一些效率来定义更安全、更灵活的数组构造。实验的目的是学习如何这样做并获得运算符重载的经验。作业的核心是定义一个 `IntArray` 类。通过它，用户可以声明任何大小的数组，且索引可以是任何正负整数。还可以实现数组之间的赋值、不等性比较、数组相加以及使用 `<<` 输出数组。例如：

```cpp
#include <iostream>
#include "IntArray.h"
using namespace std;
int main() {
    IntArray a(10), w(10);    // 10 个元素，索引从 0 到 9
    IntArray b(-3, 6);      // 10 个元素，索引从 -3 到 6
    IntArray c(6, 8);        // 3 个元素，索引从 6 到 8
    IntArray d(5, 5);        // 单元素数组，索引为 5
    IntArray z;             // 10 个元素，索引从 0 到 9
```
