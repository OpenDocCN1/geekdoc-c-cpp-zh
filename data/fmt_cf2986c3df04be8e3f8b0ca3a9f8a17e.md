
```cpp
#include "intarray.h"
#include <cstring>

IntArray::IntArray(size_t size)
{
    d_size(size);
    if (d_size < 1)
        throw "IntArray: size of array must be >= 1";
    d_data = new int[d_size];
}

IntArray::IntArray(IntArray const &other)
{
    d_size(other.d_size),
    d_data(new int[d_size]);
    memcpy(d_data, other.d_data, d_size * sizeof(int));
}

IntArray::~IntArray()
{
    delete [] d_data;
}

IntArray &IntArray::operator=(IntArray const &other)
{
    IntArray tmp(other);
    swap(tmp);
    return *this;
}

int &IntArray::operatorIndex(size_t index) const
{
    boundary(index);
    return d_data[index];
}

int &IntArray::operator[](size_t index)
{
    return operatorIndex(index);
}

int const IntArray::operator[](size_t index) const
{
    return operatorIndex(index);
}

void IntArray::swap(IntArray &other)
{
    // 交换 *this 和 other 的 d_size 和 d_data 数据成员
    std::swap(d_size, other.d_size);
    std::swap(d_data, other.d_data);
}
```

# 第 11 章 更多运算符重载

```cpp
void IntArray::boundary(size_t index) const
{
    if (index < d_size)
        return;
    ostringstream out;
    out << "IntArray: boundary overflow, index < " << index
        << " , should be < " << d_size << "\n";
    throw out.str();
}
```

注意观察`operator[]`方法是如何实现的：非 const 成员函数可以调用 const 成员函数，因为 const 成员函数的实现通常与非 const 成员函数的实现是相同的。因此此`operator[]`可以使用辅助函数`&operatorIndex(size_t index) const`来定义。const 成员函数可以返回指向其对象中某个数据成员的非 const 引用（或指针）。当然，这是一个潜在的危险“后门”，可能会破坏数据隐藏。然而，公共接口中的成员防止了这一点，而且两个公共`operator[]`成员本身调用了同一个`int &operatorIndex() const`成员函数，该函数定义了一个私有的后门。

## 11.1.1 多参数 `operator[]()`

考虑一个标准的二维数组。它有`nRows`和`nCols`。这种数组是一维数组的推广：每一行都由一个包含`nCols`个元素的数组组成。这里有一个类型`DoubleArray`，其定义类似于上一节中的`IntArray`，但包含的是`double`值而不是`int`值，设计一个`Matrix`类可以如下所示：

```cpp
class Matrix
{
    size_t d_nRows;
    size_t d_nCols;
    DoubleArray *d_row;

public:
    Matrix(size_t nRows, size_t nCols);
...
};
```

它的构造函数分配了`nRows`个`DoubleArray`，每个对象都有`nCols`列，每个`DoubleArray`都被初始化为`nCols`个元素，并通过`DoubleArray`的默认构造函数初始化为 0：

```cpp
Matrix::Matrix(size_t nRows, size_t nCols)
    : d_nRows(nRows),
      d_nCols(nCols),
      d_row(new DoubleArray[nRows]) {}
```

传统上，访问`Matrix`的元素可以通过三种方式实现（以及可选对应的 const 变体）：

## 11.2 重载插入和提取运算符

- 一个成员函数`double&element(size_t row, size_t col)`，返回`double [row, col]`的值；

- 一个成员函数`DoubleArray&row(size_t row)`，返回该行的数据；

- 一个成员函数`DoubleArray&operator[](size_t row)`，同样返回`DoubleArray`；

`element`和`row`成员虽然可以工作，但缺点是没有使用引用矩阵元素的语法。例如，为了访问`matrix[3, 4]`，我们需要写成`matrix.element(3, 4)`或`matrix.row(3)[4]`，其中第三个元素允许我们使用两个索引运算符：`matrix[3][4]`。此外，如果这些成员的唯一目的是访问`Matrix`元素，那么`DoubleArray&row`的第二个和第三个成员的数据隐藏就会被弃用。

然而，重载的索引运算符`operator[]`也可以定义为接受多个参数，从而允许使用（标准的）数学语法`matrix[row, col]`（通常情况下：重载的索引运算符也可以有更多参数，这在定义例如数组数组时非常有用）。

提供一个接受两个参数的索引运算符非常简单：只需在类的接口中添加一个成员函数`double&operator[](size_t row, size_t col)`（可选一个可比较的 const 成员）即可。它的实现可以直接返回请求的数组元素：

```cpp
double Matrix::operator[](size_t row, size_t col)
{
    return d_row[row][col];
}
```

需要注意的是：该实现没有检查提供的索引是否有效。传统上，索引运算符不执行此类检查，以便在已知索引可能无效时提高程序的效率。例如，为了用随后的整数值初始化`Matrix`的所有元素，可以使用如下函数：

```cpp
void init(Matrix &matrix, size_t size_value)
{
    for (size_t row = 0; row != matrix.rows(); ++row)
        for (size_t col = 0; col != matrix.nCols(); ++col)
            matrix[row, col] = size_value;
}
```

另一方面，如果需要检查索引的有效性，则可以定义如下多参数成员函数：

```cpp
double Matrix&::at(size_t row, size_t col)
{
    if (row >= d_nrows || col >= d_nCols)
        throw runtime_error("Matrix::at: invalid indices");
    return d_row[row][col];
}
```

## 11.2 重载插入和提取运算符

类可以被调整，使其对象可以分别被插入到`std::ostream`和从`std::istream`中提取。

`std::ostream`定义了针对基本类型（如`int`、`char *`等）的插入运算符。在本节中，我们将学习如何扩展类的功能（特别是`std::istream`和`std::ostream`），以便它们与后续开发的类结合使用。

特别是，我们将展示如何重载插入运算符，允许将任何类型的对象（例如`Person`，见第9章）插入到`ostream`中。（注：原文此处存在大量重复的段落，翻译时已按要求进行去重处理并保留核心逻辑）。

等等，注意这里遵循了步进的方法。一个简单的实现如下：

```cpp
istream &operator>>(istream &in, Person &person)
{
    string name;
    string address;
    string phone;

    if (in >> name >> address >> phone) // 提取三个字符串
    {
        person.setName(name.c_str());
        person.setAddress(address.c_str());
        person.setPhone(phone.c_str());
    }
    return in;
}
```

## 11.3 转换运算符

类可以围绕内置类型构建。例如，一个围绕`char *`类型构建的`String`类。这种类可以定义各种操作，如赋值。查看下面模仿`string`类设计的类接口：

```cpp
class String
{
    char *d_string;

public:
    String();
    String(char *arg);
    ~String();
    String(String const &other);
    String &operator=(String const *value);
    String &operator=(char const *value);
}
```

该类的对象可以从`char *`初始化，也可以从`String`自身初始化。存在一个重载运算符，允许从`String`对象和`char const *`进行赋值。

通常，在与数据比这个`String`类更直接相关的情况下，会有一个访问成员函数，例如成员函数`char *String::c_str() const`。当`String`对象数组由（例如）`StringArray`类定义时，使用后者的需求并不符合我们的直觉。该类提供了`operator[]`来访问单个`String`成员，它最可能在如下类接口提供的最少：

> ¹注意从`char const *`赋值也允许空指针。像`stringObject = 0`这样的赋值是完全正常的。

```cpp
class StringArray
{
    String *d_store;
    size_t d_n;

public:
    StringArray(size_t size);
    StringArray(StringArray const &other);
    StringArray &operator=(StringArray const &rvalue);
    ~StringArray();

    String &operator[](size_t index);
};
```

此接口允许我们将`String`元素进行相互赋值：

```cpp
StringArray sa{ 10 };
s[4] = sa[3]; // String 之间的赋值
```

但也可以将`char const *`赋值给 sa 的元素：

```cpp
sa[3] = "hello world";
```

在这里，执行了以下步骤：

- 首先，求值`sa[3]`。

- 接下来，检查`String`类是否有重载的赋值运算符，期望右侧为`char const *`。找到了该运算符，字符串对象`sa[3]`接收了它的新值。

现在我们尝试另一种方法：如何访问存储在`sa[3]`中的`char const *`？以下尝试失败了：

```cpp
char const *cp = sa[3];
```

它失败了，因为我们需要为 `char const *` 提供一个重载的赋值运算符。遗憾的是，并没有这样的类，因此无法构建该重载的赋值运算符（参见 11.15）。此外，类型转换不起作用，因为编译器不知道如何将`String`转换为`char const *`。该如何继续？

一种可能性是定义一个成员函数`c_str()`：

```cpp
char const *cp = sa[3].c_str();
```

这可以编译通过，但看起来很笨拙……一个更好的方法是使用转换运算符。转换运算符是重载运算符的一种，但这次重载被用于将对象转换为另一种类型。在类中，转换运算符的通用形式为：

```cpp
operator <type>() const;
```

## 11.3. 转换运算符

转换运算符通常是`const`成员函数；当它们的对象在具有类型值的表达式中使用时，会被自动调用。通过使用转换运算符，`String`对象可以被解释为`char const *`值，允许我们执行上述赋值。

转换运算符是有一定危险的。转换是由编译器自动执行的，除非它是完全透明的，否则可能会困扰阅读使用了转换运算符代码的人员。例如，C++ 程序员经常对像`if (cin) ...`这样的语句感到困惑。

根据经验法则：类最多最多应有一个转换运算符。可以定义多个转换运算符，但通常会导致歧义。例如，如果一个类定义了`operator bool()`和`operator int() const`，那么将此类的对象传递给一个期望`size_t`参数的函数会导致歧义，因为`int`和`bool`都可以用于初始化`size_t`。

在当前的示例中，`String`类可以为`char const *`定义如下转换运算符：

```cpp
String::operator char const *() const
{
    return d_string;
}
```

注意：

- 转换运算符不定义返回值。转换运算符返回`operator`关键字之后指定的类型的值。

```cpp
std::ostream& operator<<(std::ostream &out, std::string const &str)
{
    return out.write(str.data(), str.length());
}
```

当定义转换运算符的类对象被插入流中时，也会使用转换运算符。注意，转换运算符的右侧插入的是函数参数，规则是：

- 如果定义转换运算符的类`x`也定义了接受`X`对象的插入运算符，则使用该插入运算符；

在下面的示例中，`Insertable`类对象被直接插入；`Converter`类对象使用转换运算符；`Error`类对象无法插入，因为它没有定义插入运算符，且其转换运算符的类型无法被插入（`Text`虽然定义了`operator int() const`，但`Text`本身无法被插入导致了错误）：

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Insertable {
    operator int() const {
        cout << "op int()\n";
        return 0;
    }
};

ostream &operator<<(ostream &out, Insertable const &ins) {
    return out << "insertion operator";
}

struct Converter {
    operator Insertable() const {
        return Insertable();
    }
};

struct Text {
    operator int() const {
        return 1;
    }
};

struct Error {
    operator Text() const {
        return Text();
    }
};

int main() {
    Insertable insertable;
    cout << insertable << '\n';
    Converter convertor;
    cout << convertor << '\n';
    Error error;
    // cout << error << '\n'; // This would fail because Text has no insertion operator
}
```

关于转换运算符的最后几点说明：

## 11.4. `BYTE` 类型的另一种实现

- 转换运算符应该是对象功能的“自然扩展”。例如，流类定义了`bool()`，允许了诸如`if (cin)`这样的构造。

- 转换运算符通常返回一个值，以强制数据隐藏，因为这是转换运算符的意图用法。将转换运算符定义为别名（例如定义一个`operator int()`转换运算符）会打开一个后门，且该运算符只有在显式转换时才能作为值使用。

- 转换运算符通常是`const`成员函数；当它们的对象在具有类型值的表达式中使用时，会被自动调用。使用转换运算符`String`对象可以被解释为`char const *`值，允许我们执行上述赋值。

## 11.4. `BYTE` 类型的另一种实现（继续）

运算符重载
