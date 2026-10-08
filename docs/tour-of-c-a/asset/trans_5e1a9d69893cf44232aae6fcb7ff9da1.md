

```cpp
copy(v, oo);
ranges::copy(v, oo);
using ranges::copy(v, oo);
copy(v, oo);
```

// 可能存在义
// OK
// 从此处起 copy(v, oo) OK
// OK

```cpp
set<string> b{ii, eos};
copy(b, oo);
```

// 从输入中收集字符串
// 将缓冲区拷贝到输出

```cpp
int main()
{
    string from, to;
    cin >> from >> to;
```

// 获取源和目标文件名

```cpp
ifstream is{from};                   // 文件 "from" 的输入流
ofstream os(to);                    // 文件 "to" 的输出流

set<string> b{istream_iterator<string>{is}, istream_iterator<string>{}}; // 读取输入
copy(b, ostream_iterator<string>{os, "\n"});          // 拷贝到输出

return !is.eof() || !os;                            // 返回错误状态 (§1.2.1, §11.4)
}
```

```cpp
void f(map<string, int>& m)
{
    auto p = find_if(m, Greater_than{42});
    // ...
}
```

```cpp
struct Greater_than {
    int val;
    Greater_than(int v) : val{v} { }
    bool operator()}(const pair<int, string>& r) const { return r.second > val; }
};
```

```cpp
auto p = find_if(m, [](const auto& r) { return r.second > 42; });
```

```cpp
vector<int> v = {0,1,2,3,4,5};
for_each(v, [](int& x){ x = x*x; }); // v==={0,1,4,9,16,25}
for_each(v.begin(), v.begin() + 3, [](int& x){ x = sqrt(x); }); // v==={0,1,2,9,16,25}
```

```cpp
sort(v.begin(), v.end());           // 顺序
sort(seq, v.begin(), v.end());     // 顺序（同默认）
sort(par, v.begin(), v.end());        // 并行
sort(par_unseq, v.begin(), v.end());  // 并行和或向量化
```

```cpp
void sort(auto pol, random_access_range auto& r)
{
    sort(pol, r.begin(), r.end());
}
```

```cpp
template<forward_range R>
    requires sortable<iterator_t<R>>
void my_sort(R& r) // 现代的、受概念限制的 my_sort
{
    return my_sort(r.begin(), r.end()); // 使用 1994 式的 sort
}
```

```cpp
void user(forward_range auto& r)
{
    filter_view v{r, [](int x) { return x % 2; } }; // 从 r 中过滤（仅）奇数数

    cout << "odd numbers: ";
    for (int x : v) {
        cout << x << ' ';
    }
}
```

```cpp
void user(forward_range auto& r)
{
    filter_view v{r, [](int x) { return x % 2; } };
    take_view tv{v, 100};

    cout << "odd numbers: ";
    for (int x : tv) {
        cout << x << ' ';
    }
}
```

```cpp
for (int x : take_view{ filter_view { r, [](int x) { return x % 2; } }, 3 })
cout << x << ' ';
```

```cpp
auto bad()
{
    vector v{1, 2, 3, 4};
    return filter_view{v};
}
// v 在 view 之前被析毁了
```
struct Reading {
    int location;
    int temperature;
    int humidity;
    int air_pressure;
    // ...
};
```

```cpp
int average_temp(vector<Reading> readings)
{
    if (readings.size() == 0) throw {};
    double s = 0;
    for (int x : readings)
        s += x;
    return s / readings.size();
}
```

```cpp
for (int x : iota_view{42, 5})
    cout << x << ' ';
```

```cpp
for (auto x : istream_view<complex<double>>cin})
    cout << x << '\n';
```

```cpp
auto cpx = istream_view<complex<double>>(cin);

for (auto x : transform_view{cpx, [](auto z){ return z; }})
    cout << x << '\n';
```

```cpp
void user(forward_range auto& r)
{
    auto odd = [](int x) { return x % 2; };

    for (int x : r | filter(odd) | take(3))
        cout << x << ' ';
}
```

```cpp
void user(forward_range auto& r)
{
    using namespace views;

    auto odd = [](int x) { return x % 2; };

    for (int x : r | filter(odd) | take(3))
        cout << x << ' ';
}
```

```cpp
void user(forward_range auto& r)
{
    int count = 0;
    for (int x : r) {
        if (x % 2) {
            cout << x << ' ';
            if (++count == 3) return;
        }
    }
}
```

```cpp
common_type<string, const char*> s1 = some_fct();
common_type<string, const char*> s2 = some_other_fct();

if (s1 == s2) {
    // ...
}
```

```cpp
using common_type_t<Bigint, long> = Bigint; // 一个合适的 Bigint 定义
```

```cpp
template<class Iter>
class Sentinel {
public:
    Sentinel(int ee) : end(ee) {}
    Sentinel() : end(0) {} // sentinel_for 需要默认构造函数

    friend bool operator==(const Iter& p, Sentinel s) { return *p == s.end); }
    friend bool operator!=(const Iter& p, Sentinel s) { return !(p == s); }
private:
    iter_value_t<const char*> end; // 哨兵值
};
```

```cpp
static_assert(sentinel_for<Sentinel<const char*>, const*>>); // 为 C 风格字符串检查 Sentinel
```

```cpp
const char aa[] = "Hello, World!\nBye for now\n";

ranges::for_each(aa, Sentinel<const char*>('\n'), [](char x) { cout << x; });
```

```cpp
mutex m; // 用于保护共享数据

void f()
{
    scoped_lock lck{m}; // 获取互斥 m
    // ... 操作共享数据 ...
}
```

```cpp
void f(int i, int j)    // X* 与 unique_ptr<X>
{
    X* p = new X;               // 分配一个新的 X
    unique_ptr<X> sp{new X};      // 分配一个新的交给 unique_ptr
    // ...
    if (i < 99) throw {};
    if (j < 77) return;
    // ... 使用 p 和 sp ..
    delete p;
}
// 可能抛出异常
// 可能提前返回
// 析毁 *p
```

```cpp
void f(int i, int j) // 使用局部变量
{
    X x;
    // ...
}
```

```cpp
unique_ptr<X> make_X(int i)
    // 创建一个 X 并立即交给 unique_ptr
{
    // ... 检查 i 等等 ...
    return unique_ptr<X>{new X{i}};
}
```

```cpp
void f(shared_ptr<fstream>);
void g(shared_ptr<fstream>);

void user(shared_ptr<fstream> fs)
{
    if (fs)
        // ...
}
```

