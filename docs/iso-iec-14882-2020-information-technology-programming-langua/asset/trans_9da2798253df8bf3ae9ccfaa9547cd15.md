

## ISO/IEC 14882:2020(E)

```
wstring to_wstring(unsigned long val);
wstring to_wstring(long long val);
wstring to_wstring(unsigned long long val);
wstring to_wstring(float val);
wstring to_wstring(double val);
wstring to_wstring(long double val);
```

返回：每个函数返回一个 `wstring` 对象，该对象保存其参数的值的字符表示；该表示将分别通过使用格式说明符 L"%d"、L"%u"、L"%ld"、L"%lu"、L"%lld"、L"%llu"、L"%f"、L"%f" 或 L"%Lf" 调用 `swprintf(buf, buffsz, fmt, val)` 生成，其中 `buf` 指定一个大小足够为 `buffsz` 的内部字符缓冲区。

## 21.3.6 哈希支持 [basic.string.hash]

```
template<> struct hash<string>;
template<> struct hash<u8string>;
template<> struct hash<u16string>;
template<> struct hash<u32string>;
template<> struct hash<wstring>;
template<> struct hash<pmr::string>;
template<> struct hash<pmr::u8string>;
template<> struct hash<pmr::u16string>;
template<> struct hash<pmr::u32string>;
template<> struct hash<pmr::wstring>;
```

如果 S 是这些字符串类型之一，SV 是对应的字符串视图类型，而 s 是类型 S 的对象，则 `hash<S>()(s) == hash<SV>()(SV(s))`。

## 21.3.7 basic_string 字面量后缀 [basic.string.literals]

```
constexpr string operator""s(const char* str, size_t len);
```

返回：string{str, len}。

```
constexpr u8string operator""s(const char8_t* str, size_t len);
```

返回：u8string{str, len}。

```
constexpr u16string operator""s(const char16_t* str, size_t len);
```

返回：u16string{str, len}。

```
constexpr u32string operator""s(const char32_t* str, size_t len);
```

返回：u32string{str, len}。

```
constexpr wstring operator""s(const wchar_t* str, size_t len);
```

返回：wstring{str, len}。

[注 1：相同的后缀 s 也用于表示秒的 chrono::duration 字面量，但两者并无冲突，因为 duration 后缀应用于数字，而字符串字面量后缀应用于字符数组字面量。—— 尾注]

## 21.4 字符串视图类 [string.view]

### 21.4.1 概述 [string.view.general]

类模板 `basic_string_view` 描述了一个可以引用常量连续的 char-like（21.1）对象序列的对象，序列的第一个元素位于位置零。在 21.4 的其余部分中，`basic_string_view` 对象所持有的 char-like 对象的类型用 `charT` 表示。

[注 1：标准库提供了从 `const charT*` 和 `std::basic_string<charT, ...>` 到 `std::basic_string_view<charT, ...>` 的隐式转换，因此只要期望字符序列，用户代码就可以仅接受 `std::basic_string_view<charT>` 作为非模板参数。用户自定义类型可以定义它们自己的到 `std::basic_string_view` 的隐式转换，以便与这些函数互操作。—— 尾注]

```
public:
    // types
    using traits_type          = traits;
    using value_type           = charT;
    using pointer              = value_type*;
    using const_pointer        = const value_type*;
    using reference            = value_type&;
    using const_reference      = const value_type&;
    using const_iterator       = implementation-defined; // see 21.4.3.3
    using iterator             = const_iterator;²²⁹
    using const_reverse_iterator = reverse_iterator<const_iterator>;
    using reverse_iterator     = const_reverse_iterator;
    using size_type            = size_t;
    using difference_type      = ptrdiff_t;
    static constexpr size_type npos = size_type(-1);

    // 21.4.3.2, construction and assignment
    constexpr basic_string_view() noexcept;
    constexpr basic_string_view(const basic_string_view&) noexcept = default;
    constexpr basic_string_view& operator=(const basic_string_view&) noexcept = default;
    constexpr basic_string_view(const charT* str);
    constexpr basic_string_view(const charT* str, size_type len);
    template<class It, class End>
        constexpr basic_string_view(It begin, End end);

    // 21.4.3.3, iterator support
    constexpr const_iterator begin() const noexcept;
    constexpr const_iterator end() const noexcept;
    constexpr const_iterator cbegin() const noexcept;
    constexpr const_iterator cend() const noexcept;
    constexpr const_reverse_iterator rbegin() const noexcept;
    constexpr const_reverse_iterator rend() const noexcept;
    constexpr const_reverse_iterator crbegin() const noexcept;
    constexpr const_reverse_iterator crend() const noexcept;

    // 21.4.3.4, capacity
    constexpr size_type size() const noexcept;
    constexpr size_type length() const noexcept;
    constexpr size_type max_size() const noexcept;
    [[nodiscard]] constexpr bool empty() const noexcept;

    // 21.4.3.5, element access
    constexpr const_reference operator[](size_type pos) const;
    constexpr const_reference at(size_type pos) const;
    constexpr const_reference front() const;
    constexpr const_reference back() const;
    constexpr const_pointer data() const noexcept;

    // 21.4.3.6, modifiers
    constexpr void remove_prefix(size_type n);
    constexpr void remove_suffix(size_type n);
    constexpr void swap(basic_string_view& s) noexcept;

    // 21.4.3.7, string operations
    constexpr size_type copy(charT* s, size_type n, size_type pos = 0) const;

    constexpr basic_string_view substr(size_type pos = 0, size_type n = npos) const;

    constexpr int compare(basic_string_view s) const noexcept;
    constexpr int compare(size_type pos1, size_type n1, basic_string_view s) const;
    constexpr int compare(size_type pos1, size_type n1, basic_string_view s,
                          size_type pos2, size_type n2) const;
```

229) 由于 basic_string_view 引用的是常量序列，iterator 和 const_iterator 是同一类型。

## ISO/IEC 14882:2020(E)

```
constexpr int compare(const charT* s) const;
constexpr int compare(size_type pos1, size_type n1, const charT* s) const;
constexpr int compare(size_type pos1, size_type n1, const charT* s, size_type n2) const;

constexpr bool starts_with(basic_string_view x) const noexcept;
constexpr bool starts_with(charT x) const noexcept;
constexpr bool starts_with(const charT* x) const;
constexpr bool ends_with(basic_string_view x) const noexcept;
constexpr bool ends_with(charT x) const noexcept;
constexpr bool ends_with(const charT* x) const;
```

```
// 21.4.3.8, searching
constexpr size_type find(basic_string_view s, size_type pos = 0) const noexcept;
constexpr size_type find(charT c, size_type pos = 0) const noexcept;
constexpr size_type find(const charT* s, size_type pos, size_type n) const;
constexpr size_type find(const charT* s, size_type pos = 0) const;
constexpr size_type rfind(basic_string_view s, size_type pos = npos) const noexcept;
constexpr size_type rfind(charT c, size_type pos = npos) const noexcept;
constexpr size_type rfind(const charT* s, size_type pos, size_type n) const;
constexpr size_type rfind(const charT* s, size_type pos = npos) const;
```

```
constexpr size_type find_first_of(basic_string_view s, size_type pos = 0) const noexcept;
constexpr size_type find_first_of(charT c, size_type pos = 0) const noexcept;
constexpr size_type find_first_of(const charT* s, size_type pos, size_type n) const;
constexpr size_type find_first_of(const charT* s, size_type pos = 0) const;
constexpr size_type find_last_of(basic_string_view s, size_type pos = npos) const noexcept;
constexpr size_type find_last_of(charT c, size_type pos = npos) const noexcept;
constexpr size_type find_last_of(const charT* s, size_type pos, size_type n) const;
constexpr size_type find_last_of(const charT* s, size_type pos = npos) const;
constexpr size_type find_first_not_of(basic_string_view s, size_type pos = 0) const noexcept;
constexpr size_type find_first_not_of(charT c, size_type pos = 0) const noexcept;
constexpr size_type find_first_not_of(const charT* s, size_type pos, size_type n) const;
constexpr size_type find_first_not_of(const charT* s, size_type pos = 0) const;
constexpr size_type find_last_not_of(basic_string_view s, size_type pos = npos) const noexcept;
constexpr size_type find_last_not_of(charT c, size_type pos = npos) const noexcept;
constexpr size_type find_last_not_of(const charT* s, size_type pos, size_type n) const;
constexpr size_type find_last_not_of(const charT* s, size_type pos = npos) const;
```

```
private:
    const_pointer data_;      // exposition only
    size_type size_;          // exposition only
};
```

```
// 21.4.4, deduction guide
template<class It, class End>
    basic_string_view(It, End) -> basic_string_view<iter_value_t<It>>;
}
```

1 在每个 `basic_string_view<charT, traits>` 特化中，类型 `traits` 应满足字符特征要求（21.2）。
[注 1：如果 `traits::char_type` 与 `charT` 不是同一类型，则程序为非良构。—— 尾注]

2 对于 `basic_string_view` str，任何使 `[str.data(), str.data() + str.size()]` 范围内的指针失效的操作，也会使从 str 的成员函数返回的指针、迭代器和引用失效。

3 除非另有规定，`basic_string_view` 成员函数的复杂度为 O(1)。

### 21.4.3.2 构造与赋值 [string.view.cons]

```
constexpr basic_string_view() noexcept;
```

1 后置条件：size_ == 0 且 data_ == nullptr。

