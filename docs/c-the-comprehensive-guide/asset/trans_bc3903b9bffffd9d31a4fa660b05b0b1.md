
然而，如果你做出任何非数学上的愚蠢行为，set 可能就无法按预期工作了。例如，如果你定义 < 时不小心在元素类型上定义了 <=，那么 set 就无法再判断相等性。如果值为 7 的 e 已经包含在集合中，而你用同样值为 7 的 f 去查找，它就不再起作用了。

在清单 24.46 中，我定义了一个 lambda 作为比较函数，这样我的示例也能用于普通的 int，因为 int 已经有了 <。如果你想将自己的数据类型 Elem 放入 set，只需重载

```cpp
bool operator<(const Elem &e, const Elem &f);
```

不过，至少从 C++20 开始，重载 operator<=> 应该更容易。因为如果你这样做，C++ 会自动从中推导出所有比较运算符。

清单 24.46 错误地定义了 set 的比较操作，当 e 和 f 相等时返回 true 而不是 false。然后，当用 find(7) 搜索实际包含在集合中的元素时，它将不再被找到。

```cpp
// https://godbolt.org/z/jdfh3ddss
using std::cout; using std::ostream; using std::set;
auto comp = [](auto e, auto f) { return e <= f; }; // ✖ defined wrong!
std::set<int,decltype(comp)> data(comp);
data.insert({ 9,5,7,2,3,6,8 });
cout << data;                    // Output with luck: 2 3 5 6 7 8
auto it = data.find(7);
if (it != data.end()) {
    cout << "got it: " << *it << '\n';
} else {
    cout << "it's gone!" << '\n'; // you will probably end up here
}
```

**清单 24.46** 如果你错误地定义了比较操作，那么“set”将不再起作用。

然而，你可以将多个元素归入一个类别。例如，如果你只要求十位匹配即可认为相等，那么你的比较操作可以做到这一点。

```cpp
// https://godbolt.org/z/xdPc51q5s
auto comp = [](auto e, auto f) { return e/10<f/10; }; // grouping is okay
std::set<int,decltype(comp)> data(comp);
data.insert({ 14,23,56,71 });
cout << data;                    // Output: 14 23 56 71
auto it = data.find(29);         // 29 now always finds 23
```

这里，输出随后将按字母顺序排序。

如你所见，你可以将 `operator<=>` 写成一个普通的成员函数。你不需要将它定义为 `friend`，甚至不需要在类外部定义。

## 初始化

除了元素或键类型 `Key`，`set` 还有一个*比较器*（comparator）类型名 `Compare` 作为模板参数（以及必须的*分配器*（allocator）；参见 24.3 节）。如果你不指定，默认是 `std::less<Key>`。这最终意味着两个键 `e` 和 `f` 使用小于号 `<` 进行比较，以保持集合有序。对于像 `int` 这样的内置类型，这也就是内置的 `<`。对于你自己的类型，你可以重载自由函数 `operator<`。如果你选择这些选项之一，就不需要指定自己的比较器。

只有当 `<` 不能满足你的需求时，才应定义自己的比较器。你需要定义一种“小于”`<`，但绝不能是“小于或等于”`<=`；参见清单 24.46。比较器是一个可调用对象，带有两个 `Key` 参数并以 `bool` 作为返回类型，或者可隐式转换为这些的类型。和通常一样，可以是函数指针、lambda 或仿函数。

仿函数在这里很实用，因为只需将其类型指定为模板参数即可。另外，从 C++17 开始，你可以使用 lambda 或函数指针作为构造函数参数，从而可以省略其他显式模板参数。

```cpp
// https://godbolt.org/z/c8a9qPoPP
#include <set>
#include <functional> // function
using std::set; using std::function; using std::initializer_list;
bool fcompTens(int a, int b) { return a % 10 < b %10; }
struct Fives {
    bool operator()(int a, int b) const { return a%5 < b % 5; }
};

int main() {
    //Functor
    set<int, Fives> ff1;
    ff1.insert(5);
    set f2({5}, Fives{});
    set f3{initializer_list<int>{{}}, Fives{}};
    //Lambda
    set<int, function<bool(int,int)>> l1{[](auto a,auto b){return a%3<b%3;}};
    l1.insert(3);
    auto lcomp = [](int a, int b) { return a%3 < b%3; };
    set<int, decltype(lcomp)> l2(lcomp);
    l2.insert(3);
    set l3{{3}, lcomp};
    // Function pointer
    set<int, bool(*)(int,int)> zz1(&fcompTens);        // C-style
    zz1.insert(10);
    set<int, function<bool(int,int)>> zz2(&fcompTens); // C++ style
    zz2.insert(10);
    set<int, decltype(&fcompTens)> zz3(&fcompTens);     // C++ style
    zz3.insert(10);
}
```

**清单 24.49** 有多种指定比较器的方式。

比较器通常可以与用于初始化 set 的元素一起指定。类似于 vector（24.6.3 节），有以下几种方式可以将初始元素传递给构造函数：

- 不带参数（例如，默认构造函数）
- 使用一对迭代器，从另一个容器中获取一个范围
- 作为另一个 set 进行复制
- 作为初始化列表
- 从 C++23 开始，作为带有 *from_range* 标签的范围

```cpp
// https://godbolt.org/z/oc9xxe95
// without arguments
set<int> empty{};
cout << empty;          // Output:
// initializer list
set list{1,2,2,3,3,4,4,5,5};  // set does not take duplicates
cout << list;           // Output: 1 2 3 4 5
// copy
set copy(list);
cout << copy;           // Output: 1 2 3 4 5
// pair of iterators
set from_to( std::next(list.begin()), std::prev(list.end()));
cout << from_to;        // Output: 2 3 4
// Range
set even(from_range, list | vs::filter([](int i){ return i%2; }));
cout << even;           // Output: 2 4
```

**清单 24.50** 构造时又有几种指定元素的方式。

移动是可能的，因为移动构造函数也被定义了。为此，像通常一样，Elem 必须是可移动的：

```cpp
// https://godbolt.org/z/1dTPed3nP
set source{1,2,3,4,5};
cout << source;          // Output: 1 2 3 4 5
set target( std::move(source) ); // move instead of copy
cout << source;          // Output:
cout << target;          // Output: 1 2 3 4 5
```

## 赋值

set 也提供了 operator=(const set<Elem>&)，因此你可以在之后将另一个 set 的内容复制到一个已创建的 set 中。并且由于存在 operator=(set<Elem>&&) 的重载，这也适用于移动：

```cpp
// https://godbolt.org/z/8eGWY45o
set source{1,2,3,4,5};
set<int> target{};
set<int> target2{};
cout << source;          // Output: 1 2 3 4 5
cout << target;          // Output:
cout << target2;         // Output:
target = source;         // copy afterward
cout << source;          // Output: 1 2 3 4 5
cout << target;          // Output: 1 2 3 4 5
target2 = std::move(source); // move
cout << source;          // Output:
cout << target2;         // Output: 1 2 3 4 5
```

assign 和 assign_range 方法不适用于关联容器，因此也不适用于 set。对于序列容器，此方法用于重新初始化一个已存在的容器，提供与构造函数调用类似的参数指定选项。

如果你想对关联容器进行这种类似构造函数的重新初始化，你需要采取不同的方式。这可以在不损失性能的情况下完成。清单 24.51 展示了两种可能性。

```cpp
// https://godbolt.org/z/oZMY86ns8
#include <vector>
//...
set data{1,2,3,4,5};
std::vector source{10, 20, 30, 40, 50};

// There is no set::assign:
data.assign(source.begin(), source.end()); // no set::assign
// So simulate it using a temporary set:
set temp(source.begin(), source.end()); // copy from source...
data.swap(temp); // ... efficiently swap contents
cout << data; // Output: 10 20 30 40 50

// ... or by clearing first and then inserting:
data.clear();                                      // clear ...
data.insert(source.begin(), source.end());   // ... and insert
cout << data;                                  // output: 10 20 30 40 50
```

**清单 24.51** 你可以使用“拷贝并交换”惯用法来代替“assign”。

在第一种变体中，我使用了临时 set 并应用了“拷贝并交换”惯用法。第二种选项利用了 insert 支持的参数组合与构造函数一样多这一事实。

## 插入

在 set 中，你总是使用 insert 或 emplace 进行插入。insert 支持所有可能的参数组合，类似于 set 构造函数的那些参数组合，从 C++23 开始还支持 *insert_range*。可能更快的 *emplace_hint* 与 emplace 一起可用。

在插入操作之后，所有指向 set 的迭代器都保持有效。

### *插入单个元素并自动定位*

insert 可以通过拷贝插入单个值。元素会自动插入到有序顺序中的正确位置。为了保证这一点，首先需要在 log n 步内找到正确位置，其次，内部树结构可能需要重新调整。emplace 也是如此，不同之处在于你直接指定元素的构造函数参数，而不是元素本身。如果你要插入的内容已经存在于 set 中，它不会被覆盖！在这种情况下，insert 的返回值是 pair<iterator,bool>：如果 bool 为 true，则确实插入了新元素。迭代器指向插入位置。

我让编译器用 = default 为 Point 定义方法 operator<=>，然后它会按字典序比较字段 x_ 和 y_。编译器会从中生成 operator<。如果你没有 C++20，可以定义一个 friend 函数 operator<，返回 tie(a.x_, a.y_) < tie(b.x_, b.y_);。

```cpp
// https://godbolt.org/z/8nj7vfeba
// ...
template<typename IT> ostream& operator<<(ostream& os, const pair<IT,bool> wh)
{ return os << (wh.second ? "yes" : "no"); }
struct Point {
    double x_, y_;
    Point(double x, double y) : x_{x}, y_{y} {}
    auto operator<=>(const Point&) const = default;
    friend ostream& operator<<(ostream& os, const Point& p) {
        return os << "(" << p.x_ << "," << p.y_ << ")";
    }
};
```
