
- **不指定特定键进行搜索**  
  如果在搜索过程中为合适的比较函子配备 `is_transparent`，就可以省去创建具体搜索键，如清单 24.70 中对 set 所示。

下面的清单给出了一些访问 multiset 的示例。

```cpp
// https://godbolt.org/z/fWGrbbYa7
#include <string>
#include <iterator> // distance
#include <ranges>   // subrange
struct Person {
    std::string name;
    friend bool operator<(const Person &a, const Person &b) {
        // only first letter
        return a.name.size()==0 ? true
             : (b.name.size()==0 ? false : a.name[0] < b.name[0]);
    }
};
// ...
multiset<int> data{ 1, 4,4, 2,2,2, 7, 9 };
auto [from1, to1] = data.equal_range(2);
cout << "Number of 2s: "
     << std::distance(from1, to1) << '\n';    // Output: Number of 2s: 3
auto [from2, to2] = data.equal_range(5);
cout << "Number of 5s: "
     << std::distance(from2, to2) << '\n';    // Output: Number of 5s: 0
multiset<Person> room{
    {"Karl"}, {"Kurt"}, {"Peter"}, {"Karl"}, {"Ken"}};
auto [p, q] = room.equal_range(Person{"K"});
for(auto& p : std::ranges::subrange(p,q)) { // C++20 range or simple loop
    cout << p.name << ' ';
}
cout << '\n'; // Output: Karl Kurt Karl Ken
```

**清单 24.70** “multiset” 的搜索函数会查找匹配元素的范围。

在 `room` 示例中，借助合适的 `operator<`，你确实可以把 `multiset` 中实际不同的元素视为相等。例如这里只比较名字的首字母。当你用 `room.equal_range(Person{"K"})` 搜索时，所有以 `K` 开头的名字都会落在返回的范围内。请注意，定义的 `operator<` 也用于内部排序，因此排序时只使用名字的首字母。这就是为什么未按顺序排列的“K...”名字会出现在搜索结果中。

`equal_range` 的返回值是一个 `pair`，从 C++17 起，可以使用结构化绑定将其赋给两个新变量。在 C++17 之前，你会使用 `auto x`，然后使用 `x.first` 或 `x.second`。

### 删除

与 set 一样，使用 erase 或 clear 进行删除：

- **删除所有元素**  
  使用 `clear()` 可删除所有内容。
- **删除或转移单个元素**  
  如果提供迭代器，`erase` 会删除单个元素；否则会删除与给定搜索键匹配的所有元素。  
  如果你之后想在其他位置 `insert` 它，`extract` 也能做到这一点。
- **删除多个元素**  
  以两个迭代器作为参数时，你会像使用 `set` 一样删除多个元素。

所有未被删除元素的迭代器都保持有效。

## 24.7.6 “multimap”

multimap 有两个相关容器：与 map 的共同点是，每个条目都由一个键和一个目标组成。来自 multiset 的特性是键可以出现多次。因此，`multimap<int,string>` 可以在键 7 下同时存储目标 "sieben" 和目标 "seven"，如图 24.13 所示。

因此我将简要介绍，并请你参阅第 24.7.4 节和第 24.7.5 节以获取更多信息。

multimap 的接口与 map 相比有一个关键区别：multimap 既不提供 `operator[]`，也不提供 `at`。

本节中 multimap 的示例应视为嵌入在清单 24.71 中。

```cpp
// https://godbolt.org/z/bxW63jPor
#include <map>       // the main thing
#include <iostream>  // for output
#include <string>    // often used for key or target
using std::multimap; using std::cout; using std::string;
template<typename Key, typename Tp, typename Cmp>
std::ostream& operator<<(std::ostream& os, const multimap<Key,Tp,Cmp>&data){
    for(auto &e : data) {
        os << e.first << ": " << e.second << ' ';
    }
    return os << '\n'; //'<<'=instead of '<<' for line break
}
int main() {
    //Example code here
}
```

清单 24.71 这是本节中关于“multimap”的各清单所用的模板。

请注意我在清单 24.12 之后的框中关于 << 的注释。

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_744_0.png)

**图 24.13** 可能存在重复键。

### 元素及其属性

与 map 一样，存储在 `multimap<Key,Target>` 中的元素（键和目标）的类型为 `pair<const Key,Target>`。

键同样使用 `operator<` 保持有序。不过，你也可以提供自己的比较器。

### 初始化

初始化 `multimap` 的方式与 map 一样，不同之处在于重复键会被接受，而不会被忽略。

你可以从以下方式中选择：

- 不带参数的默认构造函数
- 一对用于复制另一个范围的迭代器
- 一个初始化列表，在这种情况下由多个 pair 组成
- 另一个用于复制的 `multimap`
- 从 C++23 起，带有 `from_range` 标签的构造函数

下面的清单展示了初始化 multimap 的示例。

```
// https://godbolt.org/z/6no9dW64d
multimap<int,int>{ std::make_pair(3,4) };  // multimap<int,int>
using namespace std::literals; // for "s"
multimap<int,string> numlang{
    {7,"seven"s}, {6,"six"s},
    {7,"siete"s}, {6,"sechs"s},
    {7,"seven"s}, {7,"yedi"s},
    {8,"eight"s} };
cout << numlang; // Output: 6:six 6:sechs 7:seven 7:siete 7:seven 7:yedi 8:eight
```

**清单 24.72** 所有条目最终都会进入“multimap”中。

如你所见，重复键会被保留。重复的目标在 `map` 中本来自然也是可能的。键始终保持在有序状态，这从输出中可以看出。

### 赋值

与 `map` 一样，`multimap` 有一个 `operator=`，用于之后从另一个 `multimap` 复制或移动。使用 `swap`，你可以快速交换两个 `multimap` 的内容。

`merge` 会在两个 `multimap` 之间转移所有元素，并且不会像 `map` 那样在源容器中留下重复元素。

### 插入

你可以使用 `insert`、`emplace`、`emplace_hint`，以及从 C++23 起也可使用 `insert_range`，将新元素插入 `multimap`。与 `map` 不同，即使新键已经存在，元素也总会被插入。与 `map` 相比，不存在用于自动插入的 `operator[]`：

- **插入单个元素并自动定位**  
  与 `map` 一样，你可以使用 `insert` 向 `multimap` 添加新的 `pair<Key,Target>`。使用 `emplace` 方法时，你直接以参数形式提供 Key 和 Target。与 `map` 不同，这两个方法不会返回表示插入是否成功的 bool，而只返回一个指向插入元素位置的迭代器。这在[清单 24.73](#) 中演示。
- **带位置提示插入单个元素**  
  与 `map` 一样，你可以为 `insert` 提供一个额外的迭代器作为位置提示，或以相同方式使用 `emplace_hint`。如果提示正确，那么插入平均以 O(1) 时间完成。
- **插入多个元素**  
  与 `map` 一样，`multimap` 的 insert 也可以接收一对迭代器。从 C++23 起，你还可以使用 `insert_range`。

下面的清单展示了如何向 `multimap` 插入元素。

```
/// https://godbolt.org/z/dj68ej9r
using namespace std::literals; // for "s"

multimap<int,string> numlang{};
numlang.insert( std::make_pair(7, "seven"s) );
numlang.insert( std::pair<int,string>(7, "sieben"s) );
numlang.emplace( 7, "yedi"s );
cout << numlang; // Output: 7:seven 7:sieben 7:yedi
```

**清单 24.73** “multimap”中的“insert”和“emplace”。

如你所见，相同的键总是被插入到相同键中的最后。

与有序关联容器通常情况一样，`multimap` 的迭代器不受插入操作影响，并保持有效。

### 访问

与 `map` 一样，`multimap` 的迭代器引用 `pair<const Key, Target>`。你可以覆写 `Target`——当然，除非你获得的是 `const_iterator`。

与 `map` 不同，不能通过 `operator[]` 或 `at` 进行类似索引的访问：

- **通过迭代器访问**  
  与 `map` 一样，使用 `begin()` 和 `end()` 方法及其 const 和反向对应版本，可以获得 `multimap` 的双向迭代器。
- **通过搜索访问**  
  与在 `map` 中一样，你可以使用 `find`、`upper_bound`、`lower_bound` 和 `equal_range` 在 `multimap` 中查找键。接口完全相同，不同之处在于 `find` 会找到任意一个匹配的键，而其余方法实际上可以返回包含多个相同键的整个范围。`count` 给出找到的键的数量，从 C++20 起的 `contains` 则给出是否包含该键。

### 删除

与 `map` 相比，删除时几乎没有什么区别，除了按键搜索进行 `erase` 之外：

- **删除所有元素**  
  使用 `clear()` 可删除 `multimap` 的所有元素。
- **删除或转移单个元素**  
  与 `map` 中通常情况一样，`erase` 通过迭代器删除单个元素。

使用 `extract`，你可以删除元素，以便之后用 `insert` 将其插入其他位置：

- **删除单个键**  
  如果指定一个键，那么在 `multimap` 中该键的所有条目都会被移除。对于 `map` 通常也是一样，因为 `map` 中最多只有一个键，但我要特别为 `multimap` 强调这一点。
- **删除多个元素**  
  带有一对迭代器的 `erase` 指的是要删除的多个元素。

下面的清单演示了删除——容器中未被删除元素的迭代器保持有效。

```cpp
// https://godbolt.org/z/TbvKTn4Px
multimap<char,int> vals{ {'c',1}, {'c',8}, {'g',1},
    {'c',1}, {'a',7}, {'a',1}, {'c',2} };
cout << vals;              // Output: a:7 a:1 c:8 c:1 c:2 g:1
```
