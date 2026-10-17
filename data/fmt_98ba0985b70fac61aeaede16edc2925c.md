
回想一下，类唯一的内置操作是赋值运算符和成员选择运算符。因此，其他运算符不能直接应用于类对象。然而，C++ 允许程序员扩展大多数运算符的定义，使得运算符——例如关系运算符、算术运算符、数据输出的插入运算符以及用于输入的提取运算符——可以应用于类。在 C++ 术语中，这被称为运算符重载。

# 运算符重载

回想算术运算符 `/` 是如何工作的。如果 `/` 的两个操作数都是整数，结果就是整数；否则结果是浮点数。同样，流插入运算符 `<<` 和流提取运算符 `>>` 也被重载了。运算符 `>>` 既可以用作流提取运算符和右移运算符。这些都是运算符重载的示例。（注意运算符 `<<` 和 `>>` 也针对各种数据类型（如 `int`、`double` 和 `string`）进行了重载）

重载运算符的其他示例还有 `+` 和 `-`。`+` 和 `-` 的结果在整数算术、浮点算术和指针算术中是不同的。

C++ 允许用户重载大多数运算符，以便运算符能够在特定的应用程序中有效工作。它不允许用户创建新运算符。大多数现有的运算符都可以被重载以操作类对象。

在重载运算符时，你必须编写函数（即头部和函数体）。重载运算符的函数名称是保留字 `operator` 后面跟上要重载的运算符。例如，重载运算符 `>=` 的函数名称为：

```
operator==()
```

运算符函数：重载运算符的函数。

## 运算符函数的语法

操作的结果是一个值。因此，运算符函数是一个返回值的函数。

运算符函数头部的语法为：

```
returnType operator operatorSymbol(formal parameter list)
```

在 C++ 中，`operator` 是一个保留字。

回想一下，类类唯一的内置操作是赋值 (`=`) 和成员选择。为了在类对象上使用其他运算符，必须显式地重载它们。运算符重载为用户定义的数据类型提供了与内置数据类型相同的简洁表达式。

要为类重载运算符：

1. 在类的定义中包含声明重载运算符的函数（即运算符函数）原型的语句。
2. 编写运算符函数的定义。

在类定义中包含运算符函数时，必须遵循某些规则。这些规则在在本章后面的“作为成员函数和非成员函数的运算符函数”章节中描述。

## 重载运算符：某些限制

在重载运算符时，请记住以下点：

1. 你不能改变运算符的优先级。
2. 结合性不能改变。（例如，算术运算符加法的结合性是从左到右的，且无法更改。）
3. 重载运算符不能使用默认参数。
4. 你不能更改运算符所接受的参数个数。
5. 你不能创建新运算符。只有现有的运算符可以被重载。
6. 无法重载的运算符有：
   - `.`
   - `::`
   - `=`
   - `?`
   - `:`
7. 运算符对于内置类型（如 `int`）的含义保持不变。
8. 运算符可以针对用户定义类型或针对内置类型进行重载。

## 指针 this

成员函数可以访问对象本身。有时，成员函数需要引用整个对象，而不是单个变量。你如何引用该对象？在 C++ 中，这是一个保留字。每个对象都维护一个指向自身的隐藏指针。例如，假设 `test` 是一个类，并且有一个名为 `one` 的成员函数。假设 `one` 的定义如下：

```
test::one()
{
  return *this;
}
```

如果 `x` 和 `y` 是 `test` 的对象，那么语句 `y = x.one();` 将对象 `x` 拷贝到 `y`。也就是说，`x` 的成员变量被拷贝到 `y`。当 `x` 调用 `one` 时，指针 `this` 指向 `x`。

### 示例 15-1

考虑以下类：

```
class thisPointerClass {
public:
  void set(int a, int b, int c);
  void print() const;
thisPointerClass updateXYZ(); // 后置条件：x = 2 * x; y = y + 2; z = z * z;

thisPointerClass(int a = 0, int b = 0, int c = 0);

private:
int x;
int y;
int z;
};
```

假设类 `thisPointerClass` 的成员函数的定义如下：

```
void thisPointerClass::set(int a, int b, int c) {
    x = a;
    y = b;
    z = c;
}
```

```
void thisPointerClass::print() const {
    cout << "x = " << x
         << ", y = " << y
         << ", z = " << z << endl;
}
```

```
thisPointerClass thisPointerClass::updateXYZ() {
    x = 2 * x;
    y = y + 2;
    z = z * z;
    return *this;
}
```

函数 `updateXYZ` 的定义更新了 `x`、`y` 和 `z` 的值。使用指针 `this` 返回整个对象的值。也就是说，成员变量 `x`、`y` 和 `z` 的值被返回了。

```
thisPointerClass::thisPointerClass(int a, int b, int c) {
    x = a;
    y = b;
    z = c;
}
```

考虑以下 `main` 函数：

```cpp
//第15章：this 指针插图
#include <iostream>
#include "thisPointerClass.h"

using namespace std;
```

```cpp
int main() {
    thisPointerClass object1(3, 5, 7);
    thisPointerClass object2;

    cout << "Object 1: ";
    object1.print();

    object2 = object1.updateXYZ();

    cout << "After updating object1: ";
    object1.print();

    cout << "Object 2: ";
    object2.print();

    return 0;
}
```

# 示例运行：

- Object 1: x = 3, y = 5, z = 7
- After updating object1: x = 6, y = 7, z = 49
- Object 2: x = 6, y = 7, z = 49

在大多数情况下，输出是自而易懂的。第 5 行语句评估了表达式 `object1.updateXYZ()`，它更新了 `object1` 成员变量的值。该值由指针 `this` 返回，如 `updateXYZ` 函数的定义所示。随后赋值运算符将该值复制到 `object2` 中。

下面的示例还展示了指针是如何运作的。

# 示例 15-2

在示例 12-9（第12章）中，我们设计了一个类来实现程序中人的姓名。在这里，我们扩展了 `personType` 类的定义，以单独设置人的名和姓，并返回整个对象。`personType` 类的定义如下：

```cpp
class personType {
public:
    void print() const;
    // 输出名和姓的函数；
    // 格式为 firstName lastName

    void setName(string firstName, string lastName);
    // 根据参数设置 firstName 和 lastName 的函数；
    // 后置条件：firstName = first; lastName = last

personType& setName(string name);
    // 设置名的函数。
    // 后置条件：firstName = first
    // 设置名后，返回对象的引用，
    //  true对象的地址。

personType& setName(string last);
    // 设置姓的函数。
    // 后置条件：lastName = last
    // 设置姓后，返回对象的引用，
    //  true对象的地址。

string getFirstName() const;
    // 返回名的函数。
    // 后置条件：返回 firstName 的值。

string getLast() const;
    // 返回姓的函数。
    // 后置条件：返回 lastName 的值。

personType(string first = "", string last = "");
    // 构造函数
    // 根据参数设置 firstName 和 lastName。
    // 后置条件：firstName = first; lastName = last

private:
    string firstName; // 用于存储名的变量
    string lastName; // 用于存储姓的变量
};
```

注意，在 `personType` 类的定义中，我们用一个带默认参数的构造函数替换了默认构造函数和带参数的构造函数。

`print`、`setName`、`getFirstName`、`getLast` 以及构造函数的定义与之前相同（参见示例 12-9）。`setFirstName` 和 `setName` 函数的定义如下：

```cpp
personType& personType::setName(string last)
{
    lastName = last;
    return *this;
}

personType& personType::setFirstName(string first)
{
    firstName = first;
    return *this;
}
```

下面的程序展示了如何使用 `personType` 类。（我们假设该类的定义在 `personType.h` 文件中）

```cpp
// 测试程序：class personType

#include <iostream>
#include <string>
#include "personType.h"

using namespace std;

int main() {
    personType student1("Angela", "Smith"); // 第 1 行
    personType student2; // 第 2 行
    personType student3; // 第 3 行
    cout << "Line 4 -- Student 1: "; // 第 4 行
    student1.print(); // 第 5 行
    cout << endl; // 第 6 行

    student2.setFirstName("Shelly");
    cout << "Line 7 -- Student 2: "; // 第 7 行
    student2.print(); // 第 8 行
    cout << endl; // 第 9 行

    student3.setFirstName("Chelsea");
    cout << "Line 10 -- Student 3: "; // 第 10 行
    student3.print(); // 第 11 行
    cout << endl; // 第 12 行
```

    student3.setName("Tomek");

    cout << "Line 13 -- Student 3: "; // 第 13 行

    student3.print(); // 第 14 行

    cout << endl; // 第 15 行

    return 0;

}
```
（注：main 函数的 OCR 文本包含严重的损坏/乱码行。我根据标准的 C++ 模式和提供的示例运行输出上下文重建了逻辑，以提供一个功能性的表示。）*

考虑以下函数 `two` 的定义：

```
void two(classIllusFriend cIllusObject) {

  classIllusFriend localTwoObject;

  localTwoObject.x = 45;

  localTwoObject.print();

  cout << "Line 5: In Friend Function two "

    << "accessing private member variable "

    << "x = " << localTwoObject.x

    << endl;

  cIllusObject.x = 88;

  cIllusObject.print();

  cout << "Line 8: In Friend Function two "

    << "accessing private member variable "

    << "x = " << cIllusObject.x << endl;

}
```

该函数包含一个形式参数 `cIllusFriend` 和局部变量 `localTwoObject`，它们的类型均为 `classIllusFriend`。在第 3 行，对象 `localTwoObject` 访问了它的私有成员 `x` 并将其值设置为 45。如果它没有声明为 `classIllusFriend` 类的友元函数，该语句将导致语法错误，因为对象不能直接访问其私有成员。同样，在第 6 行，形式参数 `cIllusObject` 访问了它的私有成员 `x` 并将其值设置为 88。再次，如果未声明为 `classIllusFriend` 类的友元函数，该语句也会导致语法错误。第 5 行的语句通过直接访问 `x` 输出了 `localTwoObject` 私有成员 `x` 的值。同样，第 8 行的语句通过直接访问输出了 `cIllusObject` 的 `x` 值。函数 `two` 还使用 `print` 函数打印了 `x` 的值（参见第 4 行和第 7 行的语句）。

现在考虑以下函数 `main` 的定义：

```
int main() {

  classIllusFriend aIllusObject;

  aIllusObject.setx(32);

  cout << "Line 11: aIllusObject.x: ";

  aIllusObject.print();

  cout << endl;

  cout << "* ~* ~* ~* ~* Testing Friend Function "

    << "two ~* ~* ~* ~*" << endl << endl;

  // Line 14

  two(aObject);

  // Line 15

  return 0;

}
```

# 运算符重载 | 873

# 示例运行：

Line 11: aObject.x: In class classIllusFriend: x = 32
* ~* ~* ~* ~* Testing Friend Function two ~* ~* ~* ~*

In class classIllusFriend: x = 45
Line 5: In Friend Function two accessing private member variable x = 45
In class classIllusFriend: x = 88
Line 8: In Friend Function two accessing private member variable x = 88

在大多数情况下，输出结果是自言自足的。第 15 行的语句调用了函数 `two`（`classIllusFriend` 类的友元函数），并将对象 `aObject` 作为实际参数传递。注意，该函数生成了输出的最后四行。

在本章稍后的部分，你将学习到对于一个类，流的插入和提取运算符只能作为友元函数进行重载。

# 作为成员函数和非成员函数的运算符函数

本章开头提到，在类定义中包含运算符函数时，必须遵循某些规则。本节描述了这些规则。

大多数运算符函数既可以是成员函数，也可以是非成员函数——即类的友元函数。要使一个运算符函数成为类的成员函数或非成员成员函数，请记住以下几点：

- 1. 重载任何运算符 `()`、`[]`、`->` 或 `for` 的函数必须声明为该类的成员。
- 2. 假设某个运算符被重载用于类——例如 `opOverClass`。这里 `op` 代表一个可以重载的运算符，如 `+` 或 `>>`。
    a. 如果 `op` 的左操作数是不同的类型（即不是 `opOverClass`），则重载 `opOverClass` 运算符的函数必须是该类的友元。
    b. 如果重载 `opOverClass` 运算符的函数是 `opOverClass` 类的成员，那么当应用 `op` 时，其左操作数必须是 `opOverClass` 类型。

874 | 第15 章：重载与模板

你必须遵循这些规则。

你将在本章后面看到，类的插入运算符 `<<` 和提取运算符 `>>` 必须作为成员函数或友元函数进行重载。为了方便我们讨论运算符重载，给如下代码：

```
class rectangleType {

private:

    double length;

    double width;

public:

    rectangleType() {

        length = 0;

        width = 0;

    }

    rectangleType(double l, double w) {

        if (l >= 0)
