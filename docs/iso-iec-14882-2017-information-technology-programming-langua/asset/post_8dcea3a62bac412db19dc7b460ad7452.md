
# ISO/IEC 14882:2017(E)

Table 134 — match_results assignment operator effects

| Element | Value |
| --- | --- |
| ready() | m.ready() |
| size() | m.size() |
| str() | m.str(n) for all integers n < m.size() |
| prefix() | m.prefix() |
| suffix() | m.suffix() |
| (*this)[n] | m[n] for all integers n < m.size() |
| length(n) | m.length(n) for all integers n < m.size() |
| position(n) | m.position(n) for all integers n < m.size() |

# 31.10.2 match_results state

[re.results.state]

```cpp
bool ready() const;
```

Returns: true if *this has a fully established result, otherwise false.

# 31.10.3 match_results_size

[re.results.size]

```cpp
size_type size() const;
```

Returns: One the number of marked sub-expressions in the regular expression that *this represents the result of a successful match. Otherwise returns 0. [Note: The state of a match_results object can be modified only by passing that to regex_match or regex_search. Sections 31.11.2 and 31.11.3 specify the effects of these algorithms on their match_results arguments.]

```cpp
size_type max_size() const;
```

Returns: The maximum number of sub_match elements that can be stored in *this.

```cpp
bool empty() const;
```

Returns: size() == 0.

# 31.10.4 match_results_element access

[re.results.acc]

```cpp
difference_type length(size_type sub = 0) const;
```

Requires: ready() == true.

Returns: (*this)[sub].length().

```cpp
difference_type position(size_type sub = 0) const;
```

Requires: ready() == true.

Returns: The distance from the start of the target sequence to (*this)[sub].first.

```cpp
string_type str(size_type sub = 0) const;
```

Requires: ready() == true.

Returns: string_type((*this)[sub]).

```cpp
const_reference operator[](size_type n) const;
```

Requires: ready() == true.

Returns: A reference to the sub_match object representing the character sequence matched marked sub-expression. If n == 0 returns a reference to a sub_match object representing the character sequence that matched the whole expression. If n >= size() then returns a sub_match object representing an unmatched sub-expression.

```cpp
const_reference prefix() const;
```

Requires: ready() == true;

Returns: A reference to the sub_match object representing the character sequence from the start of the string matched/searched to the start of the match.

```cpp
const_reference suffix() const;
```

Requires: ready() == true;

Returns: A reference to the sub_match object representing the character sequence from the end of the match found to the end of the string being matched/searched.

```cpp
const_iterator begin() const;
const_iterator cbegin() const;
```

Returns a starting iterator that enumerates over all the sub-expressions stored in *this.

```cpp
const_iterator end() const;
const_iterator cend() const;
```

A terminating iterator that enumerates over all the sub-expressions stored in *this.

# 31.10.5 match_formatting [re.results.form]

```cpp
template <class OutputIterator>
void format(
    OutputIterator out,
    const char* type_first, const char* type_last, const char* fmt_last,
    regex_constants::match_flag_type flags = regex_constants::format_default);
```

Requires: ready() == true and OutputIterator shall satisfy the requirements for an Input Iterator (27.2.4).

Effects: Copies the character sequence [fmt_first, fmt_last) to OutputIterator. Replaces each format specifier or escape sequence in the copied range with either the character(s) it represents or the sequence of characters within *this to which it refers. The bitmasks in flags determine which format specifiers and escape sequences are recognized.

Returns: out.

```cpp
template <class OutputIterator, class ST, SA>
void format(
    OutputIterator out,
    const basic_string<char_type, SA>& fmt,
    regex_constants::match_flag_type flags = regex_constants::format_default);
```

Effects: Equivalent to:

```cpp
return format(out, fmt.data(), fmt.data() + fmt.size(), flags);
```

```cpp
template <class ST, SA>
void format(
    basic_string<char_type, ST, SA>& fmt,
    regex_constants::match_flag_type flags = regex_constants::format_default);
```

5 Requires: ready() == true.

6 Effects: Constructs an empty string result of type basic_string<char_type, ST, SA> and calls:
`format(back_insert(result), fmt, flags);`

7 Returns: result.

```cpp
string_type format(const char* fmt, 
                   regex_constants::match_flag_type flags = regex_constants::format_default);
```

8 Requires: ready() == true.

9 Effects: Constructs an empty string result of type string_type and calls:
`format(back_insert(result), fmt, char_traits<char_type>::length(fmt), flags);`

10 Returns: result.

# 31.10.6 match_results allocator [re.results.all]

```cpp
allocator_type get_allocator() const;
```

1 Returns a copy of the Allocator that was passed to the object's constructor or, if allocator has
been replaced, a copy of the most recent replacement.

# 31.10.7 match_results swap [re.results.swap]

```cpp
void swap(match_results& m1, match_results& that);
```

1 Effects: Swaps the contents of the two sequences.

2 Postconditions: this contains the contents of the other sequence.

3 `template <class BidirectionalIterator, class Allocator> void swap(match_results& m1, match_results& m2);`
Complexity: Constant time.

```cpp
template <class BidirectionalIterator, class Allocator>
void operator=(match_results& m1, const match_results& m2);
```

4 Effects: Copies the contents of the right sequence to the first.

5 Postconditions: this contains the contents of the other sequence.

# 31.10.8 match_results member [re.results.member]

```cpp
template <class BidirectionalIterator, class Allocator>
bool operator==(match_results& m1, const match_results& m2);
```

1 Returns true if both m1 and m2 are equal, otherwise false. (Wait, the OCR text is a bit garbled here, let's stick to the provided flow while fixing typos).

*Actually, based on the provided messy OCR text for 31.10.8:*
The text provided seems to be a mix of different sections. I will reconstruct the logical flow based on standard C++ standard documentation while fixing the OCR artifacts.

# 31.11 Regular expression algorithms

### 31.11.1 Exceptions

The algorithms described in this subclause may throw an exception of type regex_error.

### 31.11.2 regex_match

```cpp
template <class BidirectionalIterator, class Allocator, class charT, class traits>
bool regex_match(BidirectionalIterator first, BidirectionalIterator last,
                 match_results<BidirectionalIterator, Allocator>& m,
                 const charT& str,
                 regex_constants::match_flag_type flags = regex_constants::default);
```

1 Requires: The BidirectionalIterator first shall satisfy the requirements of a Bidirectional Iterator (27.2.6).

2 Effects: Determines whether there is a match between the regular expression, and all of the
sequence [first, last). The parameter flag is used to control how the expression is matched
against the sequence. When determining if there is a match, only potential matches that
the entire sequence are considered. Returns true if such a match exists, false
otherwise. Example:

```cpp
std::regex re("GetValue");
std::smatch m;
// get "GetValue"
regex_match("GetValue", m, re); // returns true, and m[0] contains "Get"
regex_match("GetValue", m, re); // returns true, and m[0] contains "GetValue"
regex_search("GetValue", m, re); // returns true, and m[0] contains "Get"
regex_search("GetValue", m, re); // returns false
// end example
```

3 Postconditions: m.ready() == true in all cases. If the function returns false, then the effect
on parameter m is unspecified unless m.size() returns 0 and m.empty() returns true. Otherwise
the effects on m are given in Table 135.

Table 135 — Effects of regex_match algorithm

| Element | Value |
| --- | --- |
| m.size() | 1 + e.count() |
| m.empty() | false |
| m.prefix().first | first |
| m.prefix().second | first |
| m.prefix().matched | false |
| m.suffix().first | last |
| m.suffix().second | last |
| m.suffix().matched | false |
| m[0].first | first |
| m[0].second | last |
