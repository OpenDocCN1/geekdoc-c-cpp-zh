

# ISO/IEC 14882:2017(E)

```cpp
void shrink_to_fit();
void clear() noexcept;
bool empty() const noexcept;
```

```cpp
// 24.3.2.5. 元素访问
const_reference operator[](size_type pos) const;
operator[](size_type pos);
const_reference at(size_type n) const;
reference at(size_type n);
const char& front() const;
front();
const char& back() const;
back();
```

```cpp
// 24.3.2.6. 修改器
basic_string& operator+=(const basic_string& str);
basic_string& operator+=(basic_string_view<char,traits> sv);
basic_string& operator+=(const char* s);
basic_string& operator+=(char_T c);
basic_string& append(const basic_string& str);
basic_string& append(const basic_string& str, size_type pos, size_type n = npos);
basic_string& append(basic_string_view<char, traits> sv);
template<class T>
basic_string& append(const T& t, size_type pos, size_type n = npos);
basic_string& append(const char* s, size_type n);
basic_string& append(size_type pos, n, char c);
template<class InputIterator>
basic_string& append(InputIterator first, InputIterator last);
basic_string& append(initializer_list<char_T> c);
```

```cpp
void push_back(char c);
basic_string& assign(const basic_string& str);
basic_string& assign(const basic_string& str)
noexcept(allocator_traits<Allocator>::propagate_move_on_assignment::value ||
allocator_traits<Allocator>::is_always_equal::)
basic_string& assign(const basic_string& str, size_type pos, size_type n = npos);
basic_string& assign(basic_string_view<char, traits> sv);
template<class T>
basic_string& assign(const T& t, size_type pos, size_type n = npos);
basic_string& assign(const char* s, size_type n);
basic_string& assign(size_type n, n, char c);
template<class InputIterator>
basic_string& assign(InputIterator first, InputIterator last);
basic_string& assign(initializer_list<char_T> c);
```

```cpp
basic_string& insert(size_type pos, const basic_string& str);
basic_string& insert(size_type pos, const basic_string& str,
size_type pos2, size_type n = npos);
basic_string& insert(size_type pos, basic_string_view<char, traits> sv);
```

```cpp
template<class T>
basic_string& insert(size_type pos1, const T& t, size_type pos2, size_type n = npos);
basic_string& insert(size_type pos, const char* s, size_type n);
basic_string& insert(size_type pos, size_type n, char c);
iterator(const_iterator p, char c);
iterator(const_iterator p, size_type n, char c);
template<class InputIterator>
iterator(const_iterator p, InputIterator last);
iterator(const_iterator p, initializer_list<charT> list);

basic_string& erase(size_type pos = 0, size_type n = npos);
iterator erase(const_iterator p);
iterator erase(const_iterator first, const_iterator last);

void pop_back();

basic_string& replace(size_type pos1, size_type n1, const basic_string& str);
basic_string& replace(size_type pos1, size_type n1, const basic_string& str,
size_type pos2, size_type n2 = npos);
basic_string& replace(size_type pos1, size_type n1, const basic_view<char, traits> sv);
template<class T>
basic_string& replace(size_type pos1, size_type n1, const T& t,
size_type pos2, size_type n2 = npos);
basic_string& replace(size_type pos1, size_type n1, const char* s);
basic_string& replace(const_iterator i1, const_iterator i2, const char* s);
basic_string& replace(size_type pos1, size_type n1, size_type n2, char c);

basic_string& replace(const_iterator i1, const_iterator i2, const basic_string& str);
basic_string& replace(const_iterator i1, const_iterator i2, const basic_view<char, traits> sv);
basic_string& replace(const_iterator i1, const_iterator i2, const char* s, size_type n);
basic_string& replace(const_iterator i1, const_iterator i2, size_type n2, char c);
template<class InputIterator>
basic_string& replace(const_iterator i1, const_iterator i2, InputIterator j1, InputIterator j2);
basic_string& replace(const_iterator i1, const_iterator i2, const initializer_list<charT> list);

size_type copy(const charT* s, size_type n, size_type npos = 0);
void swap(basic_string& str)
noexcept(allocator_traits<Allocator>::propagate_on_swap == value ||
allocator_traits<Allocator>::is_always_equal() == value);
```

```cpp
// 24.3.2. 字符串操作
const charT* c_str() const noexcept;
const charT* data() const noexcept;
charT* data() const noexcept;
operator basic_string_view<charT, traits>() const noexcept;
allocator_type get_allocator() const noexcept;
```

```cpp
size_type find(const basic_view<char, traits> sv, size_type pos = 0) const noexcept;
size_type find(const basic_string& str, size_type pos = 0) const noexcept;
size_type find(const char* s, size_type pos, size_type n) const;
size_type find(const char* c, size_type pos = 0) const;
size_type rfind(const basic_view<char, traits> sv, size_type pos = npos) const;
size_type rfind(const basic_string& str, size_type pos = 0) const noexcept;
size_type rfind(const char* s, size_type pos, size_type n) const;
size_type rfind(const char* s, size_type pos = npos) const;
size_type rfind(const char* c, size_type pos = npos) const;
size_type find_last_of(const basic_view<char, traits> sv);
size_type find_last_of(const char* s, size_type pos = 0) const;
size_type find_last_of(const basic_string& str, size_type pos = npos) const noexcept;
size_type find_last_of(const char* s, size_type pos, size_type n) const;
size_type find_last_of(const char* s, size_type pos = npos) const;
size_type find_last_of(const char* c, size_type pos = npos) const;
size_type find_last_of(const basic_view<char, traits> sv, size_type pos = npos) const noexcept;
size_type find_last_of(const basic_string& str, size_type pos = npos) const noexcept;
size_type find_last_of(const char* s, size_type pos, size_type n) const;
size_type find_last_of(const char* s, size_type pos = npos) const;
size_type find_last_of(const char* c, size_type pos = npos) const;
size_type find_last_not(const basic_view<char, traits> sv, size_type pos = 0) const noexcept;
size_type find_last_not(const basic_string& str, size_type pos = 0) const noexcept;
size_type find_last_not(const char* s, size_type pos, size_type n) const;
size_type find_last_not(const char* c, size_type pos = 0) const;
size_type find_last_not(const basic_view<char, traits> sv, size_type pos = npos) const noexcept;
size_type find_last_not(const basic_string& str, size_type pos = npos) const noexcept;
size_type find_last_not(const char* s, size_type pos, size_type n) const;
size_type find_last_not(const char* s, size_type pos = npos) const;
size_type find_last_not(const char* c, size_type pos = npos) const;
size_type find_last_of(const char
```

# 24.3.2.1 basic_string 通用要求 [string require]

- 1 如果任何操作调用 `size()` 超过 `max_size()`，该操作应抛出 `length_error` 异常。
- 2 如果任何 basic_string 函数或操作抛出异常，该操作将不产生影响。
- 3 在 `basic_string<charT, Allocator>` 的特化版本中，`allocator_traits<Allocator>::value_type` 类型必须与 `charT` 相同。`basic_string<charT, traits>` 对象应使用类型为 Allocator 的对象分配和释放 `charT` 对象的存储空间。所使用的 Allocator 应根据 26.2.1 获取。每个 `basic_string<charT, Allocator>` 都应满足要求 (24.2)，且 `traits::char_type` 必须与 `charT` 相同。

`basic_string` 元素的引用、指针和迭代器可能会因以下 `basic_string` 使用而失效：

- (4.1) 作为接收非 const `basic_string` 参数的任何标准库函数的参数。
- (4.2) 调用非 const 成员函数，除 `[]`、`data`、`front`、`back`、`begin`、`rbegin` 和 `rend` 之外。

# 24.3.2.2 basic_string 构造函数和赋值运算符 [string const]

```cpp
explicit basic_string(const Allocator& a) noexcept;
```

- 1 影响：构造一个 basic_string 对象。该函数的后条件如表 55 所示。

表 55 — basic_string(const Allocator&) 影响

| 元素 | 值 |
| --- | --- |
| data() | 可拷贝且可以在其加 0 的非空指针 |
| size() | 0 |
| capacity() | 未定义的值 |

```cpp
basic_string(const basic_string& str);
basic_string(const basic_string&& str) noexcept;
```

- 2 影响：如表 56 所示构造一个 basic_string 类对象。在第二种形式中，str 处于有效状态且其值未定义。

```cpp
basic_string(const basic_string& str, size_type pos, const Allocator& a = Allocator());
```

- 3 抛出：如果 `pos > str.size()`，则抛出 `out_of_range`。
- 4 影响：构造一个 basic_string 类对象，并确定初始字符串值的有效长度 `len`（`str.size() - pos`），如表 57 所示。

