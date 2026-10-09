
```cpp
template<class T>
constexpr basic_string& insert(size_type pos, const T& t);
template<class T>
constexpr basic_string& insert(size_type pos, const T& t,
      size_type pos2, size_type n = npos);
constexpr basic_string& insert(size_type pos, const char* s, size_type n = npos);
constexpr basic_string& insert(size_type pos, const char* s);
constexpr basic_string& insert(size_type pos, size_type n, charT c);
iterator insert(const_iterator p, charT c);
iterator insert(const_iterator p, size_type n, charT c);
```

```cpp
template<class InputIterator>
constexpr iterator insert(const_iterator p, InputIterator last);
iterator insert(const_iterator p, initializer_list<charT>);
```

```cpp
constexpr basic_string& erase(size_type pos = 0, size_type n = npos);
constexpr erase(const_iterator p);
constexpr erase(const_iterator first, const_iterator last);
```

```cpp
constexpr basic_string& replace(size_type pos, size_type n1, const basic_string& str);
constexpr basic_string& replace(size_type pos, size_type n1, const basic_string& str,
      size_type pos2, size_type n2 = npos);
```

```cpp
template<class T>
constexpr basic_string& replace(size_type pos, size_type n1, const T& t);
template<class T>
constexpr basic_string& replace(size_type pos, size_type n1, const T& t,
      size_type pos2, size_type n2 = npos);
constexpr basic_string& replace(size_type pos, size_type n1, const char* s, size_type n2);
constexpr basic_string& replace(size_type pos, size_type n1, const char* s);
constexpr basic_string& replace(size_type pos, size_type n1, charT c);
constexpr basic_string& replace(const_iterator i1, const_iterator i2, charT c);
replace(const_iterator i1, const_iterator i2);
```

```cpp
template<class T>
constexpr basic_string& replace(const_iterator i1, const_iterator i2, const T& t);
constexpr basic_string& replace(const_iterator i1, const_iterator i2, const char* s,
      size_type n);
constexpr basic_string& replace(const_iterator i1, const_iterator i2, const char* s);
constexpr basic_string& replace(const_iterator i1, const_iterator i2, size_type n, charT c);
template<class InputIterator>
constexpr basic_string& replace(const_iterator i1, const_iterator i2, InputIterator j1, InputIterator j2);
replace(const_iterator i1, const_iterator i2, initializer_list<charT>);
```

```cpp
constexpr size_type copy(const charT* s, size_type n, size_type pos = 0);
```

```cpp
constexpr void pop_back(allocator<charT>& alloc = {propagate_on_container_swap = value} : allocator<charT>::is_always_equal = value});
```

// 21.3.3 字符串操作

```cpp
template<class T>
constexpr size_type find(const T& t, size_type pos = 0) const;
;
```

```cpp
cpp size_ size find(const basic_string& s, size_type_ = 0)0)except;
```

```cpp
constexpr size_type find(const char* s, size_type pos, size_type n) const;
```

```cpp
constexpr size_type find(const char* c, size_type pos = 0) const no
;
```

```cpp
constexpr size_type rfind(const basic_string& s, size_type pos = npos) const noexcept(see below);
```

```cpp
constexpr size_type rfind(const basic_string& s, size_type pos, size_type n) const noexcept;
```

```cpp
constexpr size_type rfind(const char* s, size_type pos, size_type n) const;
```

```cpp
constexpr size_type rfind(const char* c, size_type pos = 0) const noexcept;
```

```cpp
template<class T>
constexpr size_type find_first_of(const basic_string& s, size_type pos = 0) const noexcept(see below);
```

```cpp
constexpr size_type find_first_of(const basic_string& s, size_type pos, size_type n) const noexcept;
```

```cpp
constexpr size_type find_first_of(const char* s, size_type pos, size_type n) const;
```

```cpp
constexpr size_type find_first_of(const char* c, size_type pos = 0) const noexcept;
```

```cpp
template<class T>
constexpr size_type find_last_of(const basic_string& s, size_type pos = npos) const noexcept(see below);
```

```cpp
constexpr size_type find_last_of(const basic_string& s, size_type pos, size_type n) const noexcept;
```

```cpp
constexpr size_type find_last_of(const char* s, size_type pos, size_type n) const;
```

```cpp
constexpr size_type find_last_of(const char* c, size_type pos = 0) const noexcept;
```

```cpp
template<class T>
constexpr size_type find_last_not_of(const T& t, size_type pos = npos) const noexcept(see below);
```

```cpp
constexpr size_type find_last_not_of(const basic_string& s) const noexcept;
```

```cpp
constexpr size_type find_last_not_of(const basic_string& s, size_type pos, size_type n) const noexcept;
```

```cpp
constexpr size_type find_last_not_of(const char* s, size_type pos, size_type n) const noexcept;
```

```cpp
constexpr size_type find_last_not_of(const char* c, size_type pos = 0) const noexcept;
```

```cpp
template<class T>
constexpr basic_string substr(size_type pos = 0, size_type n = npos) const;
```

```cpp
template<class T>
constexpr int compare(const T& t) const noexcept(see below);
```

```cpp
template<class T>
constexpr int compare(size_type pos, size_type n1, const T& t, const;
      size_type pos2, size_type n2 = npos) const;
```

```cpp
constexpr int compare(const basic_string& str, const char* str) const;
```

```cpp
constexpr int compare(size_type pos, size_type n1, const basic_string& str) const noexcept;
      size_type pos2, size_type n2 = npos) const;
```

```cpp
constexpr int compare(size_type pos, size_type n1, const char* s) const noexcept;
      size_type pos2, size_type n2 = npos) const;
```

```cpp
constexpr bool starts_with(const basic_view<char, traits> t) const noexcept;
```

```cpp
constexpr bool starts_with(const char* t) const noexcept;
```

```cpp
constexpr bool ends_with(const basic_view<char, traits> t) const noexcept;
```

```cpp
constexpr bool ends_with(const char x) noexcept;
constexpr bool ends_with(const char* x) noexcept;
};
template<class InputIterator>
    class Allocator = allocator<typename iterator_traits<InputIterator>::value_type>
    basic_string(InputIterator, InputIterator, Allocator& = Allocator())
    -> basic_string(typename iterator_traits<InputIterator>::value_type,
        char_traits<typename iterator_traits<InputIterator>::value_type,
        Allocator);
template<class charT>
    class traits {
        class Allocator = allocator<charT>
        explicit basic_string(basic_string<charT, traits>, const, Allocator& = Allocator())
        -> basic_string<charT, traits, Allocator>;
template<class charT>
    class traits {
        class Allocator = allocator<charT>
        basic_string(basic_view<charT>, typename see below::size_type,
            const Allocator& = Allocator())
        -> basic_string<charT, traits, Allocator>;
    }
};
```

4 `size_type` 参数通过推导指南中得到的 `size_type`。

# 21.3.2 通用要求 [string-require]

- 1 如果任何导致 `size()` 超过 `max_size()` 的操作将抛出一个 `length_error` 异常对象。
- 2 如果 `basic_string` 的任何成员抛出异常，则函数或运算符对 `basic_string` 对象不产生其他影响。
- 3 在 `basic_string<charT, traits, Allocator>` 的每个特化中，`traits<Allocator>::char_type` 必须与 `charT` 类型相同。每个 `basic_string<charT, traits, Allocator>` 对象使用 `Allocator` 对象来分配和释放包含的 `charT` 对象的存储。`Allocator` 对象按照 22.2.1 的描述使用。在 `basic_string<charT, traits, Allocator>` 的每个特化中，`traits` 必须满足字符特性要求（21.2.2）。

> 注意 1：如果 `traits::char_type` 与 `charT` 类型不同，则程序是格式错误的（ill-formed）。

指向 `basic_string` 序列中元素的引用、指针和迭代器可能由于以下对 `basic_string` 对象的使用而失效：

- (4.1) 作为任何接收非 const `basic_string` 引用的标准库函数的参数传递。
- (4.2) 调用非 const 成员函数，但 `operator[]`、`at`、`data`、`front`、`back`、`begin`、`end` 和 `rend` 除外。
- (4.3) 作为非 const 成员 `swap()` (21.3.4.3)、`operator()` (21.3.4.4) 和 `getline()` (21.3.4.4) 的参数，或者作为 `basic_string::swap()` 的参数。

# ISO/IEC 14882:2020(E)

```cpp
constexpr_basic_string(const basic_string& str, size_type pos,
const Allocator& a = Allocator());
constexpr_basic_string(const basic_string& str, size_type pos, size_type n,
const Allocator& a = Allocator());
```

4 效果：令第一个循环的 `n` 为 `pos`。等价于：
basic_string(basic_string<char,traits>::substr(str, n), a);

```cpp
template<class T>
```
