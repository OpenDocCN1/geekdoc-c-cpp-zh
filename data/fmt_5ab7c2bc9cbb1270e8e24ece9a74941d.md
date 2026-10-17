
`myCell.setValue(6);`

// 然而，这一行将无法编译。

`cout << "cell 1: *" << myCell.getValue() << endl;`

```
不幸的是，尝试调用默认构造函数的这一行会编译。但下一行将无法编译。问题在于，你的编译器认为第一行实际上是一个名为 `myCell`、不接受任何参数并返回 `Spreadsheet` 对象的函数声明。当它处理到第二行时，它认为你正试图将一个函数名当作对象来使用！

> 警告 在栈上创建对象时，请省略默认构造函数的括号。
```

对于堆上的对象分配，可以使用如下方式默认构造函数：

```
auto smartCell = make_unique<SpreadsheetCell>();

// 使用裸指针（不推荐）

SpreadsheetCell* myCell = new SpreadsheetCell();

// 或者

SpreadsheetCell* myCell = new SpreadsheetCell;

// ... 使用 myCell

delete myCell; myCell = nullptr;
```

## 编译器生成的默认构造函数

本章第一个 `SpreadsheetCell` 类定义如下：

```
class SpreadsheetCell
{
    public:
        void setValue(double inValue);
        double getValue() const;
    private:
        double mValue;
};
```

此定义没有声明默认构造函数，但代码仍然可以完美运行。

```
SpreadsheetCell myCell;
myCell.setValue(6);
```

以下定义与之前的定义相同，但它添加了一个接受 `double` 的显式构造函数。它仍然没有显式声明默认构造函数。

```cpp
class SpreadsheetCell
{
    public:
        SpreadsheetCell(double initialValue); // 没有默认构造函数
        // 为了简单起见，省略类定义的其余部分
};
```

（注：由于提供的原始文本后半部分存在大量重复的乱码/重复内容，已根据要求提取核心逻辑并完成翻译。）

构造函数的实现如下：

```
SpreadsheetCell::SpreadsheetCell(double d) { }
```

该类仅有一个接受 `double` 的显式构造函数，并且不包含默认构造函数。你可以如下将其作为另一个类的数据成员使用：

```cpp
class SomeClass {
    public:
        SomeClass();
    private:
        SpreadsheetCell mCell;
};
```

并如下实现 `SomeClass` 构造函数：

```
SomeClass::SomeClass() { }
```

然而，使用这种实现，代码将无法编译。编译器不知道如何初始化 `SomeClass` 的 `mCell` 数据成员，因为它没有默认构造函数。

解决方案是使用构造初始化列表（ctor-initializer）来初始化 `mCell` 数据成员，如下：

```
SomeClass::SomeClass() : mCell(1.0) { }
```

> 注意：构造初始化列表允许在创建数据成员时对其初始化。

有些程序员倾向于在构造函数体中赋值初始值。然而，某些数据类型必须在构造初始化列表中初始化。下表总结了这些类型：

| 数据类型 | 解释 |
| --- | --- |
| const 数据成员 | 你无法在创建后合法地为其赋值。任何值必须在创建时提供。 |
| 引用数据成员 | 引用必须指向某些东西。 |
| 没有默认构造函数的对象成员 | C++ 尝试使用默认构造函数初始化对象。如果不存在默认构造函数，则无法初始化。 |
| 没有默认构造函数的基类 | [见第 9 章] |

构造初始化列表有一个重要的注意事项：它们按照数据成员在类定义中出现的顺序进行初始化，而不是按照构造初始化列表中的顺序。参考以下 `SpreadsheetCell` 类的定义：

```cpp
class SpreadsheetCell{
public:
    // 代码省略
private:
    // 代码省略
    double mValue;
    std::string mString;
};
```

假设你这样编写 `SpreadsheetCell` 构造函数以使用初始化列表：

```
SpreadsheetCell::SpreadsheetCell(const string& initialValue) :
mString(initialValue), mValue(stringToDouble(mString)) // 顺序错误！
```

代码可以编译（尽管某些编译器会发出警告），但程序运行并不正确。你可能认为因为 `mString` 在初始化列表中第一个出现，所以它会先于 `mValue` 初始化。但 C++ 并不是那样工作的。类声明 `mValue` 在 `mString` 之前；因此初始化列表尝试先初始化 `mValue`。然而，初始化 `mValue` 的代码尝试使用 `mString`，而它尚未初始化！这里的解决方案是在初始化 `mValue` 时使用 `initialValue` 而不是 `mString`。你应该交换初始化列表中的顺序：

```cpp
SpreadsheetCell::SpreadsheetCell(const string&initialValue) :
mValue(stringToDouble(initialValue)), mString(initialValue);
```

> 警告：初始化列表按照类定义的顺序初始化数据成员，而不是初始化列表中的顺序。

## 拷贝构造函数

C++ 中有一种特殊的构造称为拷贝构造函数，允许你创建一个对象的拷贝。如果你不写拷贝构造函数，C++ 会为你生成一个，通过源对象的对应数据成员来初始化新对象的每个成员。对于对象成员，这意味着它们的构造函数会被调用。以下是 `SpreadsheetCell` 类中拷贝构造函数的声明：

```cpp
class SpreadsheetCell
{
public:
    SpreadsheetCell(const SpreadsheetCell& src);
    // 类定义的其余部分省略
};
```

拷贝构造函数接收源对象的常量引用。在构造函数内部，你应该从源对象拷贝所有字段。技术上讲，你可以在构造函数中做任何你想做的事，但通常的做法是将新对象初始化为旧对象的拷贝。以下是 `SpreadsheetCell` 构造函数的示例实现：

```cpp
SpreadsheetCell::SpreadsheetCell(const SpreadsheetCell& src) :
mValue(src.mValue), mString(src.mString)
{}
```

注意初始化列表的使用。

> 注意：给定一组成员变量 m1, m2, ... mn，编译器生成的拷贝构造函数可以表示为：
> 
> `classname(const className& src) : m1(src.m1), m2(src.mn) { }`

因此，在许多情况下，你不需要自己指定拷贝构造函数。但在某些情况下，这种默认构造函数是不够的。这些情况在第 8 章中会有。

### 拷贝构造函数的调用

C++ 中传递参数的默认语义是值传递。这意味着函数或方法接收值或对象的拷贝。因此，每当你将对象传递给函数或方法时，编译器都会调用新对象的拷贝构造函数来初始化它。例如，假设 `SpreadsheetCell` 类中的 `setString()` 方法如下：

```cpp
void SpreadsheetCell::setString(string inString)
{
mString = inString;
mValue = stringToDouble(mString);
}
```

记住 C++ 的 `string` 实际上是一个类，而不是内置类型。当你传递字符串参数调用 `setString()` 时，`inString` 通过其拷贝构造函数初始化。在下面的示例中，为 `inString` 执行了拷贝构造函数。

```cpp
SpreadsheetCell myCell;
string name = "heading one";
myCell.setString(name); // 拷贝 name
```

当 `setString()` 方法结束时，`inString` 被销毁。因为它只是 `name` 的拷贝，所以 `name` 保持不变。

当从函数或方法返回对象时，也会调用拷贝构造函数。在这种情况下，编译器通过其拷贝构造函数创建一个临时对象。第 25 章详细探讨了临时对象的影响。你可以像本章通过通过常量引用传递参数来避免拷贝构造函数的开销。

### 显式调用拷贝构造函数

你也可以显式地使用拷贝构造函数。将一个对象构造为另一个对象的拷贝通常很有用。例如，你可能想创建一个 `SpreadsheetCell` 对象的拷贝：

```cpp
SpreadsheetCell myCell2(4);
SpreadsheetCell myCell3(myCell2); // myCell3 的值与 myCell2 相同
```

### 引用传递对象

为了在获取对象引用时避免拷贝，你可以声明函数或方法接收它的引用。引用传递通常比值传递更高效，因为只拷贝了对象的地址，而不是对象的全部内容。此外，引用传递避免了对象中的动态内存分配问题，这在第 8 章中讨论过。

当你通过引用传递对象时，使用引用的函数或方法可能会更改原始对象。当你仅为了效率使用引用时，可以通过将对象声明为 `const` 来排除这种可能性。这被称为常量引用传递对象，之前所有的代码示例都已这样做。例如，`SpreadsheetCell` 类中需要字符串的方法被声明为常量字符串引用参数。如果你不带引用参数声明方法，类定义将如下：

```cpp
class SpreadsheetCell
{
public:
    SpreadsheetCell();
    SpreadsheetCell(double initialValue);
    SpreadsheetCell(const SpreadsheetCell& src);
    void setValue(double inValue);
    double getValue() const;
    void setString(std::string inString) const;
    std::string getString() const;
private:
    std::string doubleToString(double inValue) const;
    double stringToDouble(std::string inString) const;
};
```

```cpp
double maxValue;
std::string mString;
};
```

这里是 `setString()` 的实现。请注意该方法保持不变，仅参数类型不同。

```cpp
void SpreadsheetCell::setString(string inString)
{
    mString = inString;
    maxValue = stringToDouble(mString);
}
```

> 注意：出于性能考虑，最好通过 `const` 引用传递对象而不是值。

`SpreadsheetCell` 类的 `doubleToString()` 方法始终按值返回字符串，因为该方法的实现在方法结束时创建了一个局部字符串对象并返回给调用者。返回该字符串的引用是不可行的，因为引用的字符串在函数退出时会被销。

### 显式默认和删除拷贝构造函数

你可以按照如下方式显式地默认或删除编译器生成的拷贝构造函数：

```cpp
SpreadsheetCell(const SpreadsheetCell& src) = default;
```

或者

```cpp
SpreadsheetCell(const SpreadsheetCell& src) = delete;
```

### 初始化列表构造函数

初始化列表构造函数是以 `std::initializer_list<T>` 作为第一个参数的构造函数，且没有任何额外参数，或者参数具有默认值。在使用 `std::initializer_list<T>` 模板之前，你需要包含 `<initializer_list>` 头文件。下面的类演示了它的用法。

```cpp
class EvenSequence {
    public:
    EvenSequence(initializer_list<double> args) {
        if (args.size() % 2 != 0) {
            throw invalid_argument("initializer_list should \"contain even number of elements.");
        }
        mSequence.reserve(args.size());
    }
```

```cpp
for (auto value : args) {
    mSequence.push_back(value);
}
void dump() const {
    for (auto value : mSequence) {
        cout << value << ",";
    }
}
```

在初始化列表构造函数内部，你可以使用基于范围的循环（range-based loop）访问初始化列表的元素。你可以通过 `size()` 方法获取初始化列表中的元素数量。

`Even` 初始化列表构造函数使用基于范围循环从给定的 `initializer_list` 拷贝元素。建议尽可能使用 STL 算法。STL 算法在第 17 章中进行了详细讨论。之前带有 `push_back()` 的基于范围循环可以用如下 STL 算法重写：

```cpp
mSequence.insert(insert(mSequence), cbegin(args), cend(args));
```

`EvenSequence` 对象的构造可以如下所示进行：

```cpp
EvenSequence p1 = (1.0, 2.0, 3.0, 4.0, 5.0, 6.0);
p1.dump();
try {
    EvenSequence p2 = (1.0, 2.0, 3.0);
} catch (const invalid_argument& e) {
    cout << e.what() << endl;
}
```

`p2` 的构造将抛出一个异常，因为它的初始化列表中的元素个数是奇数。前面的等号是可选的，可以省略，例如：

```cpp
EvenSequence p1(1.0, 2.0, 3.0, 4.0, 5.0, 6.0);
```

STL 对初始化列表构造函数有完全支持。例如，`std::vector` 容器可以使用初始化列表进行初始化：

```cpp
std::vector<std::string> myVec = {"String 1", "String 2", "String 3"};
```

如果没有初始化列表构造函数，初始化 vector 的一种方法是多次调用 `push_back()`：

```cpp
std::vector<std::string> myVec;
myVec.push_back("String 1");
myVec.push_back("String 2");
myVec.push_back("String 3");
```

初始化列表不仅限于构造函数，还可以用于普通函数，如第 10 章所解释的那样。

### 类内成员初始化器

从 C++11 开始，成员变量可以直接在类定义中初始化。例如：

```cpp
#include <string>
class MyClass
{
    private:
    int mInt = 1;
    std::string mstr = "test";
}
```

在 C++11 之前，初始化 `mint` 和 `mstr` 的唯一方法是在构造函数体内部，使用如下的 C 初始化列表：

```cpp
#include <string>
class MyClass
{
    public:
    MyClass() : mint(1), mstr("test") {}
    private:
    int mint;
    std::string mstr;
}
```

在 C++11 之前，只有 `static const` 成员变量可以在类定义中初始化。例如：

```cpp
#include <string>
class MyClass
{
    private:
    static const int kII = 1; // OK
    static const std::string kStr = "test"; // Error: 不是整数类型
    static int si2 = 2; // Error: 不是 const
    const int ki3 = 3; // Error: 不是 static
}
```

### 委托构造函数

委托构造函数允许构造函数调用同一类中的另一个构造函数。然而，此调用不能放在构造函数体中；它必须置于构造函数初始化列表中，并且必须是列表中唯一的成员初始化。以下是一个示例：
