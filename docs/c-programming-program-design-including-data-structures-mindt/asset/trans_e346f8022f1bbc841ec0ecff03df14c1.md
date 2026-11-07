
现在考虑以下语句：

```cpp
cout << myRectangle << yourRectangle;
```

该语句等价于以下语句：

```cpp
operator<<(operator<<(cout, myRectangle), yourRectangle); //line A
```

因为运算符 `<<` 的结合性是从左到右。

要执行前一条语句，必须首先执行表达式

```cpp
cout << myRectangle
```

也就是表达式

```cpp
operator<<(cout, myRectangle)
```

执行该表达式（它输出 `myRectangle` 的值）后，函数 `operator<<` 返回的任何内容都将成为运算符 `<<` 的左侧参数（即函数 `operator<<` 的第一个参数），以便输出对象 `yourRectangle` 的值（参见 A 行中的语句）。运算符 `<<` 的左侧参数必须是 `ostream` 类型的对象，因此表达式

```cpp
cout << myRectangle
```

必须将对象 `cout`（而不是其值）返回到第二个运算符 `<<` 的左侧，以便输出 `yourRectangle` 的值。

因此，函数 `operator<<` 的返回类型必须是对 `ostream` 类型对象的引用。

## 重载流提取运算符（>>）

下面描述为某个类重载流提取运算符 `>>` 的一般语法。**函数原型**（应包含在类的定义中）：

```cpp
friend istream& operator>>(istream&, className&);
```

### 函数定义：

```cpp
istream& operator>>(istream& isObject, className& cObject)
{
    //local declaration, if any
    //Read the data into cObject.
    //isObject >> ...

    //Return the stream object.
    return isObject;
}
```

在这个函数定义中：

- 两个参数都是引用参数。
- 第一个参数——即 `isObject`——是对 `istream` 对象的引用。
- 第二个参数通常是对特定类的引用。读取的数据将存储在该对象中。
- 函数返回类型是对 `istream` 对象的引用。

出于前面解释过的相同原因（当我们重载插入运算符 `<<` 时），函数 `operator>>` 的返回类型必须是对 `istream` 对象的引用。这样我们就能成功执行以下类型的语句：

```cpp
cin >> myRectangle >> yourRectangle;
```

例 13-7 展示了如何为 `class rectangleType` 重载流插入和提取运算符。

### 例 13-7

`class rectangleType` 的定义以及运算符函数的定义如下：

```cpp
#include <iostream>

using namespace std;

class rectangleType
{
    //Overload the stream insertion and extraction operators
    friend ostream& operator<< (ostream&, const rectangleType &);
    friend istream& operator>> (istream&, rectangleType &);

public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;

    rectangleType operator+(const rectangleType&) const;
    //Overload the operator +
    rectangleType operator*(const rectangleType&) const;
    //Overload the operator *

    bool operator==(const rectangleType&) const;
    //Overload the operator ==
};
```

```cpp
cin >> yourRectangle;
cout << endl;

cout << "Line 12: yourRectangle: "
     << yourRectangle << endl;

cout << "Line 13: myRectangle + yourRectangle: "
     << myRectangle + yourRectangle << endl;
cout << "Line 14: myRectangle * yourRectangle: "
     << myRectangle * yourRectangle << endl;

return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```text
Line 8: myRectangle: Length = 23; Width = 45
Line 9: Enter the length and width of a rectangle: 28 17

Line 12: yourRectangle: Length = 28; Width = 17
Line 13: myRectangle + yourRectangle: Length = 51; Width = 62
Line 14: myRectangle * yourRectangle: Length = 644; Width = 765
```

第 6 行和第 7 行中的语句声明并初始化 `myRectangle` 和 `yourRectangle`，使其成为 `rectangleType` 类型的对象。第 8 行中的语句使用 `cout` 和插入运算符输出 `myRectangle` 的值。第 10 行中的语句使用 `cin` 和提取运算符将数据输入到 `yourRectangle` 中。第 12 行中的语句使用 `cout` 和插入运算符输出 `yourRectangle` 的值。第 13 行中的 `cout` 语句将 `myRectangle` 和 `yourRectangle` 的长度与宽度相加并输出结果。类似地，第 14 行中的 `cout` 语句将 `myRectangle` 和 `yourRectangle` 的长度与宽度相乘并输出结果。输出表明，流插入运算符和流提取运算符都已被成功重载。

### 重载赋值运算符（=）

类上的内置操作之一是赋值操作。赋值运算符会逐成员复制类的成员变量。例如，语句

```cpp
myRectangle = yourRectangle;
```

等价于以下语句：

```cpp
myRectangle.length = yourRectangle.length;
myRectangle.width = yourRectangle.width;
```

回顾第 12 章可知，内置赋值运算符适用于没有指针成员变量的类，但不适用于有指针成员变量的类。因此，为了避免对带有指针成员变量的类进行数据浅拷贝，我们必须显式重载赋值运算符。

回顾一下，要为某个类重载赋值运算符 `=`，运算符函数 `operator=` 必须是该类的成员。

### 为类重载赋值运算符 `=` 的一般语法

下面描述为某个类重载赋值运算符 `=` 的一般语法。

**函数原型**（应包含在类的定义中）：

```cpp
const className& operator=(const className&);
```

### 函数定义：

```cpp
const className& className::operator=
                    (const className& rightObject)
{
    //local declaration, if any

    if (this != &rightObject)//avoid self-assignment
    {
        //algorithm to copy rightObject into this object
    }

        //Return the object assigned.
    return *this;
}
```

在函数 `operator=` 的定义中：

- 只有一个形参。
- 形参通常是对特定类的 `const` 引用。
- 函数返回类型是对特定类的 `const` 引用。

现在我们解释为什么函数 `operator=` 的返回类型应该是类类型的引用。

假设已经为类 `rectangleType` 重载了赋值运算符 `=`。

语句

```cpp
myRectangle = yourRectangle;
```

等价于语句

```cpp
myRectangle.operator=(yourRectangle);
```

也就是说，对象 `yourRectangle` 成为函数 `operator=` 的实参。

现在考虑以下语句：

```cpp
myRectangle = yourRectangle = tempRect;
```

## 复杂数据的混合效应模型

Richard A. Berk

> “对广泛应用的混合效应模型进行了深刻而透彻的论述。”

本书全面介绍混合效应模型，强调实际数据分析与解释。内容涵盖线性、广义线性和非线性混合效应模型，并详细讨论估计、推断和模型检验。

- 理论与应用的均衡处理
- 来自生态学、医学和社会科学的示例
- 强调模型诊断与解释

![](img/b217c421655b51e7494cf3b89bb5432d_986_0.png)

| 章节 | 主题 | 页码 |
|---------|-------|-------|
| 1       | 引言 | 1–15 |
| 2       | 线性混合模型 | 16–42 |
| 3       | 广义线性混合模型 | 43–70 |

```r
library(lme4)
model <- lmer(Reaction ~ Days + (1 | Subject), data = sleepstudy)
summary(model)
```

