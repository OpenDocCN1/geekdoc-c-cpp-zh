

## ISO/IEC 14882:2020(E)

Table 136: syntax_option_type 效果  [tab:re.synopt]

| Element | Effect(s) if set |
|---|---|
| icase | 指定对字符容器序列进行正则表达式匹配时应忽略大小写。 |
| nosubs | 指定不应将任何子表达式视为已标记，因此当正则表达式与字符容器序列匹配时，不应在提供的 match_results 对象中存储任何子表达式匹配。 |
| optimize | 指定正则表达式引擎应更关注正则表达式匹配的速度，而较少关注正则表达式对象构造的速度。否则它对程序输出没有可检测的影响。 |
| collate | 指定形式为 "[a-b]" 的字符范围应为区域设置敏感。 |
| ECMAScript | 指定正则表达式引擎识别的语法应为 ECMA-262 中 ECMAScript 使用的语法，经 30.13 修改。另请参见：ECMA-262 15.10 |
| basic | 指定正则表达式引擎识别的语法应为 POSIX 中基本正则表达式使用的语法。另请参见：POSIX，Base Definitions and Headers，第 9.3 节 |
| extended | 指定正则表达式引擎识别的语法应为 POSIX 中扩展正则表达式使用的语法。另请参见：POSIX，Base Definitions and Headers，第 9.4 节 |
| awk | 指定正则表达式引擎识别的语法应为 POSIX 中 awk 实用程序使用的语法。 |
| grep | 指定正则表达式引擎识别的语法应为 POSIX 中 grep 实用程序使用的语法。 |
| egrep | 指定正则表达式引擎识别的语法应为 POSIX 中 grep 实用程序在给定 -E 选项时使用的语法。 |
| multiline | 指定 ^ 应匹配一行的开头，$ 应匹配一行的结尾，如果选择了 ECMAScript 引擎。 |

```
inline constexpr match_flag_type match_not_bow = unspecified;
inline constexpr match_flag_type match_not_eow = unspecified;
inline constexpr match_flag_type match_any = unspecified;
inline constexpr match_flag_type match_not_null = unspecified;
inline constexpr match_flag_type match_continuous = unspecified;
inline constexpr match_flag_type match_prev_avail = unspecified;
inline constexpr match_flag_type format_default = {};
inline constexpr match_flag_type format_sed = unspecified;
inline constexpr match_flag_type format_no_copy = unspecified;
inline constexpr match_flag_type format_first_only = unspecified;
}
```

1 类型 match_flag_type 是一个实现定义的位掩码类型（16.3.3.3.4）。该类型的常量，除 match_default 和 format_default 外，都是位掩码元素。match_default 和 format_default 常量为空位掩码。对字符序列 [first, last) 进行正则表达式匹配应根据正则表达式对象指定的语法规则进行，并根据 Table 137 中列出的任何已设置位掩码元素的效果进行修改。

Table 137: regex_constants::match_flag_type 在获取对字符容器序列 [first, last) 的匹配时的效果  [tab:re.matchflag]

| Element | Effect(s) if set |
|---|---|
| match_not_bol | 序列 [first, last) 中的第一个字符应被视为不在一行的开头，因此正则表达式中的字符 ^ 不应匹配 [first, first)。 |

that returns a value in which each ctype_base::mask value corresponding to a value in f named in Table 139 is set, then the result is determined as if by:

```
ctype_base::mask m = convert<charT>(f);
const ctype<charT>& ct = use_facet<ctype<charT>>(getloc());
if (ct.is(m, c)) {
  return true;
} else if (c == ct.widen('_')) {
  charT w[1] = { ct.widen('w') };
  char_class_type x = lookup_classname(w, w+1);
  return (f&x) == x;
} else {
  return false;
}
```

[Example 1:

```
regex_traits<char> t;
string d("d");
string u("upper");
regex_traits<char>::char_class_type f;
f = t.lookup_classname(d.begin(), d.end());
f |= t.lookup_classname(u.begin(), u.end());
ctype_base::mask m = convert<char>(f);  // m == ctype_base::digit|ctype_base::upper
```

— end example]

[Example 2:

```
regex_traits<char> t;
string w("w");
regex_traits<char>::char_class_type f;
f = t.lookup_classname(w.begin(), w.end());
t.isctype('A', f);  // returns true
t.isctype('_', f);  // returns true
t.isctype(' ', f);  // returns false
```

— end example]

```
int value(charT ch, int radix) const;
```

Preconditions: The value of radix is 8, 10, or 16.

Returns: The value represented by the digit ch in base radix if the character ch is a valid digit in base radix; otherwise returns -1.

```
locale_type imbue(locale_type loc);
```

Effects: Imbues this with a copy of the locale loc.

[Note 1: Calling imbue with a different locale than the one currently in use invalidates all cached data held by *this. — end note]

Returns: If no locale has been previously imbued then a copy of the global locale in effect at the time of construction of *this, otherwise a copy of the last argument passed to imbue.

Postconditions: getloc() == loc.

```
locale_type getloc() const;
```

Returns: If no locale has been imbued then a copy of the global locale in effect at the time of construction of *this, otherwise a copy of the last argument passed to imbue.

## 30.8 Class template basic_regex [re.regex]

### 30.8.1 General [re.regex.general]

1 对于类字符类型 charT，类模板 basic_regex 的特化表示由 charT 字符序列构造的正则表达式。在 30.8 的其余部分中，charT 表示给定的类字符类型。正则表达式的存储由类 basic_regex 的成员函数根据需要分配和释放。

## ISO/IEC 14882:2020(E)

```
template<class ForwardIterator>
    basic_regex(ForwardIterator first, ForwardIterator last,
                flag_type f = regex_constants::ECMAScript);
    basic_regex(initializer_list<charT> il, flag_type f = regex_constants::ECMAScript);
    ~basic_regex();
    // 30.8.3, assign
    basic_regex& operator=(const basic_regex& e);
    basic_regex& operator=(basic_regex&& e) noexcept;
    basic_regex& operator=(const charT* p);
    basic_regex& operator=(initializer_list<charT> il);
    template<class ST, class SA>
        basic_regex& operator=(const basic_string<charT, ST, SA>& s);
    basic_regex& assign(const basic_regex& e);
    basic_regex& assign(basic_regex&& e) noexcept;
    basic_regex& assign(const charT* p, flag_type f = regex_constants::ECMAScript);
    basic_regex& assign(const charT* p, size_t len, flag_type f = regex_constants::ECMAScript);
    template<class ST, class SA>
        basic_regex& assign(const basic_string<charT, ST, SA>& s,
                            flag_type f = regex_constants::ECMAScript);
    template<class InputIterator>
        basic_regex& assign(InputIterator first, InputIterator last,
                            flag_type f = regex_constants::ECMAScript);
    basic_regex& assign(initializer_list<charT>,
                        flag_type f = regex_constants::ECMAScript);
    // 30.8.4, const operations
    unsigned mark_count() const;
    flag_type flags() const;
    // 30.8.5, locale
    locale_type imbue(locale_type loc);
    locale_type getloc() const;
    // 30.8.6, swap
    void swap(basic_regex&);
};
template<class ForwardIterator>
    basic_regex(ForwardIterator, ForwardIterator,
                regex_constants::syntax_option_type = regex_constants::ECMAScript)
    -> basic_regex<typename iterator_traits<ForwardIterator>::value_type>;
}
```

### 30.8.2 Constructors [re.regex.construct]

basic_regex();

Postconditions: *this does not match any character sequence.

explicit basic_regex(const charT* p, flag_type f = regex_constants::ECMAScript);

Preconditions: [p, p + char_traits<charT>::length(p)) is a valid range.

Effects: The object’s internal finite state machine is constructed from the regular expression contained in the sequence of characters [p, p + char_traits<charT>::length(p)), and interpreted according to the flags f.

Postconditions: flags() returns f. mark_count() returns the number of marked sub-expressions within the expression.

Throws: regex_error if [p, p + char_traits<charT>::length(p)) is not a valid regular expression.

