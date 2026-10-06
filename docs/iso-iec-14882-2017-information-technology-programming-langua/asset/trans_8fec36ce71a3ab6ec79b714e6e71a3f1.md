

# ISO/IEC 14882:2017(E)

13 返回：*this*。

```
basic_string
insert(size_type pos, const charT s);
```

14 要求：s 指向一个包含至少 traits::length(s) + 1 个 charT 元素的数组；

15 效果：等于返回 insert(pos, s, traits::length(s))。

```
basic_string
insert(size_type pos, size_type n, charT c);
```

16 效果：等于 insert(pos, basic_string(n), c)。

17 返回：*this*。

```
iterator insert(const_iterator p, charT c);
```

18 要求：p 是一个越过 *this* 的有效迭代器。

19 效果：插入 p 所指字符的拷贝。

20 返回：一个指向所插入字符拷贝的迭代器。

```
iterator insert(const_iterator p, size_type n, charT c);
```

21 要求：p 是一个越过 *this* 的有效迭代器。

22 效果：在 p 所指字符之前插入 n 个 c 的拷贝。

23 返回：一个指向第一个插入字符拷贝的迭代器，或者如果第一个 n == 0 则返回 p*。

```
template<class InputIterator>
```

```
iterator insert(const_iterator p, InputIterator first, InputIterator last);
```

24 要求：p 是一个越过 *this* 的有效迭代器；[first, last) 是一个有效范围。

25 效果：等于 insert(p - begin(), basic_string(first, last, get_allocator()))。

26 返回：一个指向第一个插入字符拷贝的迭代器，或者如果 first == last 则返回 p*。

```
iterator insert(const_iterator p, initializer_list<charT> l);
```

27 效果：如同执行 insert(p, l.begin(), l.end())。

28 返回：一个指向第一个插入字符拷贝的迭代器，或者如果 l 为空则返回 p*。

## § 24.3.2.6. basic_string::erase [erase]

```
basic_string& erase(size_type pos = 0, size_type n = npos);
```

- 1 抛出：如果 pos > size() 则抛出 out_of_range；
- 2 效果：要删除字符串的有效长度 len 为 n 和 size() - pos 中的较者。
- 3 该函数将 *this* 控制的字符串替换为长度为 size() - len 的字符串，其前 pos 个元素是 *this* 控制的原始字符串初始元素的拷贝，剩余元素是 *this* 控制的原始字符串从 pos + len 开始的元素的拷贝。
- 4 返回：*this*。

```
iterator erase(const_iterator p);
```

- 5 抛出：无。
- 6 效果：移除 p 所指的字符。

7 返回：一个指向被删除元素之前的 p 紧随其元素的迭代器。如果不存在这样的元素，则返回 end()。

```
iterator erase(const_iterator first, const_iterator last);
```

- 8 要求：first 和 last 是越过 *this* 的有效迭代器，定义了一个范围 [first, last)。

- 9 抛出：无。

- 10 效果：移除范围 [first, last) 中的字符。

- 11 返回：一个指向其他被删除元素之前的元素的迭代器。如果不存在这样的元素，则返回 end()。

```
void pop_back();
```

- 12 要求：empty()。

- 13 抛出：无。

- 14 效果：等于 erase(size() - 1, 1)。

## 24.3.2.6 basic_string::replace

```
basic_string replace(size_type pos1, size_type n1, const basic_string& str);
```

1 效果：等于：replace(pos1, n1, str.data(), str.size())。

```
basic_string replace(size_type pos1, size_type n1, const basic_string& str,
size_type pos2, size_type n2 = npos);
```

2 抛出：如果 pos1 > size() 或 pos2 > str.size() 则抛出 out_of_range。

3 效果：确定要插入字符串的有效长度 len 为 n2 和 str.size() - pos2 中的较者，并调用 replace(pos1, n1, str.data() + pos2)。

4 抛出：无。

```
basic_string replace(size_type pos1, size_type n1, const basic_view<charT, traits> sv);
```

5 效果：等于 replace(pos1, n1, sv.data(), sv.size())。

```
template <class T>
basic_string replace(size_type pos1, size_type n1, const T& t,
size_type pos2, size_type n2 = npos);
```

6 抛出：如果 pos1 > size() 或 pos2 > sv.size() 则抛出 out_of_range。

7 效果：通过 basic_view<charT, traits> traits = t 创建一个变量 sv。确定要插入字符串的有效长度为 n2 和 sv.size() - pos2 中的较者，并调用 replace(pos1, n1, sv.data() + pos2)。

8 备注：除非 is_convertible_const<T&, basic_view<charT, traits>> 为 true 且 is_convertible_const<charT*, T> 为 false，否则此函数不参与重载决议。

9 抛出：无。

```
basic_string replace(size_type pos1, size_type n1, const char* s);
```

10 要求：s 指向至少 n2 个字符的区域。

11 抛出：如果 pos1 > size() 则抛出 out_of_range；如果结果字符串长度超过 size() 则抛出 length_error（见下文）。

12 效果：将 *this* 替换为长度 len 的字符串，其中前 len元素是 s 的拷贝，剩余元素是 *this* 元素的拷贝。

13 返回：*this*。

```
basic_string replace(size_type pos1, size_type n1, const char* s);
```

14 要求：s 指向包含至少 length(s) + 1 个元素的数组。

15 效果：等于 replace(pos1, n1, s, length(s))。

```
basic_string replace(size_type pos1, size_type n1, const basic_string& str);
```

16 要求：str 指向至少 n1 个字符的区域。

17 效果：将 *this* 替换为长度 size() - len 的字符串。

18 返回：*this*。

```
basic_string replace(size_type pos1, size_type n1, const basic_string& str);
```

19 要求：str 指向至少 n1 个元素的区域。

20 效果：等于 replace(pos1, n1, str.data(), str.size())。

21 返回：*this*。

```
basic_string replace(size_type pos1, size_type n1, const basic_view<charT, traits> sv);
```

22 要求：sv 指向至少 sv.size() 个字符的区域。

23 效果：等于 replace(pos1, n1, sv.data(), sv.size())。

24 返回：*this*。

```
basic_string replace(size_type pos1, size_type n1, const char* s);
```

25 要求：s 指向至少 length(s) + 1 个元素的数组。

26 效果：等于 replace(pos1, n1, s, length(s))。

27 返回：*this*。

```
basic_string replace(size_type pos1, size_type n1, const basic_string& str, size_type pos2, size_type n2);
```

28 抛出：如果 pos1 > size() 或 pos2 > str.size() 则抛出 out_of_range。

29 效果：确定要插入字符串的有效长度 len 为 n2 和 str.size() - pos2 中的较者，并调用 replace(pos1, n1, str.data() + pos2)。

30 抛出：无。

```cpp
basic_string replace(size_type pos1, size_type n1, const T& t, size_type pos2, size_type n2 = npos);
```

31 抛出：如果 pos1 > size() 或 pos2 > sv.size() 则抛出 out_of_range。

32 效果：通过 basic_view<charT, traits> traits = t 创建一个变量 sv。确定要插入字符串的有效长度为 n2 和 sv.size() - pos2 中的较者，并调用 replace(pos1, n1, sv.data() + pos2)。

33 抛出：无。

```cpp
basic_string replace(size_type pos1, size_type n1, const char* s);
```

34 要求：s 指向至少 n2 个字符的区域。

35 抛出：如果 pos1 > size() 则抛出 out_of_range；如果结果字符串长度超过 size() 则抛出 length_error（见下文）。

36 效果：将 *this* 替换为长度 size() - len 的字符串。

37 返回：*this*。

```cpp
basic_string replace(size_type pos1, size_type n1, const char* s);
```

38 要求：s 指向至少 length(s) + 1 个元素的数组。

39 效果：等于 replace(pos1, n1, s, length(s))。

40 返回：*this*。

```cpp
basic_string replace(size_type pos1, size_type n1, const basic_string& str, size_type pos2, size_type n2);
```

41 抛出：如果 pos1 > size() 或 pos2 > str.size() 则抛出 out_of_range。

42 效果：确定要插入字符串的有效长度 len 为 n2 和 str.size() - pos2 中的较者，并调用 replace(pos1, n1, str.data() + pos2)。

43 抛出：无。

```cpp
basic_string replace(size_type pos1, size_type n1, const basic_view<charT, traits> sv);
```

44 效果：等于 replace(pos1, n1, sv.data(), sv.size())。

45 返回：*this*。

```cpp
template <class T>
basic_string replace(size_type pos1, size_type n1, const T& t, size_type pos2, size_type n2 = npos);
```

46 抛出：如果 pos1 > size() 或 pos2 > sv.size() 则抛出 out_of_range。

47 效果：通过 basic_view<charT, traits> traits = t 创建一个变量 sv。确定要插入字符串的有效长度为 n2 和 sv.size() - pos2 中的较者，并调用 replace(pos1, n1, sv.data() + pos2)。

48 抛出：无。

```cpp
basic_string replace(size_type pos1, size_type n1, const char* s);
```

49 要求：s 指向至少 n2 个字符的区域。

50 抛出：如果 pos1 > size() 则抛出 out_of_range；如果结果字符串长度超过 size() 则抛出 length_error（见下文）。

51 效果：将 *this* 替换为长度 size() - len 的字符串。

52 返回：*this*。

```cpp
basic_string replace(size_type pos1, size_type n1, const char* s);
```

53 要求：s 指向至少 length(s) + 1 个元素的数组。

54 效果：等于 replace(pos1, n1, s, length(s))。

55 返回：*this*。

## 24.3.2.7 basic_string string operations [string.ops]

### 24.3.2.7.1 basic_string accessors [string.accessors]

```
const charT* c_str() const noexcept;
const charT* data() const noexcept;
```

- 3 返回：一个指针 p，对于 [0, size()) 中的每个 i，p + i == operator[](i)。
- 2 复杂度：常数时间。
- 3 要求：程序不修改字符数组中的任何值。

charT* data() const noexcept;

- 4 返回：一个指针 p，对于 [0, size()) 中的每个 i，p + i == operator[](i)。
- 5 复杂度：常数时间。
- 6 要求：程序不修改 p + size() 处的值。

operator basic_string_view<charT, traits> const noexcept;

- 7 效果：等于返回 basic_string_view<charT, traits>(data(), size())。

allocator_type get_allocator() const noexcept;

- 8 返回：用于构造字符串的分配器的拷贝，如果该分配器被替换，则返回最近一次替换的拷贝。
