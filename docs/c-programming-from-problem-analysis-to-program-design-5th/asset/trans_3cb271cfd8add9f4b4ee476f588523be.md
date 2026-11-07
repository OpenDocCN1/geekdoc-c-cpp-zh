
## 示例 14-2

考虑以下语句：

```cpp
int *p;
int x;
```

假设 p 和 x 的内存分配如图 14-2 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_838_0.png)

**图 14-2** 主存、p 和 x

&p、p、*p、&x 和 x 的值如下所示：

| 表达式 | 值 |
|---|---|
| `&p` | `1400` |
| `p` | `? (unknown)` |
| `*p` | `Does not exist (undefined)` |
| `&x` | `1750` |
| `x` | `? (unknown)` |

假设按给定顺序执行以下语句：

```cpp
x = 50;
p = &x;
*p = 38;
```

在这些语句中的每一条执行后，&p、p、*p、&x 和 x 的值如下所示。

执行语句 `x = 50;` 后，&p、p、*p、&x 和 x 的值如下：

| `&p` | `p` | `*p` | `&x` | `x` |
|---|---|---|---|---|
| `1400` | `? (unknown)` | `Does not exist (undefined)` | `1750` | `50` |

执行语句 `p = &x;` 后，&p、p、*p、&x 和 x 的值如下：

| `&p` | `p` | `*p` | `&x` | `x` |
|---|---|---|---|---|
| `1400` | `1750` | `50` | `1750` | `50` |

执行语句 `*p = 38;` 后，&p、p、*p、&x 和 x 的值如下。（因为 *p 和 x 引用同一个内存位置，x 的值也变为 38。）

| `&p` | `p` | `*p` | `&x` | `x` |
|---|---|---|---|---|
| `1400` | `1750` | `38` | `1750` | `38` |

我们需要注意以下几点：

- 1. **p** 是一个指针变量。
- 2. **p** 的内容仅指向 `int` 类型的内存位置。
- 3. 内存位置 **x** 存在，且类型为 `int`。因此，赋值语句：
  
  ```cpp
  p = &x;
  ```
  
  是合法的。该赋值语句执行后，`*p` 是有效且有意义的。

示例 14-3 中的程序进一步说明了指针变量是如何工作的。

## 示例 14-3

以下程序说明了指针变量的工作方式：

```cpp
//Chapter 14: Example 14-3

#include <iostream>

using namespace std;

int main()
{
    int *p;
    int x = 37;

    cout << "Line 1: x = " << x << endl;                  //Line 1

    p = &x;                                                //Line 2

    cout << "Line 3: *p = " << *p
         << ", x = " << x << endl;                       //Line 3

    *p = 58;                                               //Line 4

    cout << "Line 5: *p = " << *p
         << ", x = " << x << endl;                       //Line 5

    cout << "Line 6: Address of p = " << &p << endl;       //Line 6

    cout << "Line 7: Value of p = " << p << endl;         //Line 7

    cout << "Line 8: Address of the memory location "
         << "pointed to by *p = " << *p << endl;           //Line 8
    cout << "Line 9: Address of x = " << &x << endl;       //Line 9
    cout << "Line 10: Value of x = " << x << endl;        //Line 10

    return 0;
}
```

在上述声明中，`student` 是 `studentType` 类型的对象，`studentPtr` 是 `studentType` 类型的指针变量。以下语句将 `student` 的地址存储到 `studentPtr` 中：

```cpp
studentPtr = &student;
```

以下语句将 3.9 存储到对象 `student` 的成员 `gpa` 中：

```cpp
(*studentPtr).gpa = 3.9;
```

表达式 `(*studentPtr).gpa` 是指针解引用和类成员选择的组合。在 C++ 中，点运算符 `.` 的优先级高于解引用运算符。

让我们稍微详细说明一下。在表达式 `(*studentPtr).gpa` 中，运算符 `*` 首先求值，因此表达式 `*studentPtr` 首先求值。因为 `studentPtr` 是 `studentType` 类型的指针变量，`*studentPtr` 引用的是类型为 `studentType` 的内存空间，它就是一个 `struct`。因此，`(*studentPtr).gpa` 引用的是该 `struct` 的 `gpa` 成员。

考虑表达式 `*studentPtr.gpa`。让我们看看这个表达式是如何求值的。因为 `.`（点）的优先级高于 `*`，所以表达式 `studentPtr.gpa` 首先求值。表达式 `studentPtr.gpa` 会导致语法错误，因为 `studentPtr` 不是 `struct` 变量，因此它没有 `gpa` 这样的成员。

正如你所看到的，在表达式 `(*studentPtr).gpa` 中，括号很重要。然而，拼写错误可能会带来问题。因此，为了简化通过指针访问类或结构体成员，C++ 提供了另一个运算符，称为**成员访问运算符箭头** `->`。运算符 `->` 由两个连续的符号组成：一个连字符和一个“大于”号。

使用运算符 `->` 访问类（`struct`）成员的语法是：

```cpp
pointerVariableName->classMemberName
```

因此，语句：

```cpp
(*studentPtr).gpa = 3.9;
```

等价于语句：

```cpp
studentPtr->gpa = 3.9;
```

通过指针并使用运算符 `->` 来访问类（`struct`）成员，从而无需再使用括号和解引用运算符。由于拼写错误难以避免，且缺少括号可能导致程序异常终止或错误结果，因此本书在通过指针访问类（`struct`）成员时使用箭头表示法。

示例 14-4 说明了指针如何与类成员函数一起工作。

## 示例 14-4

考虑以下类：

```cpp
class classExample
{
public:
    void setX(int a);
        //Function to set the value of x
        //Postcondition: x = a;
    void print() const;
        //Function to output the value of x

private:
    int x;
};
```

成员函数的定义如下：

```cpp
void classExample::setX(int a)
{
    x = a;
}

void classExample::print() const
{
    cout << "x = " << x << endl;
}
```

考虑以下 main 函数：

```cpp
int main()
{
    classExample *cExpPtr;    //Line 1
    classExample cExpObject;  //Line 2

    cExpPtr = &cExpObject;    //Line 3

    cExpPtr->setX(5);         //Line 4
    cExpPtr->print();         //Line 5

    return 0;
}
```

### 示例运行：

x = 5

在 main 函数中，第 1 行的语句将 cExpPtr 声明为 classExample 类型的指针，第 2 行的语句将 cExpObject 声明为 classExample 类型的对象。第 3 行的语句将 cExpObject 的地址存储到 cExpPtr 中（见图 14-3）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_843_0.png)

**图 14-3** 语句 `cExpPtr = &cExpObject;` 执行后的 `cExpObject` 和 `cExpPtr`

在第 4 行的语句中，指针 `cExpPtr` 访问成员函数 `setX` 来设置成员变量 `x` 的值（见图 14-4）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_843_1.png)

**图 14-4** 语句 `cExpPtr->setX(5);` 执行后的 `cExpObject` 和 `cExpPtr`

在第 5 行的语句中，指针 `cExpPtr` 访问成员函数 `print` 来打印 `x` 的值，如上所示。

## 初始化指针变量

由于 C++ 不会自动初始化变量，如果你不希望指针变量指向任何东西，就必须对它们进行初始化。指针变量使用常量值 0 进行初始化，称为**空指针**。因此，语句 `p = 0;` 将空指针存储在 `p` 中，也就是说，`p` 不指向任何东西。有些程序员使用命名常量 `NULL` 来初始化指针变量。以下两条语句是等价的：

```cpp
p = NULL;
p = 0;
```

数字 0 是唯一可以直接赋给指针变量的数字。

## 动态变量

在前几节中，你学习了如何声明指针变量、如何将变量的地址存储到与该变量类型相同的指针变量中，以及如何使用指针操作数据。然而，你只学会了如何使用指针在由其他变量创建的内存空间中操作数据。换句话说，指针操作的是已存在的内存空间中的数据。那么，使用动态变量有什么好处呢？
