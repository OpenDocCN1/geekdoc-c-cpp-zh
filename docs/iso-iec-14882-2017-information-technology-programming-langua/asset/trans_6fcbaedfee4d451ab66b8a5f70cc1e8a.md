

# ISO/IEC 14882:2017(E)

```cpp
template<class charT, class traits, class Allocator>
bool operator()(const charT& lhs,
    const basic_string<charT, traits, Allocator>& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
bool operator()(const basic_string<charT, traits, Allocator>& lhs,
    const basic_string<charT, traits, Allocator>& rhs) noexcept;
template<class charT, class traits, class Allocator>
bool operator()(const basic_string<charT, traits, Allocator>& lhs,
    const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
bool operator()(const basic_string<charT, traits, Allocator>& lhs,
    const charT& rhs);
template<class charT, class traits, class Allocator>
bool operator()(const basic_string<charT, traits, Allocator>& lhs,
    const basic_string<charT, traits, Allocator>& rhs) noexcept;
template<class charT, class traits, class Allocator>
bool operator()(const basic_string<charT, traits, Allocator>& lhs,
    const charT& rhs);
```

```cpp
template<class charT, class traits, class Allocator>
bool operator()(const basic_string<charT, traits, Allocator>& lhs,
    const basic_string<charT, traits, Allocator>& rhs);
```

// 24.3.3. swap

```cpp
template<class charT, class traits, class Allocator>
void swap(const basic_string<charT, traits, Allocator>& lhs,
    basic_string<charT, traits, Allocator>& rhs) noexcept(noexcept(swap(lhs,rhs)));
```

// 24.3.9. 插入与迭代器构造函数

```cpp
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>& operator>>(const basic_istream<charT, traits>& is,
    const basic_string<charT, traits, Allocator>& str);
template<class charT, class traits, class Allocator>
basic_ostream<charT, traits>& operator<<(const basic_ostream<charT, traits, Allocator>& os,
    const basic_string<charT, traits, Allocator>& str);
    
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>& operator>>(const basic_istream<charT, traits>& is,
    const charT& delim);
```

```cpp
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>& operator>>(const basic_istream<charT, traits>& is,
    const basic_string<charT, traits, Allocator>& str,
    const charT& delim);
```

```cpp
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>& operator>>(const basic_istream<charT, traits>& is,
    const basic_string<charT, traits, Allocator>& str,
    const charT& delim);
```

```cpp
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>& operator>>(const basic_istream<charT, traits>& is,
    const basic_string<charT, traits, Allocator>& str);
```

```cpp
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>&& is,
```

### § 24.3.1

basic_string<charT, traits, Allocator> str;

```cpp
// basic_string 类型别名
using string = basic_string<char>;
using u16string = basic_string<char16_t>;
using u32string = basic_string<char32_t>;
using wstring = basic_string<wchar_t>;

// 23.3.4. 数值转换
int stoi(const string& str, size_t idx = nullptr, int base = 10);
long stol(const string& str, size_t idx = nullptr, int base = 10);
long stoul(const string& str, size_t idx = nullptr, int base = 10);
long stoll(const string& str, size_t idx = nullptr, int base = 10);
float stof(const string& str, size_t idx = nullptr);
double stod(const string& str, size_t idx = nullptr);
long double stold(const string& str, size_t idx = nullptr);
string to_string(int val);
string to_string(unsigned val);
string to_string(long val);
string to_string(unsigned long val);
string to_string(long long val);
string to_string(unsigned long long val);
string to_string(float val);
string to_string(double val);
string to_string(long double val);

int wstoi(const wstring& str, size_t idx = nullptr, int base = 10);
long wst(const wstring& str, size_t idx = nullptr, int base = 10);
long wstoul(const wstring& str, size_t idx = nullptr, int base = 10);
long wtol(const wstring& str, size_t idx = nullptr, int base = 10);
long wstoll(const wstring& str, size_t idx = nullptr, int base = 10);
float stof(const wstring& str, size_t idx = nullptr);
double stod(const wstring& str, size_t idx = nullptr);
long double wstold(const wstring& str, size_t idx = nullptr);
wstring to_string(int val);
wstring to_string(unsigned val);
wstring to_string(long val);
wstring to_string(unsigned long val);
wstring to_string(long long val);
wstring to_string(unsigned long long val);
wstring to_string(float val);
wstring to_string(double val);
wstring to_string(long double val);
```

```cpp
// 23.3.5. 哈希支持
template<class T> struct hash;
template<class> hash<string>;
template<class> hash<u16string>;
template<class> hash<u32string>;
template<class> hash<wstring>;
```

```cpp
namespace std {
    template<class charT, class traits = char_traits<charT>, class Allocator = allocator<charT>>
    using basic_string = basic_string<charT, traits, Allocator>;

    using string = basic_string<char>;
    using u16string = basic_string<char16_t>;
    using u32string = basic_string<char32_t>;
    using wstring = basic_string<wchar_t>;
}

inline namespace literals {
    // 24.3.6. basic_string 后后缀
    string operator""(const char* s, size_t len);
    u16string operator""(const char16_t* s, size_t len);
    u32string operator""(const char32_t* s, size_t len);
    wstring operator""(const wchar_t* s, size_t len);
}

## 24.3.2 类模板 basic_string

template basic_string 描述存储任意数量字符对象的序列，第一个元素位于位置零。如果其包含的字符对象的类型上下文中明确，则该序列被称为“string”。在本条款中，其包含的字符对象的类型由 Allocator 类指定，用于分配和释放存储。在所有情况下，本条款描述的函数报告两种错误，各对应一种类型：

- (1) 长度错误对应 length_error；
- (2) 范围错误对应 out_of_range。

```cpp
namespace std {
    template<class charT, class traits = char_traits<charT>, class Allocator = allocator<charT>>
    class basic_string {
    public:
        // 类型
        using traits_type = traits;
        using value_type = charT;
        using allocator_type = Allocator;
        using size_type = typename allocator_traits<Allocator>::size_type;
        using difference_type = typename allocator_traits<Allocator>::difference_type;
        using pointer = typename allocator_traits<Allocator>::pointer;
        using const_pointer = typename allocator_traits<Allocator>::const_pointer;
        using reference = value_type&;
        using const_reference = value_type&;

        using iterator = implementation_defined;
        using const_iterator = implementation_defined;
        using reverse_iterator = std::reverse_iterator<iterator>;
        using const_reverse_iterator = std::reverse_iterator<const_iterator>;
        static const size_type npos = -1;

        Allocator::value_type 不能与 charT 同名。
};
}
```

```cpp
basic_string() noexcept(noexcept(Allocator())) : basic_string(Allocator()) {}
basic_string(const Allocator& a) noexcept;
basic_string(const basic_string& str) noexcept;
basic_string(const basic_string& str, size_type pos, const Allocator& a = Allocator());
basic_string(const basic_string& str, size_type pos, size_type n, const Allocator& a = Allocator());

template<class T>
basic_string(const T& t, size_type pos, size_type n, const Allocator& a = Allocator());
explicit basic_string(const basic_string_view<T> sv, const Allocator& a = Allocator());
basic_string(const char* s, size_type n, const Allocator& a = Allocator());
basic_string(const char* s, const char* c, const Allocator& a = Allocator());
template<class InputIterator>
basic_string(InputIterator begin, InputIterator end, const Allocator& a = Allocator());
basic_string(initializer_list<charT> l, const Allocator& a = Allocator());
basic_string(const basic_string& str, const Allocator& a = Allocator());
basic_string(const basic_string& str, const Allocator& a = Allocator());

-basic_string();

basic_string& operator=(const basic_string& str)
    noexcept(allocator_traits<Allocator>::propagate_on_container_assignment::value ||
    allocator_traits<Allocator>::is_always_equal::value);
basic_string& operator=(const basic_string_view<charT> sv);
basic_string& operator=(const char* c);
basic_string& operator=(const char* s);
basic_string& operator=(initializer_list<charT>);
```

### 24.3.3. 迭代器

```cpp
iterator begin() const noexcept;
const_iterator begin() const noexcept;
iterator end() const noexcept;
const_iterator end() const noexcept;
```

```cpp
reverse_iterator begin() const noexcept;
const_reverse_iterator rbegin() const noexcept;
reverse_iterator rend() const noexcept;
const_reverse_iterator rend() const noexcept;
```

```cpp
const_iterator cbegin() const noexcept;
const_iterator end() const noexcept;
const_reverse_iterator crbegin() const noexcept;
const_reverse_iterator crend() const noexcept;
```

### 24.3.4. 容量

```cpp
size_type size() const noexcept;
size_type length() const noexcept;
size_type max_size() const noexcept;
void resize(size_type n, charT c);
void resize(size_type n);
size_type capacity() const noexcept;
void reserve(size_type arg = 0);
```

