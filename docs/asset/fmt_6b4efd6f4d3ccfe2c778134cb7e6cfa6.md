
```cpp
            length = 0;

        if (w >= 0)

            width = w;

        else

            width = 0;

    }

    void setDimension(double l, double w) {

        length = l;

        width = w;

    }

    void setx(double x) { length = x;

    }

    double getLength() const {

        return length;

    }

    double getWidth() const {

        return width;

    }

    double area() const {

        return length * width;

    }

    double perimeter() const {

        return 2 * (length + width);

    }

    void print() const {

        cout << "Length = " << length << " Width = " << width;

    }

    friend ostream& operator<<(ostream& os, const rectangleType& obj) {

        os << "Length = " << obj.length << " Width = " << obj.width;

        return os;

    }

    friend istream& operator>>(istream& is, rectangleType& obj) {

        is >> obj.length >> obj.width;

        return is;

    }

};
```

# 将二元运算符（算术或关系运算符）重载为成员函数的通用语法

本节描述了将二元运算符重载为类成员函数的通用形式。

函数原型（应包含在类的定义中）：

```cpp
returnType operator#(const className&) const;
```

其中 `#` 代表要重载的二元运算符（算术或关系运算符）；
`returnType` 是函数返回值的类型；
`className` 是要重载该运算符的类名。

函数定义：

```cpp
returnType className::operator#
(const className& otherObject) const
{
    //执行操作的算法
    return value;
}
```

> 注意：重载关系运算符的函数返回类型为 `bool`。

# 示例 15-4

让我们为 `rectangleType` 类重载 `+`、` * `、`==` 和 `!=`。这些运算符均被重载为成员函数。

```cpp
class rectangleType
{
public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;
    rectangleType operator+(const rectangleType&) const;
    // 重载运算符 +
    rectangleType operator*(const rectangleType&) const;
    // 重载运算符 *
    bool operator==(const rectangleType&) const;
    // 重载运算符 ==
    bool operator!=(const rectangleType&) const;
    // 重载运算符 !=
    rectangleType();
    rectangleType(double l1, double w);
private:
    double length;
    double width;
};
```

函数 `operator+` 的定义如下：

```cpp
rectangleType rectangleType::operator+(const rectangleType& rectangle) const {
  rectangleType tempRect;
  tempRect.length = length + rectangle.length;
  tempRect.width = width + rectangle.width;
  return tempRect;
}
```

注意，`operator+` 将两个矩形的对应的长度和宽度相加。函数 `operator*` 的定义如下：

```cpp
rectangleType rectangleType::operator*(const rectangleType& rectangle) const {
  rectangleType tempRect;
  tempRect.length = length * rectangle.length;
  tempRect.width = width * rectangle.width;
  return tempRect;
}
```

注意，`operator*` 将两个矩形的对应的长度和宽度相乘。如果两个矩形的长度和宽度都相等，则它们相等。因此，重载运算符 `==` 的函数定义为：

```cpp
bool rectangleType::operator==(const rectangleType& rectangle) const {
  return (length == rectangle.length && width == rectangle.width);
};
```

如果两个矩形的长度不等或宽度不等，则它们不相等。因此，重载运算符 `!=` 的函数定义为：

```cpp
bool rectangleType::operator!=
  (const rectangleType& rectangle) const
{
    return (length != rectangle.length ||
           width != rectangle.width);
}
```

（注：在编写完重载运算符 `==` 的定义后，可以使用它来编写重载运算符 `!=` 的函数定义。细节留作练习）。

考虑以下程序。（我们假设 `rectangleType` 类的定义在头文件 `rectangleType.h` 中。）

```cpp
// 此程序展示了如何使用类 rectangleType。
#include <iostream>
#include "rectangleType.h"
using namespace std;
int main()
{
    rectangleType rectangle1(23, 45); // 第 1 行
    rectangleType rectangle2(12, 10); // 第 2 行
    rectangleType rectangle3; // 第 3 行
    rectangleType rectangle4; // 第 4 行
    cout << "Line 5: " << rectangle1; // 第 5 行
    rectangle1.print(); // 第 6 行
    cout << endl; // 第 7 行
    cout << "Line 8: " << rectangle2; // 第 8 行
    rectangle2.print(); // 第 9 行
    cout << endl; // 第 10 行
    rectangle3 = rectangle1 + rectangle2; // 第 11 行
    cout << "Line 12: " << rectangle3; // 第 12 行
    rectangle3.print(); // 第 13 行
    cout << endl; // 第 14 行
    rectangle4 = rectangle1 * rectangle2; // 第 15 行
    cout << "Line 16: " << rectangle4; // 第 16 行
    rectangle4.print(); // 第 17 行
    cout << endl; // 第 18 行
    if (rectangle1 == rectangle2) // 第 19 行
        cout << "Line 20: rectangle1 and " // 第 20 行
             << "rectangle2 are equal." << endl;
    else
        cout << "Line 22: rectangle1 and " // 第 22 行
             << "rectangle2 are not equal." << endl;
    if (rectangle1 != rectangle3) // 第 23 行
        cout << "Line 24: rectangle1 and "
             << "rectangle3 are not equal."; // 第 24 行
             << endl;
    else
        cout << "Line 25: rectangle1 and " // 第 25 行
             << "rectangle3 are equal."; // 第 26 行
    return 0;
}
```

# 示例结果:

Line 5: rectangle1: Length = 23; Width = 45
Line 8: rectangle2: Length = 12; Width = 10
Line 12: rectangle3: Length = 35; Width = 55
Line 16: rectangle4: Length = 276; Width = 450
Line 22: rectangle1 and rectangle2 are not equal.
Line 24: rectangle1 and rectangle3 are not equal.

```cpp
{
  locatorType tempRect;
  tempRect.length = firstRect.length + secondRect.length;
  tempRect.width = firstRect.width + secondRect.width;
  return tempRect;
}
```

在上述定义中，将 `firstRect` 和 `secondRect` 对应的成员变量相加，并将结果存储在 `tempRect` 中。记住，类的私有成员对于类是局部的，因此无法在类名之外访问。如果你遵循这条规则，由于 `operator+` 不是 `rectangleType` 类的成员，它作为 `firstRect` 的定义表达式将是非法的，因为 `length` 是 `firstRect` 的私有成员。然而，由于 `operator+` 被声明为 `rectangleType` 类的友（friend），`rectangleType` 类型的对象可以在 `operator+` 的定义中访问其成员。此外注意，在函数处理中，类名（即 `rectangleType`）和作用域解析运算符 `::` 不包含在函数名 `operator+` 之前，因为 `operator+` 不是类的成员。

要将函数 `operator==` 作为 `rectangleType` 类的非成员函数包含，它在 `rectangleType` 定义中的原型如下：

```cpp
friend bool operator==(const rectangleType&,
const rectangleType&);
```

函数 `operator==` 的定义如下：

```cpp
bool operator==(const rectangleType& firstRect, const rectangleType& secondRect) {
    return firstRect.length == secondRect.length &&
         firstRect.width == secondRect.width;
}
```

你可以编写一个与示例 15-4 类似的程序来测试作为非成员的运算符 `+` 和 `==` 的重载。

## 重载流插入 `<<` >> 运算符

对于一个类，重载插入运算符 `<<` 或提取运算符 `>>` 的运算符函数必须是该类的非成员函数，原因如下：

考虑表达式：

```
cout << myRectangle;
```

在这个表达式中，`<<` 的左操作数（即 `cout`）是一个 `ostream` 对象，而不是 `rectangleType` 类型的对象。由于 `<<` 的左操作数不是 `rectangleType` 的对象，因此重载 `rectangleType` 插入运算符的运算符函数必须是 `rectangleType` 类的非成员函数。

同样，重载 `rectangleType` 流提取运算符的运算符函数必须是 `rectangleType` 类的非成员函数。

## 重载流插入运算符 `<<`

下面描述了为类重载流插入运算符 `<<` 的通用语法：

### 函数原型（包含在类定义中）：

```
friend ostream& operator<<(ostream&, const className&);
```

### 函数定义：

```cpp
ostream& operator<<(ostream osObject, const className& cObject) {
    //局部声明（如果有的话）
    // 输出 cObject 的成员。
    //osObject << . ;
    // 返回流对象。
    return osObject;
}
```

在此函数定义中：

- 两个参数都是引用参数。
- 第一个参数（即 `osObject`）是一个 `ostream` 对象的引用。
- 第二个参数通常是某个特定类的 `const` 引用，因为（回想第 12 章）将对象作为参数传递的最有效方法是通过引用。在这种情况下，形式参数不需要复制实际参数的成员变量。在类名之前出现 `const` 单词是因为我们只想打印对象的成员变量。也就是说，函数不应修改对象的成员变量。
- 返回类型是对 `ostream` 对象的引用。

重载运算符 `<<` 的函数的返回类型必须是对 `ostream` 对象的引用，原因如下。

假设运算符 `<<` 已经为 `rectangleType` 类重载了。语句：

```
cout << myRectangle;
```

等同于语句：

```
operator<< (cout, myRectangle);
```

这是一个完全合法的语句，因为因为两个实际参数都是对象，而不是对象的值。第一个参数 `cout` 的类型是 `ostream`；第二个参数 `myRectangle` 的类型是 `rectangleType`。

现在考虑语句：

```
cout << myRectangle;
```

该语句等同于语句：

```
operator<<(operator<<(cout, myRectangle), yourRectangle); //行 A
```

这是因为运算符 `<<` 的结合性是从左到右的。

为了执行上述语句，你必须先执行表达式：

```
cout << myRectangle
```

即表达式：

```
operator<<(cout, myRectangle)
```

在执行完这个表达式（输出了 `myRectangle` 的值）后，无论结果将成为运算符 `<<` 的左侧参数（即函数 `operator<<` 的第一个参数），以便输出对象 `yourRectangle` 的值（见行 A 中的语句）。由于运算符 `<<` 的左侧参数必须是 `ostream` 类型的对象，因此表达式：

```
cout << myRectangle
```

为了输出 `yourRectangle` 的值，必须返回对象 `cout`（不是按值返回）。

因此，函数 `operator<<` 的返回类型必须是对 `ostream` 类型对象的引用。

## 重载流提取运算符 `>>`

接下来描述了为类重载流提取运算符 `>>` 的语法。

### 函数原型（包含在类定义中）：

```
friend ostream& operator>>(ostream&, className);
```

### 函数定义：

```cpp
ostream& operator>>(ostream& object, className& cObject)
{
    // 声明（如果有的话）
    // 读取 cObject 的成员
    // object >> .
    // 返回流对象。
    return object;
}
```
