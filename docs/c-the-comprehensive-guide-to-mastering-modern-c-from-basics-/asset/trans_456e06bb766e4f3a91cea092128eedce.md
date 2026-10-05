

-   函数与方法
你已经熟悉它们了：你定义一个带有返回类型、函数名、调用参数和函数体的头文件。

-   函数对象（Functors）
函数对象是一个定义了 `operator()` 的类。
该类的实例表现得像函数一样。

-   匿名函数或 lambda 表达式
如果你想向一个算法传递一个操作——例如，“我该如何比较以进行排序？”——你可以直接将函数体（“如何做”）作为参数传递，而无需预先定义函数。这就是为什么它被称为*匿名函数*，或者在计算机科学术语中被称为*lambda 表达式*。

带有 `operator()` 方法的类的实例行为就像函数。你可以像下面列表所示那样调用它们。

```cpp
// https://godbolt.org/z/xvfvG8hrd
#include <iostream> // cout
using namespace std;
class Increment {
    int amount_;
public:
    explicit Increment(int amount) : amount_{amount} {}
    int operator()(int value) const { // 使实例可调用
        return value + amount_;
    }
    void clear() {
        amount_ = 0;
    }
};
int main() {
    Increment PlusFour(4); // 创建实例
    Increment PlusEleven(1); // 另一个实例
    cout << PlusFour(8) << "\n"; // 输出: 12
    int result = 2 * PlusEleven(5) - 7; // result 为 25
    cout << PlusEleven(result/5) << "\n"; // 输出: 16
    cout << 3 * Increment{1}(7) << "\n"; // 输出: 24
    Increment plusZero = plusEleven;
    plusZero.clear(); // 修改状态
    cout << plusZero(1) << "\n"; // 输出: 1
}
```

### 列表 23.15 带有 "operator()" 的类创建函数对象

如果你只看 `plusFour(8)` 这一行，看起来好像 `plusFour` 隐藏了函数：

```cpp
int plusFour(int value) {
  return value + 4;
}
```

如果你看 `plusEleven(result/5)` 这一行，你可能会假设有一个函数：

```cpp
int plusEleven(int value) {
  return value + 1;
}
```

这种情况可以持续下去产生 `+0`、`+2` 等——你会纳惑为什么要写这么多函数。这就是函数对象大显身场的地方。如果一组函数非常相似，仅区别于可以用内部状态表示的细节，那么带有数据字段的类就是优解决方案。让我们慢慢开发这个。如果你使用已经熟悉的方法，可以像下一个列表所示，编写并使用一个带有普通方法的类。

```cpp
// https://godbolt.org/z/xa
#include <iostream> // cout
using namespace std;
class Add {
    int amount_;
public:
    explicit Add(int amount) : amount_(amount) {}
    int add(int value) const { // 代替 operator()
        return value + amount_;
    }
    void clear() { amount_ = 0; }
};
int main() {
    Add plusFour(4); // 创建实例
    Add plusEleven(1); // 另一个实例
    cout << plusEleven.add(8) << "\n"; // 输出: 12
    int result = 2 * plusEleven.add(5) - 7; // result 为 25
    cout << plusEleven.add(result/5) << "\n"; // 输出: 16
    cout << plusEleven.add(7) << "\n"; // 输出: 24
    Add plusZero = plusEleven;
    plusZero.clear(); // 修改状态
    cout << plusZero.add(1) << "\n"; // 输出: 1
}
```

### 列表 23.16 带有普通方法的类

事实上，只有两个区别：

-   `Increment` 将 `operator()(int value) const` 定义为一个方法，而 `Add` 使用了普通的 `add(int value) const` 来实现。
-   第一种情况的调用是 `plusFour(8)`，第二种情况是 `plusEleven.add(8)`。

你看到这两个类实际上的区别仅在于，当你直接使用实例时，可以省去 `.add(...)` 的输入——就像调用函数一样。这正是为什么带有 `operator()` 的类实例被称为函数对象的原因。带有 `operator()` 的类本身被称为泛型对象（functor）。

`Increment` 泛型对象确实是此类中相当复杂的代表。事实上，泛型对象既没有像 `amount_` 这样的内部状态，也没有 `clear()` 这样的修改器。泛型对象实际上更像是编写函数的另一种方式——抱歉，一个可调用对象。因此，函数对象整合到了 C++ 的其他结构中：

-   你可以编写带有 `operator()` 的类。
-   `operator()` 可以是虚函数。
-   你可以重载 `operator()`——即编写多个具有不同类型的变体。
-   你可以表示内部状态（如你所见），并通过构造函数创建变体。
-   而且，你可以像处理任何其他对象一样处理函数对象——例如将其放入容器中。

大多数泛型对象的设计都非常简单。你经常将它们作为自己的类与标准库算法之间的接口。

## 23.3.4 实用的泛型对象

`set<Type>` 总是根据 `operator<()` 进行排序。例如，你可以使用 `set<Dwarf>` 和相应的 `operator<` 创建一个按名称排序的列表。

```cpp
// https://godbolt.org/z/ov87
#include <set>
#include <string>
#include <iostream> // cout
using namespace std;
struct Dwarf {
    string name;
    int age;
    bool operator<(const Dwarf& other) const {
        return name < other.name;
    }
};

int main() {
    set<Dwarf> dwarves = { {"Balin", 50}, {"Dwalin", 60}, {"Fili", 30} };
    for (const auto& d : dwarves) {
        cout << d.name << " ";
    }
}
```

