# ISO/IEC 14882:2017(E)

+   (9.3) traits::eq(atpos + I), str.at(I) for all elements I of the string referenced by str.

+   10 Effects: Returns npos.

+   11 Returns: xpos if the function can determine a value for xpos. Otherwise, returns npos.

```
constexpr size_type find_first_of(basic_string_view str, size_type npos = 0) const noexcept;
```

+   12 Let xpos be the lowest position, if possible, such that the following conditions hold:

+   (12.1) pos < size()

+   (12.2) xpos < size()

+   (12.3) traits::eq(at(xpos), str.at(I)) for some element I of the string referenced by str.

+   13 Effects: Determines npos.

+   14 Returns: xpos if the function can determine a value for xpos. Otherwise, returns npos.

```
constexpr size_type find_last_not_of(basic_string_view str, size_type npos = npos) const noexcept;
```

+   15 Let xpos be the highest position, if possible, such that the following conditions hold:

+   (15.1) pos < xpos

+   (15.2) xpos < size()

+   (15.3) traits::eq(at(xpos), str.at(I)) for no element I of the string referenced by str.

+   16 Effects: Determines npos.

+   17 Returns: xpos if the function can determine a value for xpos. Otherwise, returns npos.

```
constexpr size_type find_last_not_of(basic_string_view str, size_type npos = npos) const noexcept;
```

+   18 Let xpos be the lowest position, if possible, such that the following conditions hold:

+   (18.1) pos < xpos

+   (18.2) xpos < size()

+   (18.3) traits::eq(at(xpos), str.at(I)) for no element I of the string referenced by str.

+   19 Effects: Determines npos.

+   20 Returns: xpos if the function can determine a value for xpos. Otherwise, returns npos.

```
constexpr size_type find_last_not_of(basic_string_view str, size_type npos = npos) const noexcept;
```

+   21 Let xpos be the highest position, if possible, such that the following conditions hold:

+   (21.1) xpos < size()

+   (21.3) traits::eq(at(xpos), str.at(I)) for no element I of the string referenced by str.

+   22 Effects: Determines npos.

+   23 Returns: xpos if the function can determine a value for xpos. Otherwise, returns npos.

# 24.4.3 Non-member comparison functions [string::comparison]

Let S basic_string_view<char, traits> and sv be instances of S. Implementations shall provide sufficient additional overloads marked constexpr noexcept so that an object t with an implicit conversion to S can be compared against Table 67.

> [Example: A conforming implementation for operator== would be:

```
template<class T> using __identity = decay_t<T>;
```