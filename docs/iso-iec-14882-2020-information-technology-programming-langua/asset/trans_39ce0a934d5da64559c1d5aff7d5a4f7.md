

## 21.3.3.7.7 basic_string::copy [string.copy]

```
constexpr size_type copy(charT* s, size_type n, size_type pos = 0) const;
```

Effects: Equivalent to: return basic_string_view<charT, traits>(*this).copy(s, n, pos);

[Note 1: This does not terminate s with a null object. — end note]

## 21.3.3.7.8 basic_string::swap [string.swap]

```
constexpr void swap(basic_string& s) noexcept(allocator_traits<Allocator>::propagate_on_container_swap::value || allocator_traits<Allocator>::is_always_equal::value);
```

Preconditions: allocator_traits<Allocator>::propagate_on_container_swap::value is true or get_allocator() == s.get_allocator().

Postconditions: *this contains the same sequence of characters that was in s, s contains the same sequence of characters that was in *this.

Throws: Nothing.

Complexity: Constant time.

## 21.3.3.8 String operations [string.ops]

## 21.3.3.8.1 Accessors [string.accessors]

```
constexpr const charT* c_str() const noexcept;
constexpr const charT* data() const noexcept;
```

Returns: A pointer p such that p + i == addressof(operator[](i)) for each i in [0, size()].

Complexity: Constant time.

## 21.3.3.8.3 basic_string::substr [string.substr]

```
constexpr basic_string substr(size_type pos = 0, size_type n = npos) const;
```

Throws: out_of_range if pos > size().

Effects: Determines the effective length rlen of the string to copy as the smaller of n and size() - pos.

Returns: basic_string(data()+pos, rlen).

## 21.3.3.8.4 basic_string::compare [string.compare]

```
template<class T>
  constexpr int compare(const T& t) const noexcept(see below);
```

Constraints:

+   - is_convertible_v<const T&, basic_string_view<charT, traits>> is true and
+   - is_convertible_v<const T&, const charT*> is false.

Effects: Equivalent to: return basic_string_view<charT, traits>(*this).compare(t);

Remarks: The expression inside noexcept is equivalent to is_nothrow_convertible_v<const T&, basic_string_view<charT, traits>>.

```
template<class T>
  constexpr int compare(size_type pos1, size_type n1, const T& t) const;
```

Constraints:

+   - is_convertible_v<const T&, basic_string_view<charT, traits>> is true and
+   - is_convertible_v<const T&, const charT*> is false.

Effects: Equivalent to:
  return basic_string_view<charT, traits>(*this).substr(pos1, n1).compare(t);

## 21.3.3.8.5 basic_string::starts_with [string.starts.with]

```
constexpr bool starts_with(basic_string_view<charT, traits> x) const noexcept;
constexpr bool starts_with(charT x) const noexcept;
constexpr bool starts_with(const charT* x) const;
```

Effects: Equivalent to:

```
return basic_string_view<charT, traits>(data(), size()).starts_with(x);
```

## 21.3.3.8.6 basic_string::ends_with [string.ends.with]

```
constexpr bool ends_with(basic_string_view<charT, traits> x) const noexcept;
constexpr bool ends_with(charT x) const noexcept;
constexpr bool ends_with(const charT* x) const;
```

Effects: Equivalent to:

```
return basic_string_view<charT, traits>(data(), size()).ends_with(x);
```

## 21.3.4 Non-member functions [string.nonmembers]

## 21.3.4.1 operator+ [string.op.plus]

```
template<class charT, class traits, class Allocator>
constexpr basic_string<charT, traits, Allocator>
operator+(const basic_string<charT, traits, Allocator>& lhs,
    const basic_string<charT, traits, Allocator>& rhs);
template<class charT, class traits, class Allocator>
constexpr basic_string<charT, traits, Allocator>
operator+(const basic_string<charT, traits, Allocator>& lhs, const charT* rhs);
```

Effects: Equivalent to:

```
basic_string<charT, traits, Allocator> r = lhs;
r.append(rhs);
return r;
```

```
template<class charT, class traits, class Allocator>
constexpr basic_string<charT, traits, Allocator>
operator+(basic_string<charT, traits, Allocator>&& lhs,
    const basic_string<charT, traits, Allocator>& rhs);
template<class charT, class traits, class Allocator>
constexpr basic_string<charT, traits, Allocator>
operator+(basic_string<charT, traits, Allocator>&& lhs, const charT* rhs);
```

Effects: Equivalent to:

```
lhs.append(rhs);
return std::move(lhs);
```

```
template<class charT, class traits, class Allocator>
constexpr basic_string<charT, traits, Allocator>
operator+(basic_string<charT, traits, Allocator>&& lhs,
    basic_string<charT, traits, Allocator>&& rhs);
```

Effects: Equivalent to:

```
lhs.append(rhs);
return std::move(lhs);
```

except that both lhs and rhs are left in valid but unspecified states.

> [Note 1: If lhs and rhs have equal allocators, the implementation can move from either. — end note]

```
template<class charT, class traits, class Allocator>
constexpr basic_string<charT, traits, Allocator>
operator+(const basic_string<charT, traits, Allocator>& lhs,
    basic_string<charT, traits, Allocator>&& rhs);
```

```
constexpr int compare(size_type pos, size_type n1, const charT* s, size_type n2) const;
```

Effects: Equivalent to: return compare(pos, n1, basic_string_view<charT, traits>(s, n2));

```
template<class charT, class traits, class Allocator>
constexpr see below operator<= (const basic_string<charT, traits, Allocator>& lhs,
const charT* rhs);
```

Effects: Let op be the operator. Equivalent to:

```
return basic_string_view<charT, traits>(lhs) op basic_string_view<charT, traits>(rhs);
```

## 21.3.4.3 swap [string.special]

```
template<class charT, class traits, class Allocator>
constexpr void
swap(basic_string<charT, traits, Allocator>& lhs,
basic_string<charT, traits, Allocator>& rhs)
noexcept(noexcept(lhs.swap(rhs)));
```

Effects: Equivalent to lhs.swap(rhs).

## 21.3.4.4 Inserters and extractors [string.io]

```
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>&
operator>>(basic_istream<charT, traits>& is, basic_string<charT, traits, Allocator>& str);
```

Effects: Behaves as a formatted input function (29.7.4.3.1). After constructing a sentry object, if the sentry converts to true, calls str.erase() and then extracts characters from is and appends them to str as if by calling str.append(1, c). If is.width() is greater than zero, the maximum number n of characters appended is is.width(); otherwise n is str.max_size(). Characters are extracted and appended until any of the following occurs:

+   (1.1) — n characters are stored;
+   (1.2) — end-of-file occurs on the input sequence;
+   (1.3) — isspace(c, is.getloc()) is true for the next available input character c.

After the last character (if any) is extracted, is.width(0) is called and the sentry object is destroyed.

If the function extracts no characters, it calls is.setstate(ios_base::failbit), which may throw ios_base::failure (29.5.5.4).

Returns: is.

```
template<class charT, class traits, class Allocator>
basic_ostream<charT, traits>&
operator<<(basic_ostream<charT, traits>& os,
const basic_string<charT, traits, Allocator>& str);
```

Effects: Equivalent to: return os << basic_string_view<charT, traits>(str);

```
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>&
getline(basic_istream<charT, traits>& is,
basic_string<charT, traits, Allocator>& str,
charT delim);
```

```
template<class charT, class traits, class Allocator>
basic_istream<charT, traits>&
getline(basic_istream<charT, traits>&& is,
basic_string<charT, traits, Allocator>& str,
charT delim);
```

Effects: Behaves as an unformatted input function (29.7.4.4), except that it does not affect the value returned by subsequent calls to basic_istream<>::gcount(). After constructing a sentry object, if the sentry converts to true, calls str.erase() and then extracts characters from is and appends them to str as if by calling str.append(1, c) until any of the following occurs:

+   (6.1) — end-of-file occurs on the input sequence (in which case, the getline function calls is.setstate(ios_base::eofbit)).
+   (6.2) — traits::eq(c, delim) for the next available input character c (in which case, c is extracted but not appended) (29.5.5.4)

