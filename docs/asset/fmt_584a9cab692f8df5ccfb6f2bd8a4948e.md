
```cpp
    rectangle3 = rectangle1 + rectangle2; // 第 16 行

    cout << "Line 17: rectangle3: "; // 第 17 行

    rectangle3.print(); // 第 18 行

    cout << endl; // 第 19 行

    rectangle4 = rectangle1 * rectangle2; // 第 20 行

    cout << "Line 21: rectangle4: "; // 第 21 行

    rectangle4.print(); // 第 22 行

    cout << endl; // 第 23 行

    if (rectangle1 == rectangle2) { // 第 24 行

        cout << "rectangles are equal" << endl;

    } else {

        cout << "rectangles are not equal" << endl;

    }

    if (rectangle1 != rectangle2) { // 第 28 行

        cout << "rectangles are not equal" << endl;

    } else {

        cout << "rectangles are equal" << endl;

    }

    return 0; // 第 32 行

}
```

示例输出：
```text

Line 10: rectangle1: 23 x 45

Line 13: rectangle2: 12 x 10

Line 17: rectangle3: 35 x 55

Line 21: rectangle4: 276 x 450

rectangles are not equal

```

## 第 13 章：重载与模板

在前面的定义中，添加了 `firstRect` 和 `secondRect` 对应的成员变量，并将结果存储在 `tempRect` 中。记住，类的私有成员对于类是局部，因此不能在类之外访问。如果确实如此，那么 `operator+` 就不是 `rectangleType` 类的成员，像 `firstRect.length` 这样的表达式在它的定义中将是非法的，因为 `length` 是 `firstRect` 的私有成员。然而，由于 `operator+` 被声明为 `rectangleType` 类的友函数，`rectangleType` 类型的对象就可以访问 `operator+` 定义中的私有成员。注意，在函数头中，类名即 `rectangleType` 和作用域解析运算符没有包含在函数名 `operator+` 之前，因为函数 `operator+` 不是类的成员。

要将函数 `operator==` 作为 `rectangleType` 类的非成员包含进来，其在 `rectangleType` 定义中的原型如下：

```cpp
friend bool operator==(const rectangleType&,
                    const rectangleType&);
```

函数 `operator==` 的定义如下：

```cpp
bool operator==(const rectangleType& firstRect,
                    const rectangleType& secondRect)
{
    return (firstRect.length == secondRect.length &&
            firstRect.width == secondRect.width);
}
```

你可以编写一个与示例 13-5 类似的程序，将运算符 `+` 和 `==` 的重载为非成员。

## 重载流插入 `<<` 和提取 `>>` 运算符

如果一个运算符函数是某个类的成员函数，那么 `operator` 的最左侧操作数必须是该类的对象。因此，为一个类重载插入运算符 `<<` 或提取运算符 `>>` 的运算符函数必须是该类的非成员函数。

考虑以下表达式：

```cpp
cout << myRectangle;
```

在这个表达式中，`<<` 的最左侧操作数即 `cout` 是一个 `ostream` 对象，而不是 `rectangleType` 类型。由于 `<<` 的最左侧操作数不是 `rectangleType` 的插入运算符，因此重载 `rectangleType` 插入运算符的运算符函数必须是 `rectangleType` 类的非成员函数。

同样，重载 `rectangleType` 提取运算符的运算符函数也必须是 `rectangleType` 类的非成员函数。

## 重载流插入运算符 `<<`

接下来描述了为类重载流插入运算符 `<<` 的通用语法。

函数原型包含在类的定义中：

```cpp
friend ostream& operator<<(ostream&, const className&);
```

函数定义：

```cpp
ostream& operator<<(ostream osObject, const className& cObject)
{
  //局部声明如果有的话
  // 输出 cObject 的成员变量。
  //osObject << . .
  // 返回流对象。
  return osObject;
}
```

在这个函数定义中：
- 两个参数都是引用参数。
- 第一个参数即 `osObject` 是对一个 `ostream` 对象的引用。
- 第二个参数通常是某个特定类的 `const` 引用，因为回想第 10 章，将对象作为参数传递给类最有效的方法是通过引用。在这种情况下，形式参数不需要拷贝实际参数的成员变量。在类名之前出现 `const` 单词是因为我们只想打印对象的成员变量。也就是说，该函数不应该修改对象的成员变量。
- 函数的返回类型是对 `ostream` 对象的引用。

重载运算符 `<<` 的函数返回类型必须是对 `ostream` 对象的引用，原因如下：

假设 `operator <<` 已为 `rectangleType` 类进行了重载。语句 `cout << myRectangle;` 等同于语句：

```cpp
operator<<(cout, myRectangle);
```

这是一个完全合法的语句，因为两个实际参数都是对象，而不是对象的值。第一个参数 `cout` 的类型为 `ostream`；第二个参数 `myRectangle` 类型为 `rectangleType`。

## 第 13 章：重载与模板

现在考虑以下语句：

```cpp
cout << myRectangle << yourRectangle;
```

该语句等同于语句：

```cpp
operator<<((cout, myRectangle), yourRectangle); //行 A
```

因为运算符 `<<` 的结合性是从左到右的。

为了执行上一个语句，你必须首先执行表达式：

```cpp
cout << myRectangle
```

即表达式：

```cpp
operator<<(cout, myRectangle)
```

在执行完这个表达式它输出了 `myRectangle` 的值后，无论函数 `operator<<` 返回什么，将成为 `operator <<` 的左侧参数即函数 `operator<<` 的第一个参数，以便放入 `yourRectangle` 的值见行 A 中的语句。`operator <<` 的左侧参数必须是一个 `ostream` 类型的对象，因此表达式：

```cpp
cout << myRectangle
```

必须返回对象 `cout`而不是它的值到第二个运算符 `<<` 的左侧，以便输出 `yourRectangle` 的值。

因此，函数 `operator<<` 的返回类型必须是对 `ostream` 类型对象的引用。

## 重载流提取运算符 `>>`

接下来描述了为类重载流提取运算符 `>>` 的通用语法。函数原型包含在类的定义中：

```cpp
friend istream& operator>>(istream&, className&);
```

函数定义：

```cpp
istream& operator>>(istream& isObject, className& cObject)
{
    // 局部声明如果有的话
    // 将数据读入 cObject。
    // isObject >> .
    // 返回流对象。
    return isObject;
}
```

在这个函数定义中：
- 两个参数都是引用参数。
- 第一个参数即 `isObject` 是对一个 `istream` 对象的引用。
- 第二个参数通常是某个类的引用。读入的数据将存储在对象中。
- 函数返回类型是对 `istream` 对象的引用。

由于之前解释的原因当我们重载 `<<` 时，函数 `operator>>` 的返回类型必须是对 `istream` 对象的引用。我们就可以成功地执行如下类型的语句：

```cpp
cin >> myRectangle >> yourRectangle;
```

示例 13-7 显示了如何为类重载流插入和提取运算符。

## 示例 13-7

`rectangleType` 类的定义以及运算符函数的定义如下：

```cpp
#include <iostream>
using namespace std;
class rectangleType {
    // 流插入和提取运算符
    friend ostream& operator<<(ostream&, const rectangleType&);
    friend istream& operator>>(istream&, rectangleType&);
public:
    void setDimension(double l, double w);
    double length() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;
    rectangleType operator+(const rectangleType&) const;
    // 重载运算符 +
    rectangleType operator*(const rectangleType&) const;
    // 重载运算符 *
    bool operator+=(const rectangleType&) const;
    // 重载运算符 =
    bool operator!=(const rectangleType&) const;
    // 重载运算符 !=
    rectangleType();
    rectangleType(double l, double w);
private:
double length;
double width;
};
```

注意我们删除了成员函数 `print`，因为我们正在重载流插入运算符 `<<`。

```cpp
// operator+, operator*,
//operator= 和 operator!= 的定义与示例 13-6 相同。
```

```cpp
ostream& operator<<(ostream& osObject,
const rectangleType& rectangle)
{
    osObject << "Length = " << rectangle.length
    << " Width = " << rectangle.width;
    return osObject;
}
```

```cpp
ostream& operator>>(istream& isObject,
rectangleType& rectangle)
{
    isObject >> rectangle.length >> rectangle.width;
    return isObject;
}
```

考虑以下程序。我们假设 `rectangleType` 类的定义在头文件 `rectangleType.h` 中。

```cpp
// 此程序展示了如何使用修改后的 rectangleType 类。
```

```cpp
cin >> yourRectangle;
cout << endl;
```

```cpp
cout << "Line 12: yourRectangle << " <<
<< yourRectangle << endl;
```

```cpp
cout << "Line 13: myRectangle << " <<
<< myRectangle + yourRectangle << endl;\ncout << "Line 14: myRectangle * yourRectangle: " <<
<< myRectangle * yourRectangle << endl;
```

```cpp
return 0;
```

**示例运行：** 在此示例运行中，用户输入已被标记。

+ Line 8: myRectangle: Length = 23; Width = 45
Line 9: Enter the length and width of a rectangle: 28 17

+ Line 12: yourRectangle: Length = 28; Width = 17
Line 13: myRectangle + yourRectangle: Length = 51; Width = 62
Line 14: myRectangle * yourRectangle: Length = 644; Width = 865

第 6 行和第 7 行的语句声明并初始化了 `myRectangle` 以及 `rectangleType` 类型的对象。第 8 行的语句使用 `cout` 和插入运算符输出了 `myRectangle` 的值。第 10 行的语句使用 `cin` 和提取运算符将数据输入到 `yourRectangle`。第 12 行的语句使用 `cout` 和插入运算符输出了 `yourRectangle` 的值。第 13 行的 `cout` 语句将 `myRectangle` 和 `yourRectangle` 的长度和宽度相加并输出结果。同样，第 14 行的 `cout` 语句将 `myRectangle` 和 `yourRectangle` 的长度和宽度相乘并输出结果。输出显示插入运算符和提取运算符都已成功重载。

## 重载赋值运算符 `=`

类的内置操作之一是赋值操作。赋值运算符会导致类成员变量的逐成员拷贝。例如，该语句：

```cpp
myRectangle = yourRectangle;
```

等同于语句

```cpp
myRectangle.length = yourRectangle.length;
myRectangle.width = yourRectangle.width;
```

回想第 12 章，内置的赋值运算符适用于没有成员变量的类，但对于具有指针成员变量的类则不适用。因此，为了避免带有指针成员的类出现浅拷贝，我们必须显式地重载赋值运算符。

## 922 | 第 13 章：重载与模板

回想，要为类重载赋值运算符 `=`，运算符函数 `operator=` 必须是该类的成员。

为类重载赋值运算符 `=` 的通用语法

接下来描述了为类重载赋值运算符 `=` 的通用语法。

**函数原型**应包含在类的定义中：

```cpp
const className& operator=(const className&);
```

函数定义：

```cpp
const className& className::operator=
    (const className& rightObject)
{
    // 局部声明，如果有的话
    if (this != &rightObject)//避免自我赋值
    {
        // 将 rightObject 拷贝到当前对象的算法
        返回被赋值的对象。
    }
    return *this;
}
```

在函数 `operator=` 的定义中：
- 只有一个形式参数。
- 形式参数通常是某个特定类的 `const` 引用。
- 函数返回类型是某个特定类的 `const` 引用。

现在我们解释为什么函数 `operator=` 的返回类型应该是该类类型的引用。

假设为 `rectangleType` 类重载了赋值运算符 `=`。

语句

```cpp
myRectangle = yourRectangle;
```

等同于语句

```cpp
myRectangle.operator=(yourRectangle);
```

现在考虑该语句：

```cpp
myRectangle = yourRectangle = tempRect;
```

## 运算符重载 | 923

由于运算符 `=` 的结合性是从左到右的，该语句等同于语句

```cpp
myRectangle.operator=(yourRectangle.operator(tempRect)); //行 A
```

显然，我们必须先执行表达式

```cpp
yourRectangle.operator=(tempRect)
```

即表达式

```cpp
yourRectangle = tempRect
```

表达式

```cpp
yourRectangle.operator=(tempRect)
```
