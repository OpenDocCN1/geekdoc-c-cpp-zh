

```cpp
void silly(vector<Entry>& book)
{
    int i = book[book.size()].number;
    // ...
}
```

// book.size() 超出范围

```cpp
template<typename T>
struct Vec : std::vector<T> {
    using vector<T>::vector; // 我使用了 vector 的构造函数（使用 Vec 命名）
    T& operator[](int i) { return vector<T>::at(i); } // 范围检查
    const T& operator[](int i) const { return vector<T>::at(i); } // 范围检查常量对象；§5.2.1
    auto begin() { return Checked_iter<vector<T>>{*this}; // 我看到 §13.1
    auto end() { return Checked_iter<vector<T>>{*this, vector<T>::end()};
};
```

```cpp
void checked(Vec<Entry>& book)
{
    try {
        book[book.size()] = {"Joe",999999}; // 我将抛出一个异常
        // ...
    }
    catch (out_of_range&) {
        cerr << "range error\n";
    }
}
```

```cpp
int main() {
try {
    // 你的代码
}
catch (out_of_range&) {
    cerr << "range error\n";
}
catch (...) {
    cerr << "unknown exception thrown\n";
}
```

```cpp
list<Entry> phone_book = {
    "David Hume",123456,
    "Karl Popper",234567,
    "Bertrand Arthur William Russell",345678
};
```

```cpp
int get_number(const string& s)
{
    for (const auto& x : phone_book)
        if (x.name==s)
            return x.number;
    return 0; // 使用 0 表示“未找到号码”
}
```

```cpp
int get_number(const string& s)
{
    for (auto p = phone_book.begin(); p!=phone_book.end(); ++p)
        if (p->name==s)
            return p->number;
    return 0; // 使用 0 表示“未找到号码”
}
```

```cpp
void f(const Entry & ee, list<Entry>::iterator p, list<Entry>::iterator q)
{
    phone_book.insert(p,ee);      // 在 p 指向的元素之前插入 ee
    phone_book.erase(q);          // 删除 q 指向的元素
}
```

```cpp
map<string,int> phone_book = {
    {"David Hume",123456},
    {"Karl Popper",234567},
    {"Bertrand Arthur William Russell",345678}
};
```

```cpp
int get_number(const string& s)
{
    return phone_book[s];
}
```

```cpp
unordered_map<string,int> phone_book = {
    {"David Hume",123456},
    {"Karl Popper",234567},
    {"Bertrand Arthur William Russell",345678}
};
```

```cpp
int get_number(const string& s)
{
    return phone_book[s];
}
```

```cpp
struct Record {
    string name;
    int product_code;
    // ...
};
```

```cpp
struct Rhash { // 用于 Record 的哈希函数
    size_t operator()(const Record& r) const
    {
        return hash<string>()(r.name) ^ hash<int>()(r.product_code);
    }
};
```

unordered_set<Record,Rhash> my_set; // 使用 Rhash 查询的 Records 集合

```cpp
namespace std {
    // 我为 Record 制作了一个哈希函数
    template<> struct hash<Record> {
        using argument_type = Record;
        using result_type = size_t;

        result_type operator()(const Record& r) const
        {
            return hash<string>()(r.name) ^ hash<int>()(r.product_code);
        }
    };
}
```

```cpp
struct Event {
    vector<int> data = vector<int>(512);
};

list<shared_ptr<Event>> q;

void producer()
{
    for (int n = 0; n!=LOTS; ++n) {
        lock_guard lk{m}; // m 是一个互斥锁；见 §18.3
        q.push_back(make_shared<Event>());
        cv.notify_one(); // cv 是条件变量；见 §18.4
    }
}
```

```cpp
pmr::synchronized_pool_resource pool; // 创建一个池
struct Event {
    vector<int> data = vector<int>{&pool}; // 让 Event 使用池
};
list<shared_ptr<Event>> q{&pool}; // 让 q 使用池
```

```cpp
void producer()
{
    for (int n = 0; n!=LOTS; ++n) {
        scoped_lock lk{m}; // m 是一个互斥锁 (§18.3)
        q.push_back(make_shared<Event>(pmr::polymorphic_allocator(&pool)));
        }
```
*(注：原文文本中 `producer` 函数部分似乎存在截断或逻辑重复，已根据提供的代码片段进行了最程度的翻译和对齐)*

