
如果避免复制是值得的，最好使用 `const&`。`&` 避免复制，`const` 则防止意外修改外部对象。

适用于类的规则对内置类型而言并无不同。然而，内置类型的复制成本可以忽略不计，这就是为什么你很少看到 `const int&` 或 `const double&`。与类相同的规则同样适用——编译器会阻止对值的修改：

```cpp
void nonsensicalParameter(const int& arga, const double& argb) {
    arga = 7;    // Assignment to constant
    argb = 3.14; // Assignment to constant
}
```

如前所述，内置类型也可以这样做，但这相当少见。内置类型几乎总是按值传递：

```cpp
void valueParameter(int arga, double argb);
```

然后你可以在函数内修改它们，这不会影响外部。如果修改应当影响外部，则可以通过引用传递它们：

```cpp
void input(int& arga, double& argb);
```

但这里更好的选择是使用返回值，例如：

```cpp
std::pair<int,double> input();
```

在第 28 章第 28.1 节关于 pair 和 tuple 的内容中，你将更详细地了解这与元组如何协同工作。

最后，你也可以选择值传递（如你所知，这有其优势）并使该值成为常量：

```cpp
void constantValues(const int arga, const double argb);
```

其效果是，调用时你会获得一个副本，同时确保你不会意外尝试 `arga = 5`。

### 13.10.2 常量方法

如果你试图修改一个 `int`，编译器能直接识别。然而，当你面对一个带方法的对象时，问题就变得复杂了：

```cpp
void print(const vector<int>& primes) {
    if(primes.size() > 100)    // that's fine
        return;
    for(auto prime : primes) {  // that's fine too
        cout << prime << " ";
    }
    primes.push_back(4);    // ✗ that's not fine
}
```

编译器怎么知道 `primes.size()` 可以在 `const&` 上调用，而 `primes.push_back(4)` 应当产生错误消息？这是因为 vector 的 `size()` 方法带有尾随 const——本质上：

```cpp
size_t vector<int>::size() const;
```

这告诉编译器，对 const 对象允许调用该方法。

对于自定义数据类型 Widget，可能如下所示：

```cpp
// https://godbolt.org/z/WTWxYa3rd
class Widget {
    unsigned x = 0, y = 0, w = 0, h = 0; // for example
public:
    unsigned getLeft() const;
    unsigned getTop() const;
    unsigned getRight() const;
    unsigned getBottom() const;
    void setWidth(unsigned w);
    void setHeight(unsigned h);
};
```

如果你现在将 Widget 作为 const 对象（引用）传入函数，就可以调用 get 方法：

```cpp
void show(const Widget& widget) {
    drawBox(
        widget.getLeft(), widget.getTop(),
        widget.getRight(), widget.getBottom()
    );
}
```

在 `show` 中调用 `widget.setWidth(100);` 会遭遇编译器错误，因为该方法未被标记为 const。

同时，尾随 const 还有另一个效果：你不能在这种方法的实现中修改数据字段。这同样包括调用非 const 方法：

```cpp
unsigned Widget::getLeft() const {
    x = 77;            // ✗ data fields cannot be changed
    setWidth(88);      // ✗ do not call non-const methods
}
```

综合起来，这三种效果对编译器检测粗心错误和设计问题是极其重要的工具。在将方法标记为 `const` 时，你需要谨慎。你会发现，这样一来，你也必须仔细地决定要么将参数设为 `const`，要么按值传递。那些为粗心错误打开大门的意外 `&` 便不再可能发生。

再练习一次：从技术上讲，隐式的 `this` 参数会因尾随 `const` 而从 `Widget* const this` 转换为 `Widget const* const this`。你已经能读出不同位置上的 `const` 了吗？这些 `const` 修饰的是其前面的 Widget。因此，在方法内部，`Widget` 中的一切都不允许被修改。

### 13.10.3 “const”变量

你也可以将 `const` 应用于变量。这既适用于函数中的局部变量，也适用于全局变量以及类中的数据字段。`const` 变量只能被初始化，你不能给它赋新值，也不能通过非 `const` 方法调用改变它的值：

```cpp
class Widget {
    const int id_;
public:
    explicit Widget(int id) : id_(id) {}
    Widget() : id_(0) {}
    void reset();
};
const Widget widget_a = Widget{12};
```

在这些代码行之后，你不能写 `widget_a = Widget{24};`。在 `reset()` 的实现中，编译器同样禁止：

```cpp
void Widget::reset() {
    id_ = 36;
}
```

因为 `id_` 是 `const`——就像你把它作为参数传递给函数一样。

在认为合理的情况下，请谨慎使用 `const` 变量。对于在很长的代码段中有效、且容易让人遗忘哪些变量存在的场景，`const` 可以有效防止意外修改。

```cpp
// https://godbolt.org/z/bXPa29aW5
#include <vector>
namespace {                  // anonymous namespace for constants
    const unsigned DATA_SIZE = 100;  /* number of elements in data */
    const double LIMIT = 999.999;    /* max value during initialization */
};

std::vector<int> createData() {
    std::vector<int> result(DATA_SIZE);
    double currVal = 1.0;
    for(auto &elem : result) {
        elem = currVal;
        currVal *= 2;          // next value is larger
        if(currVal > LIMIT) {
            currVal = LIMIT;   // no value should be larger
        }
    }
    return result;
}
```

**清单 13.8** 文件的局部常量很适合放在匿名命名空间中。

对于定义某些程序参数的全局变量尤其如此。最好将它们放入*匿名命名空间*。这样做的好处是，其他模块看不到该标识符；在大型项目中，这对防止全局变量和常量相互冲突非常重要。

这使你既能轻松调整程序的某些大小，也能很好地记录这些大小。

### 13.10.4 const 返回值

通常，函数返回值而非引用。这意味着返回的是函数中内容的副本。至少你可以从概念上这样理解。实际中，编译器通常可以避免复制（参见[第 12 章第 12.11 节](#)）。

```cpp
// https://godbolt.org/z/fM4nsx9GP
struct Widget {
    int num_ = 0;
    void setNumber(int x) {    // a non-const method
        num_ = x;
    }
};
Widget createWidget() {        // Return by value
    Widget result{};            // Create
    return result;
}
int main() {
    Widget w = createWidget();  // Return by value creates a copy
    w.setNumber(100);            // changing is naturally okay, w is non-const
}
```

因为 `result` 的副本存在于 `createWidget()` 之外的 `main()` 中，即 `Widget w = createWidget();`，函数不再关心其内容是否被修改。因此，在返回类型上标记 `const` 意义不大。

```cpp
// https://godbolt.org/z/98x3YsnKc
const Widget createWidget() {  // return as const value
    Widget result{};
    return result;
}
int main() {
    Widget w = createWidget();  // copied into new non-const w
    w.setNumber(100);           // w is non-const, changing is okay
}
```

**清单 13.9** 尽管返回类型被标记为“const”，但这里它没有任何效果，因为返回值总是被复制。

虽然返回类型是 `const Widget`，但 `const` 永远不可能产生影响，因为返回值总是按值复制——而调用者控制着复制到何处。这里它再次被复制到 `Widget w`（非 const）中，因此调用者可以随意使用自己的副本。

*引用*（和指针）则截然不同：引用意味着“不复制”。

> **注意被引用对象的生命周期**
>
> 我怎么强调都不为过：如果你返回一个引用，就必须确保引用所指向的对象在你外部使用它的期间一直存在。

```cpp
// https://godbolt.org/z/3EG1oycev
#include <string>
#include <string_view>
using std::string; using std::string_view;

class Widget {
    string name_ = "";
public:
    void setName(string_view newName) {
        name_ = newName;
    }
    const string& getName() const {   // const& return
        return name_;
    }
};
```
