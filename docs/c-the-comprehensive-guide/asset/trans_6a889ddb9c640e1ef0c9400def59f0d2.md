
对于无序容器，输出的顺序可能因标准库的实现不同而有所变化。

请注意我在清单 24.12 之后的代码框中对 `<<` 的注释。

```cpp
// https://godbolt.org/z/38TbJgnh6
#include <unordered_set>
#include <iostream>
using std::unordered_set; using std::cout; using std::ostream;
template<typename Elem, typename Cmp>
ostream& operator<<(ostream& os, const unordered_set<Elem,Cmp>&data){
    for(auto &e : data) {
        os << e << ' ';
    }
    return os << '\n'; // '\n' instead of std::endl for line break
}
int main() {
    // Example code here
}
```

**清单 24.77** 这是关于 “unordered_set” 的示例清单的模板。

## 元素属性

与 `set` 不同，unordered_set 的元素必须支持 operator==。就容器而言，你认为“相等”的事物必须让 operator==(const Elem& a, const Elem& b) 返回 true。另外，你也可以在定义时指定一个 KeyEqual 函数对象作为模板参数，它将用于替代键比较。

此外，你现在需要一个从 Key 计算哈希值的函数对象。为此，请编写一个特化的类模板 std::hash<Key>，其中包含 size_t operator()(const Key &k) const 方法。确保对于所有可能的 k，尽量利用 size_t 的范围。只有这样，容器才能有良好的性能。如果你不能或不想重载该函数，请在定义容器时指定 Hash 的模板参数。

```cpp
// https://godbolt.org/z/TY5x54efE
#include <unordered_set>
#include <iostream>
#include <vector>
#include <string>
using std::string; using std::unordered_set; using std::cout;
struct Word {
    string word_;
    size_t row_;
    Word(const string &word, size_t row)
        : word_(word), row_(row) {}
    friend bool operator==(const Word& a, const Word &b)
        { return a.word_ == b.word_; } // ignores row
};
namespace std {
template<> struct hash<Word> { // ignores row
    std::hash<string> stringHash;
    std::hash<size_t> iHash;
    bool operator()(const Word &w) const {
        return stringHash(w.word_);
    }
}; }
struct ExactWordHash { // includes row
    std::hash<string> sHash;
    std::hash<size_t> iHash;
    bool operator()(const Word &a) const {
        return sHash(a.word_) ^ iHash(a.row_);
    }
};
struct ExactWordEqual { // includes row
    bool operator()(const Word &a, const Word &b) const {
        return std::tie(a.word_, a.row_) == std::tie(b.word_, b.row_);
    }
};
int main() {
    std::vector input {
        Word{"a",0}, Word{"rose",0},
        Word{"is",1}, Word{"a",1}, Word{"rose",1},
        Word{"is",2}, Word{"a",2}, Word{"rose",2}, };
    // Use overloads
    unordered_set<Word> words(input.begin(), input.end());
    cout << words.size() << '\n'; // Output: 3
    // Use custom functors
    unordered_set<Word, ExactWordHash, ExactWordEqual> poem(
        input.begin(), input.end());
    cout << poem.size() << '\n'; // Output: 8
    // Hash as Lambda
    auto h = [](const auto &a) { return std::hash<string>{}(a.word_); };
    unordered_set<decltype(poem), decltype(h)> rose(input.begin(), input.end(), 10, h);
    cout << rose.size() << '\n'; // Output: 3
}
```

清单 24.78 一个带有自定义比较和哈希函数的 “unordered_set”。

对于第一个使用单词的示例，我采用了在常规搜索期望的位置定义这些操作的方法。模板参数的默认值是 `std::hash<Key>` 和 `std::equal_to<Key>`。后者在其实现中使用 operator==(Key, Key) 自由函数。这里定义了两者：operator== 通过 friend 方法作为自由函数可见，hash<Word> 是 std 命名空间中 template<typename Key> struct hash 的模板特化。需要注意的是，你不应该在 std 命名空间中随意定义内容：在 std 中做这样的特化是可以接受的，但你不能在 std 中随意定义新内容；否则你会得到不可移植的代码。

第二个 poem 示例则更为直接，因为它没有使用那些不易察觉的内置机制。这里我指定了要作为模板参数的函数对象。这会更清晰一些，尤其是对于哈希函数，你无法在自己的数据类型内部简单地定义一个 friend 函数。

像往常一样，你不一定必须使用函数对象；可调用对象就足够了。最后，你可以在 rose 示例中看到，我将 lambda `h` 作为哈希函数传递给了构造函数。然而，我还必须使用 `decltype(h)` 将其类型作为模板参数传递。此外，构造函数参数的顺序要求我必须在哈希函数之前传递容器的桶数量——因此这里有一个 10。

## 初始化

和往常一样，在定义和初始化时，你需要定义两件事：模板参数和构造函数参数。自 C++17 起，编译器通常可以从构造函数参数推导出模板参数，从而允许你省略尖括号 `<Key>` 部分。

作为 unordered_set 的模板参数，至少需要键——即元素类型 Key——例如 `unordered_set<int>`：

- Key，用于搜索的键类型
- 可选的 Hash，用于 Key 的哈希函数对象；默认是 `std::hash<Key>`
- 可选的 KeyEqual，用于 Key 的比较运算符；默认是 `std::equal_to<Key>`，因此就是 `operator==`
- 可选的 Allocator，用于元素的内存分配器

可选地，指定哈希函数对象、键的比较函数对象和分配器。如清单 24.78 所示，如果你没有提供比较函数对象，标准库将使用 `operator==` 自由函数。这意味着，对于自定义数据类型，`friend bool operator==` 或带有 `= default` 的 `operator<=>` 就足够了。因此，在大多数情况下，不需要指定比较函数对象。实际上，剩下的就是哈希函数，你有时需要定义它。你也会在清单 24.78 中看到这样的例子。最简单的方法是使用 lambda 和 decltype：

```cpp
auto h = [](const auto &a) { return ...; };
unordered_set<Key,decltype(h)> data( ... h );
```

你可以提供与 `set` 和其他容器类似的构造函数参数，如下所示：

- 无参数
- 使用一对迭代器从另一个容器指定一个范围
- 初始化列表
- 如果你使用 C++23，可以使用标签 `from_range` 和一个范围
- 另一个用于拷贝的 `unordered_set`

除最后两种变体外，所有形式都可以选择传入一个 `size_t`，用来设置哈希表的初始大小。

下面通过一个简单的示例来说明，如清单 24.79 所示。

```cpp
// https://godbolt.org/z/j16P6MjoWr
#include <set>
template<typename Key>
std::set<Key> sorted(const unordered_set<Key>& data)
{ return std::set<Key>(data.begin(), data.end()); }
// ...
// without arguments
unordered_set<int> empty{};
cout << empty;    // Output:
// initializer list
unordered_set data{1,1,2,2,3,3,4,4,5,5}; // duplicates are not included
cout << data;     // Output approximately: 5 4 3 2 1
// copy
unordered_set copy(data);
cout << copy;      // Output approximately: 5 4 3 2 1
// Range
auto so1 = sorted(data);
unordered_set range(std::next(so1.begin()), std::prev(so1.end()));
cout << range;    // Output approximately: 2 3 4
```

**清单 24.79** 这是初始化 “unordered_set” 的几种方式。

请注意，在你的环境中，元素的顺序可能有所不同。为了确保在拷贝最后一个示例时跳过 1 和 5，我使用 `sorted()` 将 unordered_set 数据拷贝到了有序容器 so1 中。为此，我定义了那个辅助函数。

所有插入操作都可能导致容器中的迭代器失效。但是，如果你确定没有发生元素重排，那么迭代器仍然是有效的——例如，因为你之前恰当地调用了 `reserve` 方法。

## 访问

与 `set` 不同，*无序关联容器*只提供*前向*迭代器，正如我在表 24.2 中已经展示的那样。因此它们完全不适合排序：

- **通过迭代器访问**  
  你可以使用 `begin()` 和 `cbegin()` 获得指向开头的迭代器，使用 `end()` 和 `cend()` 获得指向容器末尾之后位置的迭代器。当你随后使用 `++it`、`next(it)` 或 `advance` 遍历元素时，它们的顺序是任意的，但只要你在此期间没有修改容器，多次遍历的顺序是稳定的。

- **通过搜索访问**  
  对于无序关联容器，某些搜索函数（如有序容器中可用的那些）没有意义；对两个不同键的搜索并不能真正构成一个范围。所以你只有 `find`、`count`、`contains` 和 `equal_range`。在 `unordered_set` 中，`count` 返回 0 或 1。`equal_range` 要么包含一个恰好有一个元素的范围，要么两次返回 `end()`。

对于无序关联容器，没有具体键的搜索是不可能的，因为搜索需要哈希值，而哈希值需要一个特定的键。

## 删除

删除方法与 `set` 相同，但接口略有受限：

- **删除所有元素**  
  使用 `clear()` 清空 `unordered_set`。

- **删除或转移单个元素**  
  你可以使用迭代器或键作为参数来查找每个元素。返回值是指向被删除元素之后那个元素的迭代器。使用 `extract`，你可以移除一个元素，并可随后用 `insert` 将其插入其他地方。

- **删除多个元素**  
  你可以用两个迭代器为 `erase` 指定多个元素，但 `unordered_set` 内部的无序性使得这种操作只有部分意义，除非你使用 `begin()` 和 `end()` 作为参数，而这种情况下用 `clear()` 更好。

未被删除元素的迭代器保持有效。

此外，删除操作不会影响剩余元素之间的相对顺序。这意味着你可以在循环中删除多个元素，而不必担心某次删除操作会不会改变剩余元素的顺序，导致你再也看不到某些元素。
