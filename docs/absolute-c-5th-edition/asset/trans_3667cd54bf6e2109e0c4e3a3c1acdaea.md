

## 类、指针与动态数组

重载赋值运算符的定义使用 `this` 指针来返回 `=` 符号左侧的对象（即调用者对象）：

```cpp
// 此版本在所有情况下都不起作用。
StringClass::operator=(const StringClass& rtSide) {
    capacity = rtSide.capacity;
    length = rtSide.length;
    delete [] a;
    a = new char[capacity];
    for (int i = 0; i < length; i++)
        a[i] = rtSide.a[i];

    return *this;
}
```

当该版本在运算符的两侧都使用同一个对象进行赋值时，就会出现问题，例如如下所示：

s = s;

当执行这条句赋值时，会执行以下语句：

```
delete [] a;
```

但调用者对象的 `.a` 是 s，这意味着：

```
delete [] s.a;
```

此时指针 `.a` 变为了未定义状态。赋值运算符破坏了对象 `s`，该程序的这次运行被彻底破坏了。

对于许多类，当赋值运算符的两侧是同一个对象时，显而易见的赋值运算符重载定义是无效的。你应该始终检查这种情况，并小心编写重载赋值运算符的定义，使其在在这种情况下也能正常工作。

为了避免我们在赋值运算符的第一个定义中遇到的问题，你可以使用 `this` 指针来测试这种特殊情况，如下：

```cpp
// 修复错误后的最终版本：
StringClass::operator=(const StringClass& rtSide) {
    if (this == &rtSide)
        // 如果右侧与左侧相同
        return *this;
    else {
        capacity = rtSide.capacity;
        length = rtSide.length;
        delete [] a;
        a = new char[capacity];
        for (int i = 0; i < length; i++)
            a[i] = rtSide.a[i];
        return *this;
    }
}
```

在下一个编程示例中提供了一个带有重载赋值运算符的完整示例。

### 显示 10.10 带有动态数组成员的类的定义

```cpp
// 此类的对象是部分填充的 double 型数组。
class PFArrayD {
public:
    PFArrayD();
    // 初始化容量为 50。
    PFArrayD(int capacityValue);
    PFArrayD(const PFArrayD& pfaObject);
    void addElement(double element);
    // 前置条件：数组未满。
    // 后置条件：元素已添加。
    bool full() const { return (capacity == used); }
    // 如果数组已满，则返回 true，否则返回 false。
    int getCapacity() const { return capacity; }
    int getNumberUsed() const { return used; }
    void emptyArray(int used = 0); // 清空数组。
    double& operator(int index);
    // 读取并访问更改到 0 到 numberUsed 之间的元素
    PFArrayD& operator =(const PFArrayD& rightSide);
private:
    PFArrayD();
    double *a;// 用于 double 型数组
    int capacity; // 用于数组的大小
    int used; // 用于当前使用的数组位置数量
};
```

### 显示 10.11 PFArray 类成员函数的定义（部分 1，共 2 部分）

```cpp
// 这些是 PFArray 类的成员函数的定义。
// 它们需要以下包含和使用（命名空间）指令：
#include <iostream>
//using std::cout;
```

```cpp
PFArray::PFArray() : capacity(50), used(0)
{
    a = new double[capacity];
}
```

```cpp
PFArray::PFArray(int size) : capacity(size), used(0)
{
    a = new double[capacity];
}
```

```cpp
PFArray::PFArray(const PFArray& pfaObject)
    : capacity(pfaObject.getCapacity()), used(pfaObject.getNumberUsed())
{
    a = new double[capacity];
    for (int i = 0; i < capacity; i++)
        a[i] = pfaObject.a[i];
}
```

```cpp
void PFArray::addElement(double element)
{
    if (used >= capacity)
    {
        cout << "Attempt to exceed capacity in PFArray.\n";
        exit(0);
    }
    a[used] = element;
    used++;
}
```

```cpp
double& PFArray::operator[](int index)
{
    if (index >= used)
    {
        cout << "Illegal index in PFArray.\n";
        exit(0);
    }
    return a[index];
}
```

### 显示 10.11 PFArrayD 类成员函数的定义（部分 2，共 2 部分）

```cpp
PFArrayD& PFArrayD::operator = (const PFArrayD& rightSide) {
    if (capacity != rightSide.capacity) {
        delete[] a;
        a = new double[rightSide.capacity];
    }
    capacity = rightSide.capacity;
    used = rightSide.used;
    for (int i = 0; i < used; i++)
        a[i] = rightSide.a[i];

    // 注意，这也检查了相同对象的情况
    return *this;
}

PFArrayD::~PFArrayD() {
    delete[] a;
}
```

### 显示 10.12 针对 PFArrayD 的程序（部分 1，共 2 部分）

```cpp
// 这是一个测试 PFArrayD 类的程序。
#include <iostream>
using namespace std;

// 测试 PFArrayD 类的定义
class PFArrayD {
public:
    PFArrayD();
    PFArrayD(int capacityValue);
    PFArrayD(const PFArrayD& pfaObject);
    void addElement(double element);
    bool full() const { return (capacity == used); }
    int getCapacity() const { return capacity; }
    int getNumberUsed() const { return used; }
    void emptyArray(int used = 0);
    double& operator(int index);
    PFArrayD& operator =(const PFArrayD& rightSide);
private:
    PFArrayD();
    double *a;
    int capacity;
    int used;
};

// 成员函数的具体定义如下...
PFArrayD::PFArrayD() : capacity(50), used(0) {
    a = new double[capacity];
}

PFArrayD::PFArrayD(int capacityValue) : capacity(capacityValue), used(0) {
    a = new double[capacity];
}

PFArrayD::PFArrayD(const PFArrayD& pfaObject) 
    : capacity(pfaObject.getCapacity()), used(pfaObject.getNumberUsed()) {
    a = new double[capacity];
    for (int i = 0; i < capacity; i++)
        a[i] = pfaObject.a[i];
}

void PFArrayD::addElement(double element) {
    if (used >= capacity) {
        cout << "Attempt to exceed capacity in PFArray.\n";
        exit(0);
    }
    a[used] = element;
    used++;
}

double& PFArrayD::operator[](int index) {
    if (index >= used) {
        cout << "Illegal index in PFArray.\n";
        exit(0);
    }
    return a[index];
}

PFArrayD& PFArrayD::operator =(const PFArrayD& rightSide) {
    if (capacity != rightSide.capacity) {
        delete[] a;
        a = new double[rightSide.capacity];
    }
    capacity = rightSide.capacity;
    used = rightSide.used;
    for (int i = 0; i < used; i++)
        a[i] = rightSide.a[i];
    return *this;
}

PFArrayD::~PFArrayD() {
    delete[] a;
}

int main() {
    PFArrayD temp(10);
    cout << "Enter some nonnegative numbers:\n";
    double next;
    while (cin >> next && next >= 0) {
        temp.addElement(next);
    }
    cout << "You entered the following " << temp.getNumberUsed() << " numbers:\n";
    for (int i = 0; i < temp.getNumberUsed(); i++)
        cout << temp[i] << " ";
    cout << endl;
    return 0;
}
```

Sample Dialogue

This program tests the PFArrayD class.
Enter some nonnegative numbers:
1.1
2.2
3.3
4.4
-1

You entered the following 4 numbers:
1.1 2.2 3.3 4.4 

### 显示 10.12 针对 PFArrayD 的程序（部分 2，共 2 部分）

```cpp
// 这是一个测试赋值运算符处理相同对象的程序。
#include <iostream>
using namespace std;

class PFArrayD {
public:
    PFArrayD();
    PFArrayD(int capacityValue);
    PFArrayD(const PFArrayD& pfaObject);
    void addElement(double element);
    bool full() const { return (capacity == used); }
    int getCapacity() const { return capacity; }
    int getNumberUsed() const { return used; }
    void emptyArray(int used = 0);
    double& operator(int index);
    PFArrayD& operator =(const PFArrayD& rightSide);
private:
    PFArrayD();
    double *a;
    int capacity;
    int used;
};

PFArrayD& PFArrayD::operator =(const PFArrayD& rightSide) {
    if (capacity != rightSide.capacity) {
        delete[] a;
        a = new double[rightSide.capacity];
    }
    capacity = rightSide.capacity;
    used = rightSide.used;
    for (int i = 0; i < used; i++)
        a[i] = rightSide.a[i];
    return *this;
}

// ... 其他成员函数定义 ...

int main() {
    PFArrayD s(10);
    PFArrayD t;
    cout << "Enter some nonnegative numbers to fill s:\n";
    double next;
    while (cin >> next && next >= 0) {
        s.addElement(next);
    }
    cout << "You entered the following " << s.getNumberUsed() << " numbers:\n";
    for (int i = 0; i < s.getNumberUsed(); i++)
        cout << s[i] << " ";
    cout << endl;

    cout << "Now test assignment to self:\n";
    s = s; 
    cout << "The capacity of s is " << s.getCapacity() << " and the length is " << s.getNumberUsed() << endl;

    return 0;
}
```

Sample Dialogue

Enter some nonnegative numbers to fill s:
1.1
2.2
3.3
4.4
-1

You entered the following 4 numbers:
1.1 2.2 3.3 4.4 

Now test assignment to self:
The capacity of s is 10 and the length is 4

