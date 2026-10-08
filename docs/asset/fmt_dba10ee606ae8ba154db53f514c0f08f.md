
## 28.12.1.2 `regex_iterator` 比较

`bool operator==(const regex_iterator& right) const;`

返回值：如果 `*this` 和 `right` 都是序列结束迭代器，或者满足以下所有条件，则返回 true：

- `begin == right.begin`,
- `end == right.end`,
- `prepex == right.prepex`,
- `flags == right.flags`,且
- `match[0] == right.match[0]`；

否则返回 false。

`bool operator!=(const regex_iterator& right) const;`

返回值：`!(*this == right)`。

## 28.12.1.3 `regex_iterator` 重定向

`const value_type* operator*() const;`

返回值：`&match`。

`const value_type* operator->() const;`

返回值：`&match`。

## 28.12.1.4 `regex_iterator` 增增

`regex_iterator& operator++();`

影响：创建一个类型为 `Bidirectional` 的局部 `start`，并用 `match[0].second` 的值初始化它。

如果迭代器持有 `start` 且 `start == end`，则运算符 `*this` 返回序列结束迭代器并返回 `*this`。

否则，如果迭代器持有零长度匹配，则运算符调用 `regex_search(start, end, match, *prepex, flags | regex_constants::match_not_null | regex_constants::match_continuous)`。如果迭代器返回 true，则 `*this`。否则，运算符增加 `start` 并继续，直到最近的匹配不是零长度匹配为止。

如果最近的匹配不是零长度匹配，运算符将 `flags` 设置为 `regex_constants::match_prev_avail` 并调用 `regex_search(start, end, match, *prepex, flags)`。如果迭代器返回 false，则将 `*this` 设置为序列结束迭代器。迭代器返回 `*this`。

在所有 `regex_search` 返回 true 的情况下，`match.prefix().first` 应该等于 `match[0]` 的上一个值，并且对于半开区间 `[0, match.size())` 中的每个 `match[i].matched` 为 true 的索引，`match[i].position()` 应该返回 `distance(begin, match[i])`。

> 注意：此 `match[i].position()` 提供的是相对于目标序列的偏移量，这通常与调用 `regex_search` 时传入的序列的偏移量不同。

实现如何进行这些调整是不确定的。

> 注意：这意味着编译器可能会实现一个特定于实现的搜索函数，此时用户定义的 `regex_search` 特化将不会被调用。

`regex_iterator++(int);`

影响：

```cpp
regex_iterator tmp = *this;
++*(this);
return tmp;
```

## 28.12.2 `regex_token_iterator` 类 `[re.tokiter]`

- 1 `regex_token_iterator` 类是一个迭代器适配器；也就是说，它代表了现有迭代器序列的新视图，枚举该序列中正则表达式的所有出现位置，并为找到的每个匹配项呈现一个或多个子表达式。迭代器枚举的每个位置都是一个 `sub_match` 类实例，代表正则表达式中的某个特定子表达式。
- 2 当使用 `regex_token_iterator` 枚举索引为 `-1` 的子表达式时，迭代器执行拆分操作：也就是说，它为容器中每个不匹配正则表达式的区域枚举一个子表达式。
- 3 构造完成后，迭代器存储并返回类型为 `regex_iterator<BidirectionalIterator>` 的值 `position`，并将内部计数器 `N` 设置为零。它还维护了一份已枚举的子表达式列表。每次 `operator++` 都是 `N` 增加时；如果 `N` 等于 `max()`，则迭代器重置成员 `position` 并计数器 `N` 设置为零。
- 4 如果到达序列结束（`position` 等于序列结束迭代器），迭代器将等于序列结束迭代器值，除非正在枚举的子表达式索引为 `-1`，在这种情况下，迭代器将枚举最后一个。
- 5 默认构造函数创建一个序列结束迭代器。`operator*` 对于序列结束迭代器未定义。
- 6 两个序列结束迭代器总是相等。非序列结束迭代器与序列结束迭代器不相等。两个非序列结束的 `regex_token_iterator` 在从相同项构造时是相等的。

```cpp
namespace std {
template <class BidirectionalIterator, typename traits>
using char = traits::value_type;
class regex_token_iterator : regex_traits<char> >
public:
    typedef basic_regex<char, traits> regex_type;
    typedef sub_match<BidirectionalIterator> value_type;
    typedef std::ptrdiff_t difference;
    typedef const value_type* pointer;
    typedef const value_type* reference_type;
    typedef const value_type& reference;
    typedef iterator_forward_tag iterator_category;
    regex_token_iterator();
    regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b, const regex_type& re);
```

## 28.12.2.1 `regex_token_iterator` 构造函数 `[re.tokiter.cnstr]`

```cpp
regex_token_iterator();
```

- 1 影响：构造序列结束迭代器。

```cpp
regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b, const regex_type& re, int submatch = 0, const regex_constants::match_flag_type m = regex_constants::default);
```

```cpp
regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b, const regex_type& re, const std::vector<int>& subs, const regex_constants::match_flag_type m = regex_constants::default);
```

```cpp
regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b, const regex_type& re, std_initializer_list<int> submatches, const regex_constants::match_flag_type m = regex_constants::default);
```

```cpp
template <std::size_t>
regex_token_iterator(BidirectionalIterator a, BidirectionalIterator b, const regex_type& re, int (submatches[N]), const regex_constants::match_flag_type m = regex_constants::default);
```

- 2 要求：`submatches` 的每个初始化值都应为 `-1`。
- 3 影响：第一个构造函数将成员 `subs` 初始化为持有单个值 `submatch`。第二个构造函数将成员 `subs` 初始化为参数 `submatches` 的拷贝。第三和第四构造函数将成员 `subs` 初始化为由迭代器范围 `[submatches.begin(),submatches.end())` 和 `{submatches,submatches + N}` 指向的整数序列的拷贝。
- 4 每个构造函数随后将 `N` 设置为 0，并将 `position` 设置为 `position_iterator(a, b, re, m)`。如果 `position` 不是序列结束迭代器，构造函数将设置当前匹配的值。如果存储在 `subs` 中的任何值等于 `-1`，则构造函数将此设置为后缀。

迭代器指向范围 `[a,b)`，否则构造函数将 `*this` 设置为一个序列结束迭代器。

## 28.12.2.2 `regex_token_iterator` 比较 `[re.tokiter.comp]`

`bool operator==(const regex_token_iterator& right) const;`

- 1 返回：如果 `*this` 和 `right` 都是序列结束迭代器，或者 `*this` 和 `right` 都是后缀迭代器且 `suffix == right.suffix`；则返回 true；否则，如果 `*this` 或 `right` 其中有一个是序列结束迭代器或后缀迭代器，则返回 false。如果 `position == right.position`、`N == right.N` 且 `subs == right.subs`，则返回 true。否则返回 false。

`bool operator!=(const regex_token_iterator& right) const;`

- 2 返回：`!(*this == right)`。

## 28.12.2.3 `regex_token_iterator` 取值 `[re.tokiter.deref]`

`const value_type operator*() const;`

- 1 返回：`result`。

`const value_type* operator->() const;`

- 2 返回：`result`。

## 28.12.2.4 `regex_token_iterator` 递增 `[re.tokiter.incr]`

`regex_token_iterator operator++() const;`

- 1 影响：构造类型为 `position` 的局部变量 `prev`，初始化为 `position` 的值。
- 2 如果 `*this` 是一个后缀迭代器且 `*N + 1 < subs.size()`，则增加 `N` 并返回 `subs` 指向当前字符的地址。
- 3 否则，将 `N` 设置为 0 并增加 `position`。如果 `position` 不是序列结束迭代器，则该运算符返回指向当前字符地址的设置。
- 4 否则，如果 `subs` 中存储的任何值有任何一个等于 `-1` 且 `prev->suffix().length()` 不为 0，则该运算符将 `*this` 设置为指向范围 `[prev->suffix().first, prev->suffix().second)` 的迭代器。
- 5 否则，将 `*this` 设置为一个序列结束迭代器。
- 6 返回：`*this`

`regex_token_iterator operator++(int);`

- 7 影响：构造 `*this` 的拷贝，然后调用 `++(*this)`。
- 8 返回：`tmp`。

## 28.13 修改后的 ECMAScript 正正则表达式语法 `[re.grammar]`

- 1 使用带有 ECMAScript 标志构造的 `basic_regex` 对象所识别的正则表达式由 ECMA262 指定，如下所示：
- 2 类型为 `basic_regex` 特化类的对象在内部存储了其 `traits` 模板参数 `traits_inst` 的一个默认构造的实例。该 `traits_inst` 对象被用于支持正则表达式的本地化；`basic_regex` 成员函数不应调用任何依赖于本地的 C 或 C++ API（即格式化字符串的输入函数）。相反，它们调用相应的 `traits` 成员函数以实现所需的效果。

ECMAScript 语法中的以下产生式修改如下：

```
ClassAtom ::
- ClassAtomNoDash
ClassAtomExClass
ClassAtomCollatingElement
ClassAtomEquivalence
```

随后添加了以下新产生式：

```
ClassAtomExClass ::
[ ClassName ]
ClassAtomCollatingElement ::
[ ClassName ]
ClassAtomEquivalence ::
[ ClassName =]
```

```
ClassName ::
ClassNameCharacter
ClassNameCharacter ClassName
```

```
ClassNameCharacter ::
SourceCharacter but not of "" "m" "-",
```

产生式 `ClassAtomExClass`、`ClassAtomCollatingElement` 和 `ClassAtomEquivalence` 提供了等同于 POSIX 正正则表达式中相同的功能。

正则语法可以通过根据表 38 中的规则，在构造 `basic_regex` 特化类类型对象时指定的任何 `regex_constants::syntax_option_type` 标志进行修改。

在 `ClassAtomExClass` 中使用的 `ClassName` 产生式，如果 `traits_inst.lookup_classname` 对 `name` 返回零，则为无效。被识别为有效 `ClassNames` 的名称由 `traits` 类对 `name` 的类型决定，但至少应识别以下名称：`alpha, alem, blank, cntrl, digit, lower, print, punct, space, upper, xdigit, d, s, w`。此外，以下表达式应该是等价的：

```
\d and [[:digit:]]
\W and [[:digit:]]
```

```
\s and [[:space:]]
\S and [[:space:]]
```

```
\w and [[_alnum:]]
\W and [[_alnum:]]
```
