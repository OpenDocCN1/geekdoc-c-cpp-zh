
```cpp
1 // 本程序演示了拷贝构造函数的用法。
2 #include <iostream>
3 #include <iomanip>
4 #include "NumberArray.h"
5
6 using namespace std;
7
8 int main()
9 {
10 NumberArray first(3,10.5);
11 // 为第一个对象创建一个拷贝
12 NumberArray second = first;
13
14 // 显示两个对象的值
15 cout << setprecision(2) << fixed << showpoint << "\n";
16 cout << "Value stored in first object is ";
17 first.print();
18 cout << "\nValue stored in second object is ";
19 second.print();
20 cout << "\nonly the value in second object will "
21 << "changed.";
22
23 // 现在更改第二个对象中存储的值
24 second.setValue(20.5);
25
26 // 显示两个对象中存储的值
27 cout << "Value stored in first object is ";
28 first.print();
29 cout << endl << "Value stored in second object is ";
30 second.print();
31 return 0;
32 }
```

### 程序输出

Value stored in first object is 10.50 10.50 10.50

Value stored in second object is 10.50 10.50 10.50

Only the value in second object will be changed.

Value stored in first object is 10.50 10.50 10.50

Value stored in second object is 20.50 20.50 20.50

> 注意：拷贝构造函数必须有一个单一参数，该参数是同类对象的引用。忘记掉标识引用参数的 `&` 将导致编译器错误。此外，该参数应该是 `const` 引用，因为拷贝构造函数不应该修改正在拷贝的对象。

# 11.5 拷贝构造函数

每当在函数调用中按值传递对象时，编译器也会自动调用拷贝构造函数来创建该对象的拷贝。正因如此，拷贝构造函数的参数必须通过引用的方式传递；如果在调用构造函数时按值传递参数，那么构造函数将不得不立即再次调用以创建拷贝，从而导致无尽的调用链。

## 拷贝构造函数的调用

每当使用另一个同类对象来初始化一个对象时，系统会自动调用拷贝构造函数。例如，对于 `Rectangle` 类，在以下每个语句都会调用其拷贝构造函数：

```cpp
Rectangle box(5, 10); // 初始化语句
Rectangle b = box; // 初始化语句
Rectangle b1(box); // 初始化语句
```

当函数接收一个类类型的参数时，拷贝构造函数也会被自动调用。例如，如下形式的函数

```cpp
void fun(Rectangle rect)
{}
```

如下的调用

```cpp
fun(box);
```

将导致拷贝构造函数的调用。最后，每当函数按值返回一个类对象时，拷贝构造函数会被自动调用。因此，在函数

```cpp
Rectangle make()
{
    Rectangle rect(2, 3);
    return rect;
}
```

在执行返回语句时，拷贝构造函数会被调用，，因为返回语句必须创建一个该对象的临时非局部拷贝，以供调用者使用。总而言之，在以下情况下会调用类构造函数：

- 从一个对象初始化变量时

- 按值传递一个类对象时

- 函数按值返回一个类对象时

> 注意：拷贝构造函数必须有一个单一参数，该参数是同类对象的引用。忘记掉标识引用参数的 `&` 将导致编译器错误。此外，该参数应该是 `const` 引用，因为拷贝构造函数不应该修改正在拷贝的对象。

# 习题

- 11.8 简述什么是成员赋值。

- 11.9 描述发生成员赋值的情景。

- 11.10 描述不需要使用成员赋值的情况。

- 11.11 拷贝构造函数何时调用？

- 11.12 构造函数如何知道是成员赋值？

- 11.13 默认赋值执行了什么操作？

# 运算符重载

为了解决对象成员赋值产生的问题，我们需要修改赋值运算符的行为，使其在应用于具有指针的类时，执行成员赋值以外的操作。实际上，我们为具有指针的类提供了赋值运算符的不同版本。

要重载某个类的赋值运算符，是在该类的成员中定义一个名为 `operator=` 的运算符函数。对于 `NumberArray` 数组，这样做，我们可以如下编写类声明：

```cpp
class NumberArray {
private:
    double *aPtr;
    int arraySize;
public:
    void operator=(const NumberArray& right); // 重载运算符
    NumberArray(const NumberArray&);
    NumberArray(int size, double value);
    ~NumberArray() { if (arraySize > 0) delete [] aptr; }
    void print() const;
    void setValue(double value);
};
```

在查看运算符函数的实现之前，让我们先看看函数头部（或原型）。我们将头部分解为几个主要部分，如图 11-4 所示。

### 图 11-4

| 返回类型 | 函数名称 | 运算符右侧对象的参数 |

|---|---|---|

| NumberArray& | operator= | (const NumberArray&right) |

该函数的名称是 `operator`。由于运算符函数是类的实例成员，它只能通过类对象来调用。通过调用它的类对象被视为赋值的左操作数

# 第 11 章更多关于类和面向对象编程

operator，其中传递给函数的参数被视为赋值运算符的右操作数。为了说明这一点，让我们假设程序中定义了两个对象，left 和 right：

```
NumberArray left(3, 10.5);
NumberArray right(5, 20.5);
```

要将 `right` 的值赋给 `left`，我们调用 `left` 对象的成员函数 `operator=`并将 `right` 对象作为参数传递给它：

```
left.operator=(right);
```

虽然你可以这样调用 operator 函数，编译器也允许你使用更传统的表示法：

```
left = right;
```

> 注意：operator函数的参数不需要通过引用传递，也不需要声明为 `const`。在这个示例中，出于效率考虑，我们使用了引用：引用参数可以避免作为参数传递的对象的拷贝开销。`const` 用于保护参数不被修改。

## 类赋值运算符的返回值

图 11-4 显示重载的 `=` 运算符返回一个 `NumberArray` 的引用。这样做是为了与 C++ 内置的赋值运算符保持一致，该运算符允许像下面的级联赋值语句：

```
a = b = c;
```

级联赋值之所以有效，是因为内置赋值运算符的实现方式是在执行赋值后返回其操作数的引用。因此，在句语句中，表达式 `b = c` 会导致 `c` 被赋给 `b`，然后返回 `b` 的引用。该返回引用的值被赋给 `a`。

## 类赋值运算符的实现

让我们考虑赋值运算符的实现。首先注意到，如果像下面的语句

```
x = x;
```

导致对象被赋值给自己（这种赋值在大型程序中可能会间接发生），则不需要进行任何拷贝。我们可以通过检查赋值左侧对象的地址与右侧对象的地址是否不同来测试这一点：

```
if(this != &right) ( /* 拷贝对象 */ )
```

赋值运算符函数首先删除被赋值对象中为指针分配的内存。之后，它以与类的拷贝构造函数相同的方式对另一个对象进行拷贝。函数的最后一个动作是：

# 11.6 运算符重载

返回（通过引用）赋值左侧的对象 *this*。以下是该函数的代码：

```
NumberArray& NumberArray::operator=(const NumberArray&right)
{
    if (this != &right)
    {
        if (arraySize > 0)
        {
            delete [] aPtr;
        }
        arraySize = right.arraySize;
        aPtr = new double[arraySize];
        for (int index = 0; index < arraySize; index++)
        {
            aPtr[index] = right.aPtr[index];
        }
    }
    return *this;
}
```

本节讨论的赋值运算符也称为拷贝赋值（copy assignment），以区分我们将学习的移动赋值运算符。通常，在构造函数中分配动态内存（或任何类型的资源）的类应该始终定义析构函数、拷贝构造函数、移动构造函数、拷贝赋值运算符和移动运算符。你将在本章稍后部分学习赋值构造函数和移动构造函数。

程序 11-9 展示了经过修改包含拷贝构造函数和重载赋值运算符的 `NumberArray` 类。

# 程序 11-9

```
overload.h 内容
1 #include <iostream>
2 using namespace std;
3
4 class NumberArray
5 {
6 private:
7 double *aPtr;
8 int arraySize;
9 public:
10 // 重载运算符函数
11 NumberArray&operator=(const NumberArray&right);
12
13 // 构造函数和其他成员函数
14 NumberArray(const NumberArray &);
15 NumberArray(int size, double value);
16 ~NumberArray() { if (arraySize > 0) delete [] aPtr; }
17 void print() const;
18 void setValue(double value);
19 );
```

（继续）

# 程序 11-9（续）

```
overload.cpp 内容
1 #include <iostream>
2 #include "overload.h"
3 using namespace std;
4

5 // 赋值重载运算符函数 *
6 NumberArray& NumberArray::operator=(const NumberArray &right)
8 {
10 if (this != &right)
11 {
13 if (arraySize > 0)
14 {
15 delete [] aPtr;
16 }
17 arraySize = right.arraySize;
18 for (int index = 0; index < arraySize; index++)
19 {
21 aPtr[index] = right.aPtr[index];
22 }
23 return *this;}
```

```
27 // 拷贝构造函数。
29 NumberArray::NumberArray(const NumberArray &obj)
30 {
32 arraySize = obj.arraySize;
33 aPtr = new double[arraySize];
34 for (int index = 0; index < arraySize; index++)
35 {
36 aPtr[index] = obj.aPtr[index];
37 }
```

```
40 // 构造函数。
42 NumberArray::NumberArray(int size1, double value)
43 {
44 arraySize = size1;
45 aPtr = new double[arraySize];
46 setValue(value);
47 }
```

50 // 设置数组所有项的值。

（继续）

# 程序 11-9（续）

```
52 void NumberArray::setValue(double value)
```

```
53 {
54   for(int index = 0; index < arraySize; index++)
55   {
56     aPtr[index] = value;
57   }
58 }
59
60 // 打印数组中的所有项。
61 //**********************************
62 //**********************************
63 void NumberArray::print() const
64 {
65   for(int index = 0; index < arraySize; index++)
66   {
67     cout << aPtr[index] << " ";
68   }
69 }
```

# 程序 11-9（续）

```
11-9.cpp 内容
1 // 此程序演示了赋值运算符
2 // 重载。
3 #include <iostream>
4 #include <iomanip>
5 #include "overload.h"
6 using namespace std;
7
8 int main()
9 { NumberArray first(3, 10.5);
10 NumberArray second(5, 20.5);
11
12 // 显示两个对象的值
13 cout << setprecision(2) << fixed << showpoint;
14 cout << "First object's data is ";
15 first.print();
16 cout << endl << "Second object's data is ";
17 second.print();
18
19 // 调用重载运算符
20 cout << "Now we will assign the second object"
21 << to the first." << endl;
22 first = second;
23
24 // 显示两个对象的值
25 cout << "First object's data is ";
26 first.print();
27 cout << endl << "Second object's data is ";
28 second.print();
29
30 return 0;
31 }
```

### 程序输出

```
First object's data is 10.5 10.5 10.5 
Second object's data is 20.5 20.5 20.5 20.5 20.5 
Now we will assign the second object to the first.
First object's data is 20.5 20.5 20.5 
Second object's data is 20.5 20.5 20.5 20.5 20.5 
```

# 重载其他运算符

C++ 允许程序员重载赋值运算符以外的其他运算符。在许多情况下，重载某些 C++ 内置运算符来与类一起是很自然的。例如，假设存在一个名为 `Date` 的类，`Date` 对象持有日、月、年。假设 `Date` 类添加了一个成员函数。该成员函数向日期增加天数，如果日期跨到另一个月份或年份，则调整成员变量。例如，以下语句向 `today` 对象中的日期增加天数：

```
today.add(5);
```

虽然一眼看出语句是在向日期增加五天，但使用运算符会更直观。例如，看以下语句：

```
today += 5;
```

# 运算符重载的一些通用问题

现在你已经对运算符重载有了介绍，让我们来看看这种编程技术涉及的一些通用问题。

首先，你可以改变运算符的含义，这意味着没有什么可以阻止你将 `=` 符号从赋值运算符更改为“显示”运算符。例如，以下类就是这样做的：

```
class Weird
{
  private:
    int value;
```

## 11.6 运算符重载

```cpp
public:
  Weird(int v) : value(v) {}
  void operator=(const Weird &right) {
    cout << right.value << endl;
  }
```

尽管 `operator=` 函数重载了赋值运算符，但该函数并没有执行赋值操作。重载的运算符所做的只是显示 `right.value` 的内容。考虑以下程序段：

```cpp
Weird a(5), b(10);
a = b;
```

虽然语句 `a = b` 看起来像是一个赋值语句，但它实际上会将 `b.value`成员的内容显示在屏幕上：

```
10
```

另一个运算符重载的问题是，你不能更改运算符所的操作数个数。`=` 符号必须始终二元运算符。同样，`++` 和 `--` 必须始终是一元运算符。

最后一个问题是，尽管你可以重载大部分 C++ 运算符，但你不能重载所有的运算符。表 11-1 显示了所有可以重载的 C++ 运算符。

> 注意：表 11-1 中的某些运算符超出了本书的范围，未进行介绍。
