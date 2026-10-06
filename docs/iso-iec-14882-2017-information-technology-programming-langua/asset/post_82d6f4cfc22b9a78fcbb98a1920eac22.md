
# ISO/IEC 14882:2017(E)

Table 133 — Character class names and corresponding ctype masks

| Narrow character name | Wide character name | Corresponding ctype_base::mask value |
|--- |--- | --- |
| "alnum" | L"alnum" | ctype_base::alnum |
| "alpha" | L"alpha" | ctype_base::alpha |
| "blank" | L"blank" | ctype_base::blank |
| "cntrl" | L"cntrl" | ctype_base::ctrl |
| "digit" | L"digit" | ctype_base::digit |
| "d" | L"d" | ctype_base::digit |
| "graph" | L"graph" | ctype_base::graph |
| "lower" | L"lower" | ctype_base::lower |
| "print" | L"print" | ctype_base::print |
| "punct" | L"punct" | ctype_base::punct |
| "space" | L"space" | ctype_base::space |
| "upper" | L"upper" | ctype_base::upper |
| "w" | L"w" | ctype_base::alnum |
| "xdigit" | L"xdigit" | ctype_base::xdigit |

> The functions defined in this class report errors by throwing exceptions of type regex_error.

```cpp
namespace std {
template <class charT, class traits = regex_traits<charT>>
class basic_regex {
public:
    // types
    using value_type = charT;
    using traits_type = traits;
    using string_type = typename traits::string_type;
    using regex_constants = syntax_option_type;
    using flag_type =
    using locale_type = typename traits::locale_type;

// 31.8.1, constants
static constexpr regex_constants::syntax_option_type
    icase = regex_constants::icase;
static constexpr regex_constants::syntax_option_type
    nosub = regex_constants::nosub;
static constexpr regex_constants::syntax_option_type
    optimize = regex_constants::optimize;
static constexpr regex_constants::syntax_option_type
    collate = regex_constants::collate;
static constexpr regex_constants::syntax_option_type
    ECMAScript = regex_constants::ECMAScript;
static constexpr regex_constants::syntax_option_type
    basic = regex_constants::basic;
static constexpr regex_constants::syntax_option_type
    extended = regex_constants::extended;
static constexpr regex_constants::syntax_option_type
    awk = regex_constants::awk;
static constexpr regex_constants::syntax_option_type
    group = regex_constants::group;
```

```cpp
static constexpr regex_constants::syntax_option_type
egrep = regex_constants::egrep;
static constexpr regex_constants::syntax_option_type
multiline = regex_constants::multiline;
```

```cpp
// 3.8.2. construct/destroy
basic_regex();
explicit basic_regex(const charT p, flag_type f = regex_constants::ECMAScript);
basic_regex(const charT p, size_t len, flag_type f = regex_constants::ECMAScript);
basic_regex(const basic_regex&) noexcept;
template<class T, SA>
explicit basic_regex(const basic_string<charT, SA>& s, p
flag_type f = regex_constants::ECMAScript);
basic_regex(ForwardIterator first, ForwardIterator last,
basic_regex(initializer_list<charT> il, flag_type f = regex_constants::ECMAScript);
```

```cpp
-basic_regex();
basic_regex&operator=(const basic_regex&);
basic_regex&operator=(const basic_regex&) noexcept;
basic_regex&operator=(const charT* ptr);
basic_regex&operator=(initializer_list<charT> il);
template<class T, SA>
basic_regex&operator=(const basic_string<charT, SA>& p);
```

```cpp
// 3.8.5. assign
basic_regex assign(const basic_regex& that) noexcept;
basic_regex assign(const basic_regex& e) noexcept;
basic_regex assign(const charT* ptr, size_t len, flag_type f);
template<class string_traits, class A>
basic_regex assign(const basic_string<charT, string_traits>& s, A& s,
flag_type f = regex_constants::ECMAScript);
template<class InputIterator>
basic_regex& assign(InputIterator first, InputIterator last,
flag_type f = regex_constants::ECMAScript);
basic_regex assign(initializer_list<charT>,
flag_type f = regex_constants::);
```

```cpp
// 3.8.4. count
unsigned mark_count count() const;
flag_type flags() const;
```

```cpp
// 3.8.6. locale
locale_type imbue(locale_type loc);
locale_type getloc() const;
```

```cpp
// 3.8.6. swap
void swap(basic_regex&);
```

# ISO/IEC 14882:2017(E)

```cpp
template<class ForwardIterator>
basic_regex(ForwardIterator first, ForwardIterator last,
    flag_type f = regex_constants::ECMAScript)
    -> basic_regex<typename ForwardIterator::value_type>;
```

# 31.8.1 constants

static constexpr regex_constants::syntax_option_type
icase = regex_constants::icase;
static constexpr regex_constants::syntax_option_type
nosub = regex_constants::nosub;
static constexpr regex_constants::syntax_option_type
optimize = regex_constants::optimize;
static constexpr regex_constants::syntax_option_type
collate = regex_constants::collate;
static constexpr regex_constants::syntax_option_type
ECMAScript = regex_constants::ECMAScript;
static constexpr regex_constants::syntax_option_type
basic = regex_constants::basic;
static constexpr regex_constants::syntax_option_type
extended = regex_constants::extended;
static constexpr regex_constants::syntax_option_type
awk = regex_constants::awk;
static constexpr regex_constants::syntax_option_type
group = regex_constants::group;
static constexpr regex_constants::syntax_option_type
egrep = regex_constants::egrep;
static constexpr regex_constants::syntax_option_type
multiline = regex_constants::multiline;

# 31.8.2 constructors

basic_regex();
explicit basic_regex(const charT p, flag_type f = regex_constants::ECMAScript);
basic_regex(const charT p, size_t len, flag_type f = regex_constants::ECMAScript);
basic_regex(const basic_regex&) noexcept;
template<class T, SA>
explicit basic_regex(const basic_string<charT, SA>& s,
    flag_type f = regex_constants::ECMAScript);
basic_regex(ForwardIterator first, ForwardIterator last,
basic_regex(initializer_list<charT> il, flag_type f = regex_constants::ECMAScript);

# 31.8.3 basic_regex assign

basic_regex assign(const basic_regex& that) noexcept;
basic_regex assign(const basic_regex& e) noexcept;
basic_regex assign(const charT* ptr, size_t len, flag_type f);
template<class string_traits, class A>
basic_regex assign(const basic_string<charT, string_traits>& s, A& s,
    flag_type f = regex_constants::ECMAScript);
template<class InputIterator>
basic_regex& assign(InputIterator first, InputIterator last,
    flag_type f = regex_constants::ECMAScript);
basic_regex assign(initializer_list<charT>,
    flag_type f = regex_constants::);

# 31.8.4 count

unsigned mark_count count() const;
flag_type flags() const;

# 31.8.6 locale

locale_type imbue(locale_type loc);
locale_type getloc() const;

# 31.8.6 swap

void swap(basic_regex&);
