

```cpp
cout << lets; // Output: a:4 b:2 c:3
struct comp { // Functor
    bool operator()(char a, char b) const { return toupper(a) < toupper(b); }
};
map<char,int,Comp> lets2; // here the template parameter is sufficient
```

**Listing 24.61** 你也可以为“map”提供自定义的比较函数。

当你定义一个泛形函数（functor）——即一个带有 `operator()` 的类——只需将此类指定为模板参数就足够了。在创建 map 时，将使用其默认构造函数创建一个泛形对象的实例。使用 lambda 时，你已经有了一个可调用的实例。

## Initialize

作为 map 的模板参数，你指定了键（Key）和目标（Target）的类型——例如：

```cpp
map<int,string> // int 作为 Key，string 作为 Target
map<Person,size_t> // Person 到 age
map<unsigned,unsigned> // Key 和 target 类型也可以是相同的
map<int,shared_ptr<Image>> // 指针作为目标
```

可选地，你可以指定键（上一节）的类型以及分配器（allocator）。如果你指定了分配器，可以提供常规构造函数参数。以下变体常用于初始化：

- 默认构造函数创建一个空容器
- 迭代器从另一个容器拷贝范围
- 初始化列表使用显式值初始化
- C++23 的 from_range

通过初始化列表进行填充时，你必须考虑到每个元素都由一个对（pair）。幸运的是，对的也可以通过初始化列表创建，因此构造看起来仍然紧凑，如列表 24.62 所示。

```cpp
// https://cppreference.com/cpp/language/literals
using std::pair;
namespace {
    constexpr pair<char, char> operator ""(const char* s, size_t len) {
        return len==2 ? make_pair(s[0], s[1]) : make_pair(' ');
    }
}
struct O {
    char a;
    int n;
    O(char a, int n) : a(a), n(n) {}
    operator pair<const char, int>() const { return make_pair(a, n); }
};
// 显式对：
map<int, int> nums = {pair<int>(6), make_pair(7,8)};
map<int, int> nums2 = {pair<int>(1,6), make_pair(5,7)};
// 来自初始化列表的隐式对：
map<int, char> num = {{1,'a'}, {2,'b'}, {3,'c'};
map<int, int> nums3 = {{7,2}, {9,4}};
using namespace;
map<char, char> cmap = {"ab", "cd"}; //自定义字面量
cout << cmap; // Output: a:b c:d
map<char,int> qmap = {('a',1), ('b',2), ('c',3)}; // 隐式转换
cout << qmap; // Output: a:1 b:2 c:3
```

**Listing 24.62** 初始化列表必须包含“pair”元素。

正如 qmap 的代码所示，初始化列表的元素可以隐式转换为 `pair<const Key,Target>`。这对于紧凑表示非常有用。

## Assignment

与 set 类似，你可以使用 `operator=` 初始化 map。map 提供了拷贝的重载，虽然没有 `assign` 或 `assign_range` 方法，但像所有其他容器一样，它有 `swap`。

## Insert

就像 set 一样，你可以通过 `insert`、`emplace`、`emplace hint` 以及 C++23 中的 `insert_range` 添加元素。还有 `operator[]` 和 `insert_assign`，它们在某些情况下也可以插入新元素。无论你如何插入，指向 map 的迭代器都保持有效。

### 使用自动定位插入单个元素

在 map 中，单个元素由键和目标的对组成。你随后将其指定为参数。与 set 类似，在这种情况下 `insert` 和 `emplace` 不会覆盖内容。

```cpp
// https://godbolt.org/z/YlebrxbT
map<int,string> pl2zip;
pl2zip.insert(std::make_pair(94103, "San Francisco"));
pl2zip.emplace(10001, "New York");
cout << pl2zip; // Output: 10001:New York 94103:San Francisco
map<string,int> dwarves;
pl2zip.emplace("New York", 10001);
pl2zip.emplace("New York", 10002); // 不覆盖
cout << pl2zip; // Output: New York:10001
```

**Listing 24.63** 你将一个新元素指定为对。

### 自动插入和覆盖

通过 `operator[]`，你可以搜索键。返回值是目标的引用。如果还没有该键的条目，将被新创建。然后将使用默认构造函数 `Target()` 创建一个新的目标。如果 `[]` 出现在赋值的左侧，你可以立即用新目标覆盖新创建的目标。

```cpp
// https://godbolt.org/z/7h3vsWYG
map<string,int> dwarves;
dwarves.emplace("Fii", 2859);
cout << dwarves["Fii"] << "\n"; // Output: 2859
cout << dwarves["Dori"] << "\n"; // Output: 0
dwarves["Fii"] = 3000; // 覆盖
cout << dwarves["Fii"] << "\n"; // Output: 3000
```

**Listing 24.64** 你将一个新元素指定为对。

正如你在 qmap 代码中能看到的，初始化列表的元素可以隐式转换为 `pair<const Key,Target>`。这对于紧凑表示非常有用。

```cpp
// https://cppreference.com/cpp/language/literals
using std::pair;
namespace {
    constexpr pair<char, char> operator ""(const char* s, size_t len) {
        return len==2 ? make_pair(s[0], s[1]) : make_pair(' ');
    }
}
struct O {
    char a;
    int n;
    O(char a, int n) : a(a), n(n) {}
    operator pair<const char, int>() const { return make_pair(a, n); }
};
// 显式对：
map<int, int> nums = {pair<int>(6), make_pair(7,8)};
map<int, int> nums2 = {pair<int>(1,6), make_pair(5,7)};
// 来自初始化列表的隐式对：
map<int, char> num = {{1,'a'}, {2,'b'}, {3,'c'};
map<int, int> nums3 = {{7,2}, {9,4}};
using namespace;
map<char, char> cmap = {"ab", "cd"}; //自定义字面量
cout << cmap; // Output: a:b c:d
map<char,int> qmap = {('a',1), ('b',2), ('c',3)}; // 隐式转换
cout << qmap; // Output: a:1 b:2 c:3
```

**Listing 24.65** 你可以更改目标的值。

## 通过迭代器访问

与所有有序容器一样，你通过 `begin()` 和 `end()` 获取双向迭代器。

```cpp
// https://godbolt.org/z16t5dob7
map<char, int> data = {{'a', 1}, {'b', 2}, {'c', 3}};
for(auto it=data.begin(); it!=data.end(); ++it) { // 反向
    cout << it->first << " : " << it->second << "\n"; // 解引用访问
}
cout << '\n'; // Output: a:1 b:2 c:3
for(auto e : data) { // 正向，使用 begin() 和 end()
    cout << e.first << " : " << e.second << "\n"; // 对，元素访问
}
out << '\n'; // Output: a:1 b:2 c:3
```

**Listing 24.66** “map”的迭代器类型为“pair”。

## 索引式访问

作为关联容器（有序或无序）的特殊特性，map 拥有 `operator[]` 和 `at` 方法，你从 vector 和 array 中了解它们。这允许你像使用索引一样使用 map。与其对应不同，索引不是 `size_t` 类型，而是 `Key` 类型。因此，`operator[]` 和 `at` 的参数是该类型的值。正如列表 24.59 和列表 24.64 所示，`operator[]` 在未找到键时会自动插入元素。`at` 反之在这些情况下会抛出 `out_of_range` 异常。如果你有一个常量 map，你无法使用 `operator[]`，因为它不是

