
`compare("hi", "mom");` // 调用带有两个非类型参数的模板

// 处理字符数组指针的 compare 特化版本

```cpp
template <>
int compare(const char* const &p1, const char* const &p2)
{
    return strcmp(p1, p2);
}
```

![](img/3a7e14b77396239ca7166fc2adb32975_1363_0.png)

```cpp
// 打开 std 命名空间以便我们可以特化 std::hash
namespace std {
} // 关闭 std 命名空间；大括号后不加分号
// 打开 std 命名空间以便我们可以特化 std::hash
namespace std {
{
```

```cpp
size_t
hash<Sales_data>::operator() (const Sales_data& s) const {
    return hash<string>(s.bookNo) ^
           hash<unsigned>(s.units_sold) ^
           hash<double>(s.revenue);
}
```

```cpp
// 关闭 std 命名空间；大括号后不加分号
// 使用 hash<Sales_data> 和 Sales_data operator== = 来自 14.3.1 (p. 561)
unordered_multiset<Sales_data> S;
template <class T> class std::hash; // 需要声明
class Sales_data {
    friend class::hash<Sales_data>;
    // 之前的成员
};
```

```cpp
// 原始的最通用模板
template <class T> struct remove_reference {
    typedef T type;
};
// 用于左值和右值引用的部分特化
template <class T> struct remove_reference<T&> // 左值引用
{ typedef T type;};
template <class T> struct remove_reference<T&&> // 右值引用
{ typedef T type;};
```

```cpp
int i;
// decltype(42) 是 int，使用原始模板
remove_reference<decltype(42)>::type a;
// decltype(i) 是 int&，使用 (T&) 部分特化
remove_reference<decltype(i)>::type b;
// decltype(std::move(i)) 是 int&&，使用 (T&&) 部分特化
remove_reference<decltype(std::move(i))>::type c;
```

# C++ Primer, 第五版

```cpp
template<typename T> struct Foo {
    Foo(const T &t) : mem(t) {
    void Bar() { /* ... */ }
    T mem;
    const ... *ptr;
    // Foo 的其他成员
};
template<> // 我们正在特化模板
void Foo<int>::Bar() { // 在特化 Foo<int> 的成员
    // 适用于 int 的处理
    Foo<string> fs; // 实例化 Foo()
    fs.Bar();
    Foo<int> fi; // 实例化 Foo()
    fi.Bar();
}
// 代表一次交易：ISBN，每本书的价格
tuple<size_t, size_t, size_t> item = make_tuple("978-0-13-1163", 42, 0);
auto book = get<0>(item); // 返回 item 的第一个成员
auto cnt = get<1>(item); // 返回 item 的第二个成员
auto price = get<2>(item); // 返回 item 的最后一个成员
get<2>(item) = 0; // 应用 20% 折扣
// 返回对象中成员的数量
size_t sz = decltype(item):value; // trans 是 item 的类型
// 与第二个成员类型相同
tuple<size_t, size_t, size_t> trans = get<1>(item); // cnt 是 int
tuple<string, string> duo = make_tuple("1", "2"); //
tuple<size_t, size_t, size_t> duo = make_tuple(1, 2); //
bool b = (duo == duo); // 错误：不能比较 size_t 和 string
tuple<size_t, size_t, size_t> three = make_tuple(1, 2, 3); // 错误：成员数量不同
tuple<size_t, size_t, size_t> origin = make_tuple(0, 0); // 好：b 为 true
// files 中的每个元素存储特定 store 的交易
vector<vector<Sales_data>> data;
```

```cpp
// matches 有三个成员：store 的索引和该 store vector 的迭代器
typedef tuple<vector<Sales_data>::size_type,
              vector<Sales_data>::const_iterator,
              vector<Sales_data>::const_iterator> matches;
// files 保存每个 store 的交易
// findBook 返回每个销售该书籍的 store
vector<matches> findBook(const vector<Sales_data>& files,
                         const string &book)
{
    vector<matches> ret; // 初始化为空
    // 为每个 store 查找匹配的书范围（如果有）
    for (auto it = files.begin(); it != files.end(); ++it) {
        // 查找相同 ISBN 的 Sales_data 范围
        auto found = equal_range(it->begin(), it->end(),
                                 book, compare);
        if (found.first != found.second) // 此 store 有销售
            // 记住此 store 的索引和匹配范围
            ret.push_back(tuple(it - files.begin(), found.first, found.second));
    }
    return ret; // 如果未找到匹配项则为空
}
void reportResults(ostream &in, ostream &os,
                   const vector<Sales_data>&files) {
    string s; // 要查找的书
    while (in >> s) {
        auto trans = findBook(files, s); // 销售此书籍的 store
        if (trans.empty()) {
            cout << s << " not found in any stores" << endl;
            continue; // 获取下一个查找的书
        }
        for (const auto &store : trans) { // 对于每一个销售的 store
            // 从 tuple 中 get<n> 指定的成员到 store
            os << " store " << get<0>(store) << " sales: "
               << accumulate(get<1>(store), get<2>(store),
                             Sales_data(s))
               << endl;
        }
    }
}
bit32_t bitvec(1U); // 32 位；低位为 1，其余位为 0
// bitvec1 比初始化值小；初始化值的高位被丢弃
bit13_t bit13(0xef); // 位为 1111011101111
// bitvec2 比初始化值大；bitvec2 的高位设置为零
bit32_t bit20(0xef); // 位为 00001011111111111
// 在 long long 为 64 位的机器上，0ULL 是 64 个1
bit128_t bitvec3(0ULL); // 位 0...63 为 0；64...127 为零
bit32_t bit32(0x3); // 位 2 和 3 为 1，所有其他为 0
string s("111111111100001100");
bit32_t bitvec5(s, 5, 4); // 从 s[5] 开始的 4 位，1100
bit32_t bitvec6(s, s.size()-4); // 使用最后四个字符
```

```cpp
bitset<32> bitvec(10); // 32位；低位位为 1，其余位为 0
```

```cpp
bool is_set = bitvec.any(); // true，有一个位被置1
bool is_not_set = bitvec.none(); // false，有一个位被置1
```

```cpp
bool all_set = bitvec.all(); // false，只有一个位被置1
size_t sz = bitvec.count(); // 返回 1
```

```cpp
size_t tz = bitvec.size(); // 返回 32
bitvec.flip(); // 反转 bitvec 中所有位的值
```

```cpp
bitvec.reset(); // 将所有位置为 0
bitvec.set(); // 将所有位置为 1
```

```cpp
bitvec.flip(0); // 反转第一位的值
bitvec.set(bitvec.size()-1); // 开启最后一位
```

```cpp
bitvec.set(0, 0); // 关闭第 0 位
bitvec.reset(0); // 关闭第 0 位
```

```cpp
bitvec.test(0); // 返回 false，因为第一位是关闭的
bitvec[0] = 0; // 关闭位置 0 的位
```

```cpp
bitvec[31] = bitvec[0]; // 将该位设置为与第一位相同的值
bitvec[0].flip(); // 反转位置 0 的位的值
```

```cpp
-bitvec[0]; // 等效操作；反转位置 0 的位
bool b = bitvec[0]; // 将 bitvec[0] 的值转换为 bool
```

```cpp
unsigned long ulong = bitvec.to_ulong();
cout << "ulong = " << ulong << endl;
```

```cpp
cin >> bits; // 从 char 读取最多 16 个或 0 个字符
cout << "bits: " << bits << endl;
```

bool status; // 使用版本位运算符

```cpp
unsigned long quizA = 0; // 此值被用作位集合
quizA |= 1UL << 27; // 表示编号 27 通过了
status = quizA & (1UL << 27); // 检查编号 27 学生的情况
quizA &= ~(1UL << 27); // 编号 27 学生失败
```

// 使用 bitset 库的等效操作

```cpp
bitset<30> quizB; // 每个学生分配一个位；所有位初始化为 0
quizB[27]; // 表示编号 27 通过了
status = quizB[27]; // 检查编号 27 学生的情况
quizB.reset(27); // 编号 27 学生失败
```

// 查找 c 以外的字符之后的字符

```cpp
string pattern = "[c][[:alpha:]]+"; // 我们想要匹配模式所在的整个单词
pattern = "[[:alpha:]].*" + pattern + "[[:alpha:]]+"; // 构建正则以查找模式
```

// 定义一个包含文本且不匹配模式的字符串

```cpp
string test_str = "receipt freind theif receive"; // 如果存在匹配
if (regex_search(test_str, r)) // 定义一个对象来存储搜索结果
cout << results.str() << endl; // 打印匹配的单词
```

# C++ Primer, 第一版

```cpp
// 一个或多个字母数字字符后跟着一个 '.'，然后是 'cpp' 或 'cxx' 或 'cc'
```

```cpp
regex r("[:alnum:]]+\.(cpp|cxx|cc)\$", regex::icase);
```

```cpp
smatch results;
```

```cpp
string filename;
```

```cpp
    if (regex_search(filename, results, r))
```

```cpp
        cout << results.str(0) << endl; // 打印当前匹配项
```

```cpp
    try {
        // 错误：alnum 后缺少括号；构造函数将
        regex r("[:alnum:]:]+\.(cpp|cxx|cc)\$", regex::icase);
    } catch (regex_error e) {
        cout << "code: " << e.code() << endl;
        regex r("[:alnum:]:]+\.(cpp|cxx|cc)\$", regex::icase);
        smatch results;
        // 将匹配字符串输入序列，但不是 char // 错误：输入
        if (regex_search("myfile.cpp", results, r)) {
            cout << results.str(0) << endl; // 将匹配数组序列
            smatch results;
            if (regex_search("myfile.cpp", results, r)) {
                cout << results.str(0) << endl; // 打印当前匹配项
            }
        }
    }
```

// 查找 c 以外的字符之后的字符

```cpp
string pattern = "c[[:alpha:]]+\+";
// 我们想要模式中的整个单词出现
pattern = "[[:alpha:]]+\+" + pattern + "[[:alpha:]]+\+;
regex r(pattern, regex::icase); // 我们在匹配时将忽略大小写
// 它将反复调用 regex_search 来查找文件中所有匹配项
for (sregex_iterator it(file.begin(), file.end(), r), end_it; it != end_it; {
    cout << it->str() << endl; // 匹配的单词
}
// 像之前一样在右侧写入代码
for (sregex_iterator it(file.begin(), file.end(), r), end_it; it != end_it; {
    auto pos = it->prefix(); // 前缀的大小
    pos = pos > 40 ? 40 : pos; // 我们想要 40 个字符
    cout << "\n" << it->str().substr(pos) // 匹配的前缀
    cout << it->suffix().substr(0, 40) // 后缀的第一
// 两个表达式：第一个是点之前的名称
// 第二个是文件后缀
regex r("[:alnum:]]+\.(cpp|cxx|cc)\$", regex::icase);
```
