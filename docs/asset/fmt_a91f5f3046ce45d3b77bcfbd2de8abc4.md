
在此函数定义中：

- 两个参数都是引用参数。
- 第一个参数（即 `object`）是一个 `ostream` 对象的引用。
- 第二个参数通常是某个特定类的 `const` 引用，因为（回想第 12 章）将对象作为参数传递的最有效方法是通过引用。在这种情况下，形式参数不需要复制实际参数的成员变量。在类名之前出现 `const` 单词是因为我们只想打印对象的成员变量。也就是说，函数不应修改对象的成员变量。
- 返回类型是对 `ostream` 对象的引用。

正如前面所述（当我们重载了插入运算符 `<<`），函数 `operator>>` 的返回类型必须是对 `ostream` 对象的引用。我们就可以成功执行如下类型的语句：

```
cin >> myRectangle >> yourRectangle;
```

### 15-6 展示了类重载插入和提取运算符

```cpp
#include <iostream>
using namespace std;
class rectangleType {
    // 重载插入和提取运算符
    friend ostream& operator<<(ostream&, const rectangleType&);
    friend istream& operator>>(istream&, rectangleType&);
public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;
};
rectangleType operator+(const rectangleType&, const rectangleType&);
// 重载运算符 +
rectangleType operator*(const rectangleType&, const rectangleType&);
// 重载运算符 *
bool operator+=(const rectangleType&, const rectangleType&);
// 重载运算符 +=
bool operator!=(const rectangleType&, const rectangleType&);
// 重载运算符 !=
rectangleType();
rectangleType(double l, double w);
private:
double length;
double width;
```

由于我们重载了流插入运算符 `<<`，我们删除了成员函数 `print`。

```cpp
// operator+, operator*, 和 operator!= 的函数定义与示例 15-5 相同。
```

```cpp
ostream& operator<<(ostream& osObject, const rectangleType& rectangle) {
    osObject << "Length = " << rectangle.length
             << " Width = " << rectangle.width;
    return osObject;
}
```

```cpp
istream& operator>>(istream& isObject, rectangleType& rectangle) {
    isObject >> rectangle.length >> rectangle.width;
    return isObject;
}
```

考虑以下程序。（我们假设 `rectangleType` 类的定义在头文件 `rectangleType.h` 中。）

```cpp
// 此程序展示了如何使用修改后的 rectangleType 类。
```

```cpp
#include <iostream>
#include "rectangleType.h"
using namespace std;
int main()
{
    rectangleType myRectangle(23, 45);
    rectangleType yourRectangle;
    cout << "Line 3: myRectangle: " << myRectangle
         << endl;
    cout << "Line 4: Enter the length and width "
          <<"of a rectangle: ";
    cin >> yourRectangle;
    cout << endl;
}
```

# 运算符重载 | 887

```cpp
cout << "Line 7: yourRectangle: "
 << yourRectangle << endl;
```

```cpp
cout << "Line 8: myRectangle + yourRectangle: "
 << yourRectangle + yourRectangle << endl;
cout << "Line 9: myRectangle * yourRectangle: "
 << yourRectangle * yourRectangle << endl;
```

```cpp
return 0;
```

示例运行：在这次简单的运行中，用户被定义了。

Line 3: myRectangle: Length = 23; Width = 45

Line 4: Enter the length and width of a rectangle: 32 15

Line 7: yourRectangle: Length = 32; Width = 15

Line 8: myRectangle + yourRectangle: Length = 55; Width = 60

Line 9: myRectangle * yourRectangle: Length = 736; Width = 675

第 1 和第 2 行的语句将 `myRectangle` 初始化为 `rectangleType` 类型的对象。第 3 行的语句使用 `cout` 和插入运算符输出 `myRectangle` 的值。第 5 行的语句使用 `cin` 和提取运算符将数据输入 `yourRectangle`。第 7 行的语句使用 `cout` 和插入运算符输出 `yourRectangle` 的值。第 8 行的语句将 `myRectangle` 和 `yourRectangle` 的长度和宽度相加并输出结果。类似地，第 9 行的 `cout` 语句将 `myRectangle` 和 `yourRectangle` 的长度和宽度相乘并输出结果。输出显示，流插入运算符和提取运算符都已成功重载。

# 载类重载赋值运算符 (=)

类的内置运算符之一是赋值运算符。赋值运算符会对类的成员变量执行成员级拷贝。例如，语句：

`myRectangle = yourRectangle;`

等同于以下语句：

`myRectangle.length = yourRectangle.length;`

`myRectangle.width = yourRectangle.width;`

回想第 14 章，内置赋值运算符对于没有指针成员变量的类效果良好，但对于带有指针成员变量的类则无效。因此，为了避免带有指针成员变量的类出现数据的浅拷贝，我们必须重载赋值运算符。

回想，要为类重载赋值运算符 `=`，运算符函数 `operator=` 必须是该类的成员。

# 为类重载赋值运算符 = 的通用语法

下面描述了为类重载赋值运算符 `=` 的语法。

函数原型（应包含在类的定义中）：

```cpp
const className& operator=(const className&);
```

函数定义：

```cpp
const className& className::operator=
    (const className& rightObject)
{
    // 局部声明（若有的话）
    if (this != &rightObject) // 避免自我赋值
    {
        // 将 rightObject 拷贝到此对象的算法
    }
    return *this;
}
```

在函数 `operator=::` 的定义中：

- 只有一个形式参数。
- 形式参数通常是特定类的 `const` 引用。
- 返回类型是特定类的常量引用。

我们解释一下为什么函数 `operator=` 的返回类型应该是该类类型的引用。

假设为 `rectangleType` 类重载了赋值运算符 `=`。

语句：

`myRectangle = yourRectangle;`

等同于语句：

`myRectangle.operator=(yourRectangle);`

也就是说，对象 `yourRectangle` 变成了函数 `operator=` 的实际参数。

现在考虑以下语句：

`myRectangle = yourRectangle = tempRect;`

因为运算符 `=` 的结合性是从右到左的，该语句等同于语句：

`myRectangle.operator=(yourRectangle.operator=(tempRect)); // Line A`

# 运算符重载 | 889

显然，我们必须首先执行表达式：

`yourRectangle.operator=(tempRect)`

即表达式：

```cpp
yourRectangle = tempRect
```

表达式：

`yourRectangle.operator=(tempRect)`

返回的值将成为函数 `operator=` 的参数，以便为对象 `myRectangle` 赋值（参见 Line A 中的语句）。由于函数 `operator=` 的形式参数是一个引用参数，表达式：

`yourRectangle.operator=(tempRect)`

必须返回一个对象的引用，而不是其值*value*。也就是说，它必须返回对象 `yourRectangle` 的引用，而不是 `yourRectangle` 的值。出于此原因，为类重载赋值运算符 `=` 的函数的返回类型必须是该类类型的引用。

现在考虑以下语句：

```cpp
myRectangle = myRectangle; // Line B
```

在这里，我们正试图将 `myRectangle` 的值拷贝到 `myRectangle`；也就是说，该语句是一个自我赋值。我们必须防止此类赋值的原因之一是它们会浪费计算机时间。然而，我们首先解释赋值运算符的体是如何防止此类赋值的。

如所述，函数 `operator=` 的体确实防止了赋值，如 Line B 所示。让我们来看看：

考虑对象函数 `operator=` 体中的 `if`：

```cpp
if (this != &rightObject) // 避免自我赋值
// 将 rightObject 拷贝到此对象的算法
```

语句：

`yourRectangle = myRectangle;`

被编译为语句：

`myRectangle.operator=(myRectangle)`

因为函数 `operator=` 是由对象 `myRectangle` 调用的，所以函数体中的指针 `this` 指向对象 `myRectangle`。此外，由于 `myRectangle` 也是函数 `operator=` 的参数，表达式：

```cpp
this != &rightObject
```

`this` 和 `&rightObject` 都指向 `myRectangle` 的地址。因此，该表达式结果为假，相应的 `if` 语句将被跳过。此说明说明了赋值运算符的体防止自我赋值的另一个原因。让我们考虑以下类：

```cpp
class arrayClass{
public:
    const arrayClass& operator=(const arrayClass&);
private:
    int *list;
    int length;
    int maxSize;
};
```

`arrayClass` 类有一个指针成员变量 `list`，用于创建存储整数的数组。假设 `arrayClass` 的赋值函数定义没有 `if` 语句如下：

```cpp
const arrayClass & arrayClass::operator=
    (const arrayClass& otherList)
{
    delete [] list; // Line 1
    maxSize = otherList.maxSize; // Line 2
    length = otherList.length; // Line 3
    list = new int[maxSize]; // Line 4
    for (int i = 0; i < length; i++) // Line 5
        list[i] = otherList.list[i]; // Line 6
    return *this; // Line 7
}
```

假设用户程序中有如下声明：

`arrayClass myList;`

考虑以下语句：

`myList = myList;`

# 运算符重载 | 891

这是一个自我赋值。当该语句在函数 `operator=` 的体内执行时：

- 1. `list` 意味着 `myList.list`，`maxSize` 意味着 `myList.maxSize`，`length` 意味着 `myList.length`。
- 2. `otherList` 与 `myList` 相同。

Line 1 的语句销毁了 `list`，即 `myList.list`，存储数字的数组不再存在。也就是说，它是无效的。问题出现在 Line 6。在这里，表达式 `list[i] = otherList.list[i]` 等于语句 `myList[i] = myList[i]`。由于 `myList[i]` 没有有效数据（它在 Line 1 被销毁了），Line 6 的语句产生垃圾数据。

因此，函数 `operator=` 的定义必须防止自我赋值。`arrayClass` 类 `operator=` 的正确定义如下：

```cpp
const arrayClass& arrayClass::operator=
    (const arrayClass& otherList)
{
    if (this != &otherList) // Line 1
        delete []list; // Line 2
        maxSize = otherList.maxSize; // Line 3
        length = otherList.length; // Line 4
    list = new int[maxSize]; // Line 5
    for (int i = 0; i < length; i++) // Line 6
        list[i] = otherList.list[i]; // Line 7
    return *this; // Line 8
}
```

# 示例 15-7

以下示例展示了如何重载赋值运算符。

```cpp
class cAssignmentOpOverload{
public:
    const cAssignmentOpOverload&
        operator=(const cAssignmentOpOverload& otherList)
    // 重载赋值运算符
```

```cpp
void print() const;
//打印列表的函数
```

```cpp
void insertEnd(int item);
//在列表末尾插入一个元素的函数
// 后置条件：如果列表未满，
// length++; list[length] = item;
//
// 如果列表已满，
// 输出相应的错误
```

```cpp
void destroyList();
//销毁列表的函数
// 后置条件：length = 0; maxSize = 0; list = NULL;
```

```cpp
cAssignmentOpOverload(int size = 0);
// 构造函数：length = 0; maxSize = size;
// list 是一个大小为 maxSize 的数组
```

```cpp
private:
int maxSize;
int length;
int *list;
```

`cAssignmentOpOverload` 类成员函数的定义如下：

```cpp
void cAssignmentOpOverload::print() const
{
  if (length == 0)
    cout << "The list is empty." << endl;
  else
    for (int i = 0; i < length; i++)
      cout << list[i] << " ";
}
```

```cpp
void cAssignmentOpOverload::insertEnd(int item)
{
  if (length == maxSize)
    cout << "List is full" << endl;
  else
    list[length++] = item;
}
```

```cpp
void cAssignmentOpOverload::destroyList()
{
  delete list;
  list = NULL;
  length = 0;
  maxSize = 0;
}
```
