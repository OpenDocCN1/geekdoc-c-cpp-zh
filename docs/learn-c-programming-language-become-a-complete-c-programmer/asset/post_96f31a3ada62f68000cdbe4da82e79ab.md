
because `?` does not mean “optional” in grep. For a more exhaustive presentation of regular expressions, see [Friedl,1997].

## 37.2 regex

A regular expression is a *matching engine* (usually a state machine) constructed from a sequence of characters, such as a **string**:

```
template<class C, class traits = regex_traits<C>>
class basic_regex {
public:

using value_type = C;
using traits_type = traits;
using string_type = typename traits::string_type;
using flag_type = regex_constants::syntax_option_type;
using locale_type = typename traits::locale_type;

~basic_regex(); // not virtual; basic_regex is not meant to be used as a base class // …
};
```

The **regex_traits** are presented in §37.5. Like **string**, **regex** is an alias for the version that uses **chars**:
`using regex = basic_regex<char>;`
The meaning of regular expression patterns is controlled by **syntax_option_type** constants defined identically in **regex_constants** and **regex**:

### `basic_regex<C,Tr>` Member Constants (`syntax_option_type`, §iso.28.5.1)

| Constant | Description |
|---|---|
| icase | No case is used when matching |
| nosubs | No subexpression matches are stored in the match results |
| optimize | Prefer fast matching to fast regular expression object construction |
| collate | Character ranges of the form [a–b] are locale sensitive |
| ECMAScript | The regular expression grammar is the one used by ECMAScript in ECMA-262 (with minor modifications; §iso.28.13) |

| Grammar | Description |
|---|---|
| basic | The regular expression grammar is the one used by basic regular expressions in POSIX |
| extended | The regular expression grammar is the one used by extended regular expressions in POSIX |
| awk | The regular expression grammar is the one used by POSIX awk |
| grep | The regular expression grammar is the one used by POSIX grep |
| egrep | The regular expression grammar is the one used by POSIX grep -E |

Use the default unless you have a good reason not to. Good reasons include a large body of existing regular expressions in a non-default notation.

A **regex** object can be constructed from a **string** or similar sequence of characters:

### `basic_regex<C,Tr>` Constructors (§iso.28.8.2)

| Expression | Description |
|---|---|
| `basic_regex r {};` | Default constructor: an empty pattern; flags set to `regex_constants::ECMAScript` |
| `basic_regex r {x, flags};` | x can be a `basic_regex`, a **string**, a C-style string, or an `initializer_list<value_type>` with the notation defined by **flags**; explicit |
| `basic_regex r {x};` | `basic_regex{x,regex_constants::ECMAScript}`; explicit |
| `basic_regex r {p,n,flags};` | Construct r from the characters in `[p:p+n)` with the notation defined by **flags** |
| `basic_regex r {p,n};` | `basic_regex{p,n,regex_constants::ECMAScript}` |
| `basic_regex r {b,e,flags}` | Construct r from the characters in `[b:e)` with the notation defined by **flags** |
| `basic_regex r {b,e};` | `basic_regex{b,e,regex_constants::ECMAScript}` |

The main use of **regex** is through the search, match, and replace functions (§37.3), but there are also a few operations on **regex** itself:

### `basic_regex<C,Tr>` Operations (§iso.28.8)

| Expression | Description |
|---|---|
| `r = x` | Copy assignment: x can be a **basic_regex**, a C-style string, a **basic_string**, or an **initializer_list<value_type>** |
| `r = move(r2)` | Move assignment |
| `r = r.assign(r2)` | Copy or move |
| `r = r.assign(x, flags)` | Copy or move; set r’s flags to **flags**; x can be a **basic_string**, a C-style string, or an **initializer_list<value_type>** |
| `r = r.assign(x)` | `r = r.assign(x, regex_constants::ECMAScript)` |
| `r = r.assign(p,n,flags)` | Set r’s pattern to `[p:p+n)` and r’s flags to **flags** |
| `r = r.assign(b,e,flags)` | Set r’s pattern to `[b:e)` and r’s flags to **flags** |
| `r = r.assign(b,e)` | `r = r.assign(b,e, regex_constants::ECMAScript)` |
| `n = r.mark_count()` | n is the number of marked subexpressions in r |
| `x = r.flags()` | x is r’s flags |
| `loc2 = r.imbue(loc)` | r gets the locale **loc**; loc2 is r’s previous **locale** |
| `loc = r.getloc()` | loc is r’s locale |
| `r.swap(r2)` | Exchange values of r and r2 |

You can determine the **locale** or a **regex** by a call of **getloc()** and learn what flags are used from **flags()**, but unfortunately there is no (standard) way of reading out its pattern. If you need to output a pattern, keep a copy of the string used to initialize. For example:

```
regex pat1 {R"(\w+\d*)"}; // no way of outputting the pattern in pat1
string s {R"(\w+\d*)"};
regex pat2 {s};
cout << s << '\n'; // the pattern in pat2
```

### 37.2.1 Match Results

Results from a regular expression match are gathered in a **match_results** object which contains one or more **sub_match** objects:

```
template<class Bi>
class sub_match : public pair<Bi,Bi> {
public:

using value_type = typename iterator_traits<Bi>::value_type;
using difference_type = typename iterator_traits<Bi>::difference_type;
using iterator = Bi;
using string_type = basic_string<value_type>;

bool matched; // true if *this contains a match
// ...

};
```

**Bi** must be a bidirectional iterator (§33.1.2). A **sub_match** can be seen as a pair of iterators into the string being matched.

| Expression | Operations |
|---|---|
| `sub_match<Bi> sm {};` | Default constructor: an empty sequence |
| `constexpr n = sm.length()` | n is the number of characters matched |
| `s=sm` | Implicit conversion of a **sub_match** to a **basic_string**; s is a **basic_string** containing the characters matched |
| `s=sm.str()` | s is a **basic_string** containing the characters matched |
| `x=sm.compare(x)` | Lexicographical comparison: `sm.str().compare(x)`; x can be a **sub_match**, a **basic_string**, or a C-style string |
| `x==y` | Is x equal to y? x and y can be a **sub_match** or a **basic_string** |
| `x!=y` | `!(x==y)` |
| `x<y` | x is lexicographically before y |
| `x>y` | `y<x` |
| `x<=y` | `!(x>y)` |
| `x>=y` | `!(x<y)` |
| `sm.matched` | true if sm contains a match; false otherwise |

For example:

```
regex pat ("<(.*?)>(.*?)</(.*?)>");
string s = "Always look for the <b> bright </b> side of <b> death </b>";
smatch m;
if (regex_search(s,m,pat))
    if (m[1]==m[3]) cout << "match\n";
```

The output is **match**.

A **match_results** is a container of **sub_matches**:

```
template<class Bi, class A = allocator<sub_match<Bi>>>
class match_results {
public:
using value_type = sub_match<Bi>;
using const_reference = const value_type&;
using reference = const_reference;
using const_iterator = /* implementation-defined*/;
using iterator = const_iterator;
using difference_type = typename iterator_traits<Bi>::difference_type;
using size_type = typename allocator_traits<A>::size_type;
using allocator_type = A;
using char_type = typename iterator_traits<Bi>::value_type;
using string_type = basic_string<char_type>;

~match_results(); // not virtual
// ...
};
```

Bi must be a bidirectional iterator (§33.1.2).

As for **basic_string** and **basic_ostream**, a few standard aliases are provided for the most common **match_results**:

```
using cmatch = match_results<const char *>; // C-style string
using wcmatch = match_results<const wchar_t *>; // wide C-style string
using smatch = match_results<string::const_iterator>; // string
using wsmatch = match_results<wstring::const_iterator>; // wstring
```

A **match_results** provides access to its match string, its **sub_matches**, and the characters before and after the match:

```
m[0]
m.prefix() m[1] ... m[m.size()] m.suffix()
```

A **match_results** provides a conventional set of operations:

### regex<C, Tr> Matches and Submatches (§iso.28.9, §iso.28.10)

| Expression | Description |
|---|---|
| `match_results m {};` | Default constructor: use `allocator_type{}` |
| `match_results m {a};` | Use allocator `a`; explicit |
| `match_results m {m2};` | Copy and move constructor |
| `m2 = m` | Copy assignment |
| `m2 = move(m)` | Move assignment |
| `m.~match_results()` | Destructor: release all resources |
| `m.ready()` | Does `m` hold a complete match? |
| `n = m.size()` | n is the number of sub_matches |
| `n = m.max_size()` | n is the maximum number of sub_matches |
