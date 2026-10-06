# ISO/IEC 14882:2017(E)

basic_string& operator=(charT c);

Returns:*this = basic_string(1, c).

basic_string& operator=(initializer_list<charT> il);

Effects: As if: *this = basic_string(il);

Returns:*this.

# 24.3.2.3 basic_string iterator support

[string.iterators]

```
iterator
begin() noexcept;
const_iterator begin() const noexcept;
const_iterator cbegin() const noexcept;
```

Returns An iterator referring to the first character in the string.

```
iterator
end() noexcept;
const_iterator end() const noexcept;
const_iterator cend() const noexcept;
```

Returns An iterator which is the past-the-end value.

```
reverse_iterator
begin() noexcept;
reverse_iterator rbegin() const noexcept;
reverse_iterator crbegin() const noexcept;
```

Returns An iterator which is semantically equivalent to reverse_iterator(end()).

```
reverse_iterator
rend() noexcept;
reverse_iterator rend() const noexcept;
reverse_iterator crnd() const noexcept;
```

Returns An iterator which is semantically equivalent to reverse_iterator(begin()).

# 24.3.2.4 basic_string capacity

[string.capacity]

```
size_type size() const noexcept;
```

Returns a count of the number of char-like objects currently in the string.

Complexity: Constant time.

```
size_type length() const noexcept;
```

Returns size().

```
size_type max_size() const noexcept;
```

Returns The largest possible number of char-like objects that can be stored in a basic_string.

Complexity: Constant time.

```
void resize(size_type n, charT c);
```

Throws: length_error if n > max_size().

Effects: Alters the length of the string designated by *this as follows:

+   - If n < size(), the replaces the string designated by *this with a length of n whose elements are a copy of the initial elements of the original string designated by *this.
- If n > size(), the function replaces the string designated by *this with a length of n whose first size() elements are a copy of the original string designated by *this, and whose remaining elements are all initialized to c.