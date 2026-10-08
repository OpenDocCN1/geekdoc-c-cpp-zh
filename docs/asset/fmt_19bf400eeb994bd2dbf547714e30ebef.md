
```cpp
public:
    void foo(int i);
    void foo(double d) = delete;
};
```

通过此更改，尝试用 `double` 调用 `foo()` 将被编译器标记为错误，而不是执行到整数的转换。

## 默认参数

C++ 中一个与方法重载相似的特性是默认参数。你可以在原型中为函数和方法的参数指定默认值。如果用户使用了这些参数，则忽略默认值；如果用户省略了这些参数，则将使用默认值。然而，这里有一个限制：你只能为从右侧开始的连续参数列表提供默认值。否则，编译器将无法将缺失的参数与默认参数匹配。默认参数可以使用函数、方法和构造函数。例如，你可以在 `Spreadsheet` 构造函数中为 `width` 和 `height` 分配默认值：

```cpp
class Spreadsheet {
public:
  Spreadsheet(const SpreadsheetApplication& theApp,
  int inWidth = kMaxWidth, int inHeight = kMaxHeight // 为了省略省略了部分
};
```

`Spreadsheet` 构造函数的实现保持不变。注意你只在方法声明中指定了默认参数，而没有在定义中指定。

现在你可以用一个、两个或三个参数来调用 `Spreadsheet` 构造函数，尽管只有一个非拷贝构造函数：

```cpp
SpreadsheetApplication theApp;
Spreadsheet s1(theApp);
Spreadsheet s2(theApp, 5);
Spreadsheet s3(theApp, 5, 6);
```

一个带有所有参数的构造函数可以充当默认构造函数。这意味着你可以在不指定任何参数的情况下构造该类的对象。如果你想声明一个默认构造函数和一个多参数构造函数……

注意，你可以在任何地方引用 `SpreadsheetCell`，只要在 `Spreadsheet` 类之外，就必须使用作用域解析符来限定。

`Spreadsheet::` 范围。这甚至适用于方法定义。例如，默认构造函数现在看起来像这样：

这种语法会迅速变得笨拙。对于 `SpreadsheetCell` 赋值运算符的定义，现在看起来像这样：

```cpp
Spreadsheet::SpreadsheetCell& Spreadsheet::SpreadsheetCell::operator=(
	const SpreadsheetCell& rhs)
{
	if (this == &rhs) {
		return *this;
	}
	mValue = rhs.mValue;
	mString = rhs.mString;
	numAccesses = rhs.mNumAccesses;
	return *this;
}
```

事实上，你甚至必须为 `Spreadsheet` 类本身方法的返回类型（而不是参数）使用这种语法：

```cpp
Spreadsheet::SpreadsheetCell& Spreadsheet::getCell(int x, int y)
{
	if (!inRange(x, mwidth) || !inRange(y, mHeight)) {
		throw std::out_of_range("...");
	}
	return mCells[x][y];
}
```

你可以通过使用类型别名将 `Spreadsheet::SpreadsheetCell` 重命名为易于管理的 `SCell`，来避免这种笨拙的语法：

```cpp
using SCell = Spreadsheet::SpreadsheetCell;
```

此类型别名应该放在 `Spreadsheet` 类定义之外，否则你必须用 `Spreadsheet::` 对类型别名本身进行限定以得到 `Spreadsheet::SCell`。那对你没什么好处！

现在你可以这样写默认构造函数：

```cpp
SCell::SpreadsheetCell() : mValue(0)
{}
```

普通的访问控制适用于嵌套类定义。如果你声明了一个私有的 `private` 或保护的 `protected` 嵌套类，你只能在外部类内部使用它。

通常你应该只对简单的类使用类定义。对于像 `SpreadsheetCell` 类这样的东西，真的太笨拙了。

## 类内部的枚举类型

如果你想在类内部定义常量，应该使用枚举类型，而不是一组 `#Defines`。例如，你可以按照如下方式为 `SpreadsheetCell` 类添加单元格颜色支持：

```cpp
class SpreadsheetCell
{
    public:
    // 为了简洁起见已省略
    enum class Colors { Red = 1, Green, Blue, Yellow };
    void setColor(Colors color);
    private:
    // 为了简洁起见已省略
    Colors mColor = Colors::Red;
};
```

`setColor()` 方法的实现非常直接：

```cpp
void SpreadsheetCell::setColor(Colors color)
{
    mColor = color;
}
```

新方法可以这样使用：

```cpp
SpreadsheetCell myCell(5);
myCell.setColor(SpreadsheetCell::Colors::Blue);
```

使用枚举类型是首选方案，而不是像下面这样使用 `#define`：

```cpp
#define SPREADSHEETCELL_RED 1
#define SPREADSHEETCELL_GREEN 2
#define SPREADSHEETCELL_BLUE 3
#define SPREADSHEETCELL_YELLOW 4
class SpreadsheetCell
{
    public:
    // 为了简洁起见已省略
    void setColor(int color);
    private:
    // 为了简洁起见已省略
    int mColor;
};
```

当你使用 `#define` 时，你必须为 `setColor()` 函数使用整数参数，而不是像 `Colors` 枚举类型那样清晰的类型。

## 友元（FRIENDS）

C++ 允许类声明其他类（或其他类的成员函数）、非成员函数为友元，友元可以访问保护和私有的数据成员以及方法。例如，`SpreadsheetCell` 类可以这样指定 `Spreadsheet` 类为它的“朋友”：

```cpp
class SpreadsheetCell
{
  public:
    friend class Spreadsheet;
    // 类的其余部分为了起见已省略
};
```

现在，`Spreadsheet` 类的所有方法都可以访问 `Spreadsheet` 类的私有和保护数据成员及方法。
如果你只想让 `Spreadsheet` 类的特定成员函数成为友元，可以如下操作：

```cpp
class SpreadsheetCell
{
  public:
    friend void Spreadsheet::getCell(int x, int y,
        const SpreadsheetCell& cell);
    // 类的其余部分为了起见已省略
};
```

注意，类知道哪些其他类、方法或函数想要成为它的友元；类、方法或函数不能声明自己是某些其他类的友元，并访问该类的非公开名称。

你可能想写一个函数来验证 `SpreadsheetCell` 对象的字符串是否为空。你可能希望这个验证例程位于 `SpreadsheetCell` 类之外以模拟外部审计，但该函数应该能够访问对象的内部数据成员以进行正确检查。这里是带有友元函数 `checkSpreadsheetCell()` 的 `SpreadsheetCell` 类定义：

```cpp
class SpreadsheetCell
{
  public:
    friend bool checkSpreadsheetCell(const SpreadsheetCell& cell);
    // 为了起见已省略
};
```

类中的友元声明作为函数的原型。不需要在其他地方编写原型（尽管这样做是无害的）。这里是函数的定义：

```cpp
bool checkSpreadsheetCell(const SpreadsheetCell& cell)
{
  return !(cell.mString.empty());
}
```

编写这个函数就像编写其他函数一样，只是你可以直接访问私有的或保护的成员。在函数定义处不需要重复 `friend` 关键字。

友元类和方法很容易滥用；它们允许违反封装原则。

## 第 8 章掌握类与对象

你可以这样使用 `add()` 方法：

```cpp
SpreadsheetCell myCell(4), anotherCell(5);
SpreadsheetCell aThirdCell = myCell.add(anotherCell);
```

这种方法可行，但有点笨拙。你可以做得更好。

### 第二次尝试：作为方法的运算符+

如果能像处理整数或双点数那样方便地相两个类，例如：

```cpp
SpreadsheetCell myCell(4), anotherCell(5);
SpreadsheetCell aThirdCell = myCell + anotherCell;
```

C++ 允许你编写自己的加号版本（称为加法运算符），以便与你的类工作。你需要编写名为 `operator+` 的方法，如下所示：

```cpp
class SpreadsheetCell {
public:
    // 为了起见已省略
    SpreadsheetCell operator+(const SpreadsheetCell& cell) const;
    // 为了起见已省略
}
```

> 注意 允许在 `operator` 和加号之间写空格。例如，与其写 `operator+`，你可以写 `operator +`。这适用于所有运算符。本书采用了不带空格的风格。

方法的定义与 `add()` 方法的实现相同：

```cpp
SpreadsheetCell
SpreadsheetCell::operator+(const SpreadsheetCell& cell) const {
    SpreadsheetCell newCell;
    newCell.set(mValue + cell.mValue); // 更新 mValue 和 mString。
    return newCell;
}
```

现在你可以像之前所示使用加号来添加两个单元格。
这种语法需要一点习惯。尽量不要太担心那个奇怪的名称 `operator+` —— 它就像 `foo` 或 `add` 名字一样。理解其余语法有助于理解正在发生什么。当你的 C++ 编译器解析程序并遇到运算符（如 `+`、=` 或 `<<`）时，它会尝试寻找名为 `operator+`、`operator-`、`operator=` 或 `operator<<` 的相应函数或方法，并采取相应的参数。例如，当编译器看到以下行代码时，它尝试在 `SpreadsheetCell` 类中寻找一个接受另一个 `SpreadsheetCell` 对象的 `operator+` 方法，或者一个接受两个 `SpreadsheetCell` 对象的全局函数 `operator+`：

```
SpreadsheetCell aThirdCell = myCell + anotherCell;
```

如果 `SpreadsheetCell` 类包含一个 `operator+` 方法，那么上一行将被转换为：

```
SpreadsheetCell aThirdCell = myCell.operator+(anotherCell);
```

注意，并没有要求 `operator+` 返回一个与与其定义的类类型相同的对象。你可以为 `SpreadsheetCell` 编写一个 `operator+`，接受一个 `Spreadsheet` 并将其加到 `SpreadsheetCell` 上。这对程序员来说没有意义，但编译器会允许这样做。

同样注意，你可以给 `operator+` 返回任何想要的返回值。运算符重载是函数重载的一种，而调用该函数重载并不查看函数的返回类型。

## 隐式转换

惊讶的是，一旦你写了前面所示 `operator+`，你不仅可以将任何两个单元格相加，还可以将单元格与字符串、double 或 int 相加！

```
SpreadsheetCell myCell(4), aThirdCell;
string str = "hello"; nThirdCell = myCell + str;
ThirdCell = myCell + 5.6;
ThirdCell = myCell + 4;
```

这段代码之所以有效，是因为编译器在尝试寻找合适的 `operator+` 时所做的工作不仅仅是寻找一个类型完全匹配的运算符。当没有找到 `operator+` 时，编译器还会尝试为之寻找合适的转换。接受相关类型的构造函数就是合适的转换器。在前面的示例中，当编译器看到尝试将 `double` 加到 `Spreadsheet` 时，它构造了一个临时的 `SpreadsheetCell` 对象传递给 `operator+`。同样，当编译器看到将 `SpreadsheetCell` 加到字符串的行时，它调用 `stringCell` 构造函数创建一个临时的 `SpreadsheetCell` 传递给 `operator+`。

这种隐式转换行为通常很方便。然而，在前面的示例中，将 `SpreadsheetCell` 加到字符串并没有真正的意义。你可以通过用 `explicit` 关键字标记该构造函数来防止从字符串隐式构造 `SpreadsheetCell`：

```cpp
class SpreadsheetCell{
    public:
        SpreadsheetCell();
        SpreadsheetCell(double initialValue);
        explicit SpreadsheetCell(const std::string& initialValue);
        SpreadsheetCell(const SpreadsheetCell& src);
```

206 | 第 8 章 精通类与对象

```cpp
SpreadsheetCell::operator=(const SpreadsheetCell& rhs);
// 为了简洁，省略了其余部分；
```

`explicit` 关键字仅在类定义中有效，并且仅当应用于可以通过一个参数调用的构造函数时才有意义，例如单参数构造函数或带有参数默认值的多参数构造函数。

选择隐式构造可能是低效的，因为必须创建临时对象。为了避免添加 `double` 时的隐式构造，你可以如下所示创建另一个 `operator+`：

```cpp
SpreadsheetCell::operator+(double rhs) const
{
    return SpreadsheetCell(mValue + rhs);
}
```

同样注意，这说明你不需要创建一个变量来返回一个值。

## 第三次尝试：全局 operator+

隐式转换允许你使用 `operator+` 将你的 `SpreadsheetCell` 对象与 int 和 double 相加。然而，该运算符不是交换的，因此以下代码中的某些内容有问题：

```
aThirdCell = myCell + 4; // 正常。
aThirdCell = myCell + 5.6; // 正常。
aThirdCell = 4 + myCell; // 编译失败！
aThirdCell = 5.6 + myCell; // 编译失败！
```

当 `SpreadsheetCell` 在运算符左侧时，隐式转换工作正常，但当它在右侧时则不起作用。由于加法应该是交换的，所以哪里出了问题。问题在于在于 `operator+` 必须在 `SpreadsheetCell` 对象上调用，且该对象必须在 `operator+` 的左侧。这就是 C++ 语言的定义方式，因此你没有办法让上述代码通过 `operator+` 方法正常工作。

然而，如果我们将类内 `operator+` 替换为不绑定任何特定对象的全局 `operator+` 函数，我们能实现它吗？该函数如下：
