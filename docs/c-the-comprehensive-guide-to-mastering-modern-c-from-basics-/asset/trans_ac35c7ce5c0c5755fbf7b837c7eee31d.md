

```cpp
MyValue& MyValue::operator=(const MyValue&);
```

请注意，这是一个方法而不是构造函数。被赋值的对象已经存在；其内容将通过此赋值运算符被覆盖。由于它不是构造函数，你不需要在初始化列表中执行数据字段的传输，而是像方法体中的操作那样进行。

```cpp
// https://cppbolt.org/z/S65GV9Yj
struct MyValue {
    // 其他部分与之前相同
    MyValue& operator=(const MyValue& right) {
        if(this != &right) { // 1. 检查自赋值
            // 2. 释放之前的资源；此处没有
            // 3. 通过赋值或类似方式逐元素传输
            name_ = right.name_ + "-Assignment (previously " + name_ +
        }
        /* 保持保持不变，因此保留了原始缩进 */
        return *this; // 4. 返回自身
    }
};
```

列表 16.16 实现自定义赋值运算符的模式。

如果你将此代码插入到 `struct MyValue` 的定义中，你将得到以下输出：

Constructor ABCD
Constructor WXYZ
Destructor WXYZ
Destructor WXYZ-Assignment (previously ABCD)

这样世界就井有序了：你可以从文本和缩进中看出哪个原始对象是在被覆盖的，以及它是何时被清理的。

如果你为自己的类手动定义 `operator=` 赋值运算符，请务必遵循之前所示的实现模式：

- 使用 `if(this != &right)` 检查此地址是否与 `&` 相同。如果不这样做，在进行类似 `value1 = value1;` 的自赋值时可能会出现问题。

- 释放被覆盖对象的所有之前的资源。这在 `Listing 16.16` 的第 2 处标出，因为对于 `Value` 来说这里没有需要做的。

- 如 3 所示，将所有元素从右传输到左。这通常通过赋值或其他形式的拷贝完成。如果你在这种情况下特意省略了 `number_` 的传输，请对这种不寻常之处添加注释。

- 使用 `return *` 返回当前对象的引用。这允许诸如 `value1 = value2 = value3 = value4;` 这样的赋值链。

赋值运算符与拷贝构造函数之间的相似性非常广泛：

- 通常情况下，你不需要自定义赋值运算符；编译器生成的那个对于内置数据类型、标准容器以及标准库的大多数类型至少一样好。

- 如果你手动定义（或需要定义）拷贝构造函数或析构函数，你通常也需要自己的赋值运算符——反之亦然。

除了实现赋值运算符的方式不同外，还有另一个关键区别：如果你在类中拥有 `const` 数据元素，那么赋值运算符将从可用操作列表中移除——或者说被“删除”。结果是你再也无法通过赋值来覆盖实例。为了说明这一点，我将 `MyValue` 类简化为一个构造函数和一个常量数据字段。

```cpp
struct Number {
    const int number; // 常量数据字段
    explicit Number(int v)
        : number{v} // 常量数据字段初始化
    () {}
};
int main() {
    Number c1(4);
    Number c2(7);
    c1 = c2; // 错误：赋值被编译器移除
}
```

列表 16.17 “const”数据元素初始没有赋值运算符。

这里无法进行 `c1 = c2` 赋值。编译器尝试生成赋值运算符；它尝试赋值 `number_ = other.number_`。这是可能的，因为 `number_` 被声明为 `const`。因此，编译器没有生成赋值运算符，而是删除了它。这导致该类无法使用 `=`运算符。

## 16.8 移除方法

这的效果与如下一个列表所示定义 `MyNumber` 相同。注意，我再次将 `number_` 改为非 `const`，编译器本会生成赋值运算符。

```cpp
// https://godbolt.org/z/398GhcbaE
struct MyNumber {
    int number; // 变量数据字段

    explicit MyNumber(int v)
        : number(v) {}
    MyNumber& operator=(const MyNumber&) = delete; // 移除赋值
    MyNumber& operator=(const MyNumber&) = delete; // 移除拷贝
};
int main() {
    MyNumber c1(4);
    MyNumber c2(7);

    c1 = c2; // 错误 - 赋值被程序员移除
    MyNumber c3(c1); // 错误 - 拷贝被程序员移除
}
```

列表 16.18 使用 "= delete” 手动移除操作。

`= delete` 是程序员防止编译器生成某种方法的方法。正如你从 `MyNumber` 中 `(const MyNumber&) = delete;` 的第二个 `= delete` 所示的，你也可以用它来移除构造函数。因此，在 `MyNumber{c1}` 中对 `MyNumber` 进行拷贝也不再是可能的。

在我们的 `MyValue` 示例中，我逐步处理拷贝构造函数和赋值运算符的必要实现，这并没有产生太大的问题。编译器生成的拷贝构造函数或赋值运算符在最坏的情况下只是在屏幕上输出了错误的输出。

列表 16.7 没有处理拷贝和赋值，导致了一个容易出错的类。如果拷贝或赋值 `Database` 实例会发生什么？你最终会复制数据库句柄或覆盖现有的句柄：

- 如果复制了它，那么析构将在同一个句柄上调用两次 `db_close`。
- 如果你覆盖了它，那么你就漏掉了一个 `db_close`。

如果你的类不遵循以下规则，就会发生严重的错误：如果你定义了析构函数，你通常需要自己的拷贝构造函数和赋值运算符。

通过 `= delete`，你可以快速控制 `Database` 的问题。

```cpp
// https://godbolt.org/z/vb5a3Ej
#include <iostream> // cout
#include "database.hpp" // 外部API

class Database {
    const db_handle_t db_; // 常量
public:
    Database(const* filename);
    ~Database();
    Database(const Database&) = delete; // 禁止拷贝
    Database& operator=(const Database&) = delete; // 禁止赋值
};

// 实现如下所示
int main() {
    Database db("customers.dat");
    std::cout << "Count: " << db.execute("select * from cust") << "\n";
    Database db2{ db }; // 禁止拷贝
    db = db2; // 禁止赋值
}
```

列表 16.19 被删除的函数防止了该类的错误用法。我也将 `db_` 字段标记为 `const`。这本身就能阻止编译器生成 `operator=`，使得程序在这方面是安全的。因为我已经手动删除了拷贝构造函数，所以安全起见对待赋值运算符也是相同的。

## 16.9 移动操作

你已经学习了拷贝类实例的方法。假设你的类是 `Image`：

- `Image(const Image&)`——拷贝构造函数
这只发生在新对象的初始化期间。
- `Image& operator=(const Image&)`——赋值运算符
这会覆盖且只发生在已对象上。

在大多数情况下，源的所有数据字段都会被拷贝到目标。当然，这可能是非常昂贵的。

```cpp
// https://godbolt.org/z/75Kh5Ws45
#include <vector>
class Image {
    std::vector<std::byte> data;
public:
    explicit Image(const char *fn) { /*...*/ }
    // 编译器生成（等等）：
    // 拷贝构造、赋值，还有移动
};
std::vector<Image> loadCollection(bool empty) {
    if(empty) return std::vector<Image>();
    std::vector<Image> result = {}; // 初始为空
    // 集合中的三个图像 ... 拷贝？
    result.push_back(Image("MonaLisa.png"));
    result.push_back(Image("TheScream.png"));
    result.push_back(Image("BoyWithPipe.png"));
    return result; // 按值返回集合
}
int main() {
    // 将返回值存储在变量中
}
```

