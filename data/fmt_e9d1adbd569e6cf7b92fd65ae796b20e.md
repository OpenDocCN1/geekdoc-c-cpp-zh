
这里是 `copyFrom()` 和 `operator=` 的实现。请注意，如果 `src` 更大，`copyFrom()` 分别在 `x` 和 `y` 维度上拷贝 `WIDTH` 和 `HEIGHT` 个元素。如果 `src` 在维度上较小，`copyFrom()` 用零初始化值填充额外的位置。如果 `T` 是一个类，`T()` 会调用对象的构造函数；如果 `T` 是简单类型，则进行零初始化。这种语法被称为零初始化。这是为你未变量类型提供默认值的好方法：

```cpp
template <typename T, size_t WIDTH, size_t HEIGHT>
template <typename E, size_t WIDTH2, size_t HEIGHT2>
void Grid<T, WIDTH, HEIGHT>::copyFrom(const Grid<E, WIDTH2, HEIGHT2>& src)
{
    for (size_t i = 0; i < WIDTH; i++) {
        for (size_t j = 0; j < HEIGHT; j++) {
            if (i < WIDTH2 && j < HEIGHT2) {
                mCells[i][j] = src.getElementAt(i, j);
            } else
                mCells[i][j] = T();
            }
        }
    }
}
```

```cpp
template <typename T, size_t WIDTH, size_t HEIGHT>
template <typename E, size_t WIDTH2, size_t HEIGHT2>
Grid<T, WIDTH, HEIGHT>&Grid<T, WIDTH, HEIGHT>::operator=(
    const Grid<E, WIDTH2, HEIGHT2>& rhs)
{
    // 不需要检查自赋值
    copyFrom(rhs);
    return *this;
}
```

## 带有非类型参数的方法模板

在带有 `HEIGHT` 和 `WIDTH` 整数模板参数的示例中，你会看到一个主要问题是高度和宽度变成了类型的一部分。这种限制阻止了你将一个特定高度宽度的网格赋值给另一个不同高度宽度的网格。然而，在某些情况下，赋值或拷贝不同尺寸的网格是符合期望的。与其让目标成为源对象的完美克隆，不如你只需要从源数组中拷贝符合目标数组大小的元素，如果源数组在维度上较小，则用默认值填充目标数组。通过模板方法，你可以允许不同尺寸的赋值和拷贝。以下是该类的定义：

```cpp
template <typename T, size_t WIDTH = 10, size_t HEIGHT = 10>
class Grid
{
public:
  Grid() : mCells() {} // 初始化 mCells

  template <typename E, size_t WIDTH2, size_t HEIGHT2>
  Grid(const Grid<E, WIDTH2, HEIGHT2>& src);

  template <typename E, size_t WIDTH2, size_t HEIGHT2>
  Grid<T, WIDTH, HEIGHT>&operator=(const Grid<E, WIDTH2, HEIGHT2>& rhs);

  void setElementAt(size_t x, size_t y, int elem);

  T& getElementAt(size_t x, size_t y);
  const T& getElementAt(size_t x, size_t y) const;

  size_t getHeight() const { return HEIGHT; }
  size_t getWidth() const { return WIDTH; }

  template <typename E, size_t WIDTH2, size_t HEIGHT2>
  void copyFrom(const Grid<E, WIDTH2, HEIGHT2>& src);

  T Cells[WIDTH][HEIGHT];
};
```

在 `copyFrom()` 方法之前的模板参数行之外，你必须使用公共方法 `getWidth()`、`getHeight()` 和 `getElementAt()` 来访问 `src` 的元素。因为你正在拷贝的对象类型是 `Grid<T>`，而你正在从中拷贝的对象类型是 `Grid<E>`。它们不是同一个类型，所以你必须使用公共方法。

最后一个模板方法是赋值运算符。请注意，它接收一个 `const Grid<E>&` 但返回一个 `Grid<T>&`：

```cpp
template <typename T>
template <typename E>
Grid<T>& Grid<T>::operator=(const Grid<E>& rhs)
{
  copyFrom(rhs);
  return *this;
}
```

你不需要在模板赋值运算符中检查自赋值，因为类型的赋值仍然发生在旧的、非模板的、编译器生成的 `operator=` 版本中，所以你在这里无法发生自赋值。

## 类的特化

类特化是模板的特定实现。特化的主要好处是它们对用户是不可见的。当用户创建一个 `int` 的 `Grid` 时，编译器会从原始模板生成代码。当用户创建一个 `char*` 的 `Grid` 时，会使用你的特化。要实现特化，需要使用以下语法：

```cpp
template <>
class Grid<char*>
{
public:
    Grid(size_t inWidth = 10, size_t inHeight = 10);
    ~Grid();

    void setElementAt(size_t x, size_t y, char* elem);
    const char* getElementAt(size_t x, size_t y) const;

    size_t getHeight() const { return mHeight; }
    size_t getWidth() const { return mWidth; }
    static const size_t kWidth = 10;
    static const size_t kHeight = 10;

private:
    void initializeCells();
    std::vector<std::vector<char*>> mCells;
    size_t mWidth, mHeight;
};
```

# 336 | 第 11 章 编写泛型代码模板

```cpp
column.resize(mHeight);

void Grid const*::setElement(size_t x, size_t y, const char* inElem)
{
    if (inElem)
        mCells[x][y] = inElem;
    else
        mCells[x][y] = "";
}

const char* Grid<char*>::getElement(size_t x, size_t y) const
{
    return mCells[x][y].c_str();
}
```

本节讨论了如何使用特化。它允许为类型被替换为特定类型的模板编写特殊实现。第 21 章将通过一种名为“部分特化”的更高级特性继续讨论特化。

## 派生自类模板

你可以继承类模板。如果派生类继承自模板本身，那么它本身也必须是一个模板。或者，你可以从类模板的实例化进行派生，在这种情况下，你的派生类不需要是模板。作为前者的例子，假设你认为 `Grid` 类提供的功能不足以用作游戏板。具体来说，你想为游戏板添加一个 `move()` 方法，将棋子从一个位置移动到另一个位置。以下是 `GameBoard` 模板的类定义：

```cpp
template <typename T>
class GameBoard : public Grid<T>
{
    public:
        explicit GameBoard(size_t Width = Grid<T>::kDefaultWidth,
                           size_t Height = Grid<T>::kDefaultHeight);
        void move(size_t x, size_t y, size_t x2, size_t y2);
};
```

`GameBoard` 派生自 `Grid` 模板并继承了它所有的功能。你不需要重写 `setElement()`、`getElement()` 或任何其他方法。除非你在 `GameBoard` 中动态分配了内存，否则你不需要添加拷贝构造函数、赋值运算符或析构函数。

继承的语法看起来很正常，只是基类是 `Grid<T>`。这种语法之所以存在是因为 `GameBoard` 模板并没有真正派生自泛型模板。`GameBoard` 的每个实例化都继承自泛型模板中的一个特定类型。例如，如果你用 `ChessPiece` 类型实例化 `GameBoard`，那么编译器会为 `Grid<ChessPiece>` 生成代码。该类所继承的 `public: Grid` 语法对于 `T` 类型参数的任何 `Grid` 实例化都是有意义的。请注意，C++ 模板继承的名称查找规则要求你指定 `kDefaultWidth` 和 `kDefaultHeight` 是在 `Grid<T>` 基类中声明的，因此依赖它。

以下是构造函数和 `move()` 方法的实现。再次注意在调用基类构造函数时使用了 `Grid<T>`。此外，许多编译器没有强制要求名称查找规则使用 `this` 指针来引用基类模板中的数据成员和方法：

```cpp
template <typename T>
GameBoard<T>::GameBoard(size_t inWidth, size_t inHeight) :
    Grid<T>(inWidth, inHeight)
{
}

template <typename T>
void GameBoard<T>::setElementAt(size_t xDest, size_t yDest, size_t xSrc, size_t ySrc)
{
    this->setElementAt(xSrc, ySrc);
    this->setElementAt(xSrc, ySrc, T()); // 默认构造源单元
}
```

如你所示，可以使用“带非类型参数的方法模板”节中描述的 `T()` 语法。你可以如下使用 `GameBoard`：

```cpp
GameBoard<ChessPiece> chessboard(8, 8);
ChessPiece pawn;
chessboard.setElementAt(0, 0, pawn);
chessboard.move(0, 0, 1);
```

## 继承与特化

有些程序员发现模板继承与模板特化的区别很困惑。下表总结了这些差异：

| 特性 | 继承 | 特化 |
| :--- | :--- | :--- |
| 重用代码？ | 是：派生类包含了基类的所有数据成员和方法。 | 否：你必须在特化中重写所有需要的代码。 |
| 重用名称？ | 否：派生名称必须与基类名称不同。 | 是：特化类的名称必须与原始模板相同。 |
| 支持多态？ | 是：派生类对象可以代表基类对象。 | 否：模板的每个类型实例化都是不同的类型。 |

> **注意** 使用继承来扩展实现和支持多态。使用特化为特定类型定制实现。

## 别名模板

第 10 章引入了 `typedef` 的概念。它允许你为特定类型提供另一个名称。为了唤起记忆，例如你可以编写下面的 `typedef` 来为 `int` 类型提供第二个名称：

```cpp
typedef int MyInt;
```

同样，你可以使用 `typedef` 为模板类提供另一个名称。但 C++ 要求你为每个模板参数指定参数。

```cpp
template<typename T1, typename T2>
class MyTemplateClass /* ... */;
```

如果你想用 `typedef` 为 `MyTemplateClass` 定义另一个名称，你必须为 `T1` 和 `T2` 提供具体类型。

```cpp
res = Find<double>(d1, dArr, sizeArray); // 显式调用 Find<double>
if (res != NOT_FOUND)
    cout << res << endl;
else
    cout << "Not not found" << endl;

//res = Find(x, dArr, sizeArray); // 无法编译！// 参数类型不同。

SpreadsheetCell c1[0], cArr[2] = {
    SpreadsheetCell(10), SpreadsheetCell(10)};
size_t sizeC2Arr = sizeof(SpreadsheetCell);
res = Find(c1, c2Arr, sizeC2Arr);
res = Find<SpreadsheetCell>(c1, c2Arr, sizeC2Arr);
```

之前的 `Find()` 实现要求数组的大小作为参数之一。有时编译器知道数组的确切大小，例如对于基于栈的数组。如果可以在对此类数组时调用 `Find()` 函数，而不需要传递数组的大小，那将非常好。这可以通过添加以下函数模板来实现。该实现证明了函数模板可以像类模板一样接受非参数类型。

```cpp
template <typename T, size_t S>
size_t Find(T value, T (&arr)[S])
{
    return Find(value, arr, S);
}
```

此版本的 `Find()` 可以这样调用：
`int x = 3, intArr[] = {1, 2, 3, 4};`
`size_t res = Find(x, intArr);`

就像类模板定义一样，函数模板必须对所有使用它的源文件可见。因此，如果有超过一个源文件使用它们，你应该将定义放在头文件中。

函数模板的模板参数可以有默认值，就像类模板一样。

> C++ 标准库提供了一个模板化的 `std::find()` 函数，它比上面的函数更强大。详情请参见第 17 章。

## 函数模板特化

就像你可以特化类一样，你也可以特化函数模板。例如，你可能想为 `const char*` 字符串类型定义一个 `Find()` 函数，使用 `strcmp` 代替 `operator==` 来进行比较。以下是实现此目的的 `Find` 函数特化：

```cpp
template<>
size_t Find(const char* (const char*& value, const char** arr, size_t size)
{
    cout << "Specialization" << endl;
    for (size_t i = 0; i < size; i++) {
        if (strcmp(arr[i], value) == 0) {
            return i; // 找到了；返回索引
        }
    }
    return NOT_FOUND; // 未找到；返回 NOT_FOUND
}
```

当参数类型从参数中推导出来时，你可以在函数名中省略 `const*`，使你的原型类型看起来如下：

```cpp
template<>
size_t Find(const char& value, const char** arr, size_t size)
```
