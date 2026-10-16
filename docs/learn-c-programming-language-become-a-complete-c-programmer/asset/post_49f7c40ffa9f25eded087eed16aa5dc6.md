
## 36.3.4 String I/O

A **basic_string** can be written using `<<` (§38.4.2) and read into using `>>` (§38.4.1):

**basic_string<C,Tr,A> I/O Operations (§iso.21.4.8.9)**

| Operation | Description |
|---|---|
| `in >> s` | Read a whitespace-separated word into `s` from `in` |
| `out << s` | Write `s` to `out` |
| `getline(in,s,d)` | Read characters from `in` into `s` until the character `d` is encountered; `d` is removed from `in` but not appended to `s` |
| `getline(in,s)` | `getline(in,s,'\n')`, where `'\n'` is widened to match the string’s character type |

An input operation that would cause `size()` to exceed `max_size()` will throw `std::length_error`. A `getline()` removes its terminator character (by default `‘\n’`) from the input stream but does not enter it into the string. This simplifies handling of lines. For example:

```
vector<string> lines;
for (string s; getline(cin,s);)
    lines.push_back(s);
```

The **string** I/O operations all return a reference to their input stream, so that operations can be chained. For example:

```
string first_name;
string second_name;
cin >> first_name >> second_name;
```

The **string** target of an input operation is set to empty before reading and expands to hold the characters read. A read operation can also be terminated by reaching end-of-file (§38.3).

## 36.3.5 Numeric Conversions

In **<string>**, the standard library provides a set of functions for extracting numeric values from their character representation in a **string** or **wstring** (note: not a **basic_string<C,Tr,A>**). The desired numeric types are encoded in the function names:

**Numeric Conversions (§iso.21.5) (continues)**

| Function or expression | Description |
|---|---|
| `s` | `s` can be a **string** or a **wstring** |
| `x=stoi(s,p,b)` | String to **int**; `x` is an integer; read starting with `s[0]` |
| `if p!=nullptr, *p` | Set to the number of characters used for `x`; `b` is the base of the number (between 2 and 36, inclusive) |
| `x=stoi(s,p)` / `x=stoi(s,p,10)` | Decimal numbers |
| `x=stoi(s)` / `x=stoi(s,nullptr,10)` | Decimal numbers; don’t report the character count |
| `x=stol(s,p,b)` | String to **long** |
| `x=stoul(s,p,b)` | String to **unsigned long** |
| `x=stoll(s,p,b)` | String to **long long** |
| `x=stoull(s,p,b)` | String to **unsigned long long** |

`errno` to `ERANGE` (§40.3). For example:

`stoi(“Hello, World!”);` // *throws* `std::invalid_argument`

`stoi(“12345678901234567890”);` // *throws* `std::out_of_range`; `errno=ERANGE`

`stof(“123456789e1000”);` // *throws* `std::out_of_range`; `errno=ERANGE`

The `sto*` functions encode their target type in their names. This makes them unsuitable for generic code where the target can be a template parameter. In such cases, consider `to<X>` (§25.2.5.1).

## 36.3.6 STL-like Operations

The `basic_string` provides the usual set of iterators:

`basic_string<C,Tr,A>` **String Iterators** (§iso.21.4.3)

All operations are noexcept

+   `p=s.begin()` p is an iterator to the first character of s  
+   `p=s.end()` p is an iterator to one beyond the end of s  
+   `p=s.cbegin()` p is a const_iterator to the first character  
+   `p=s.cend()` p is a const_iterator to one beyond the end of s  
+   `p=s.rbegin()` p is the beginning of the reverse sequence for s  
+   `p=s.rend()` p is the end of the reverse sequence for s  
+   `p=s.crbegin()` p is a const_iterator to the beginning of the reverse sequence for s  
+   `p=s.crend()` p is a const_iterator to the end of the reverse sequence for s

Because `string` has the required member types and the functions for obtaining iterators, `strings` can be used together with the standard algorithms (Chapter 32). For example:

```
void f(string& s)
{
    auto p = find_if(s.begin(),s.end(),islower);
    // ...
}
```

The most common operations on `strings` are supplied directly by `string`. Hopefully, these versions will be optimized for `strings` beyond what would be easy to do for general algorithms.

The standard algorithms (Chapter 32) are not as useful for strings as one might think. General algorithms tend to assume that the elements of a container are meaningful in isolation. This is typically not the case for a string.

A `basic_string` offers complex `assignment()`s:

`basic_string<C,Tr,A>` **Assignment** (§iso.21.4.6.3)

All operations return the string to which they are applied

+   `s.assign(x)` s=x ; x can be a `string`, a C-style string, or an `initializer_list<char_type>`  
+   `s.assign(move(s2))` Move: s2 is a `string`; noexcept  
+   `s.assign(s2,pos,n)` s gets the characters `s2[pos:pos+n)`  
+   `s.assign(p,n)` s gets the characters `[p:p+n)`; p is a C-style string  
+   `s.assign(n,c)` s gets n copies of the character c

## 36.4 Advice

- [1] Use character classifications rather than handcrafted checks on character ranges; §36.2.1.
- [2] If you implement string-like abstractions, use **character_traits** to implement operations on characters; §36.2.2.
- [3] A **basic_string** can be used to make strings of characters on any type; §36.3.
- [4] Use **strings** as variables and members rather than as base classes; §36.3.
- [5] Prefer **string** operations to C-style string functions; §36.3.1.
- [6] Return **strings** by value (rely on move semantics); §36.3.2.
- [7] Use **string::npos** to indicate “the rest of the **string**”; §36.3.2.
- [8] Do not pass a **nullptr** to a **string** function expecting a C-style string; §36.3.2.
- [9] A **string** can grow and shrink, as needed; §36.3.3.
- [10] Use **at()** rather than iterators or **[]** when you want range checking; §36.3.3, §36.3.6.
- [11] Use iterators and **[]** rather than **at()** when you want to optimize speed; §36.3.3, §36.3.6.
- [12] If you use **strings**, catch **length_error** and **out_of_range** somewhere; §36.3.3.
- [13] Use **c_str()** to produce a C-style string representation of a **string** (only) when you have to; §36.3.3.
- [14] **string** input is type sensitive and doesn’t overflow; §36.3.4.
- [15] Prefer a **string_stream** or a generic value extraction function (such as **to<X>**) over direct use of **str*** numeric conversion functions; §36.3.5.
- [16] Use the **find()** operations to locate values in a **string** (rather than writing an explicit loop); §36.3.7.
- [17] Directly or indirectly, use **substr()** to read substrings and **replace()** to write substrings; §36.3.8.

***This page intentionally left blank***

```
cout << "\t: " << matches[1] << '\n'; // submatch
}
}
}
```

This function reads a file looking for U.S. postal codes, such as TX77845 and DC 20500-0001. An smatch type is a container of regex results. Here, matches[0] is the whole pattern and matches[1] is the optional four-digit subpattern. I used a raw string (§7.3.2.1) which is particularly suitable for regular expressions because they tend to contain a lot of backslashes. Had I used a conventional string, the pattern definition would have been:

```
regex pat {"\w{2}\s *\d{5}(-\d{4})?"}; // U.S.postal code pattern
```

The regular expression syntax and semantics are designed so that regular expressions can be compiled into state machines for efficient execution [Cox,2007]. The regex type performs this compilation at run time.

## 37.1.1 Regular Expression Notation

The regex library can recognize several variants of the notation for regular expressions (§37.2). Here, I first present the default notation used, a variant of the ECMA standard used for ECMAScript (more commonly known as JavaScript).

The syntax of regular expressions is based on characters with special meaning: Regular Expression Special Characters

+   . Any single character (a “wildcard”) \ Next character has a special meaning [ Begin character class * Zero or more
+   ] End character class + One or more
+   { Begin count ? Optional (zero or one)
+   } End count | Alternative (or)
+   ( Begin grouping ^ Start of line; negation
+   ) End grouping $ End of line

For example, we can specify a line starting with zero or more As followed by one or more Bs followed by an optional C like this:

```
^A *B+C?$
```

Examples that match:

```
AAAAAAAAAAABBBBBBBBBBC
BC
B
```

Examples that do not match:

```
AAAAA // no B
AAAABC // initial space
AABBCC // too many Cs
```

A part of a pattern is considered a subpattern (which can be extracted separately from an smatch) if it is enclosed in parentheses.

A pattern can be optional or repeated (the default is exactly once) by adding a suffix:
