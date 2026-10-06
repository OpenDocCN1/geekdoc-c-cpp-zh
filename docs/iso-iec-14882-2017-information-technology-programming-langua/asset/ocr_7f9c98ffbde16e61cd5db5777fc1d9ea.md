# ISO/IEC 14882:2017(E)

```
7 Requires: !empty().
8 Effects: Equivalent to return operator [] (0);
const charT& back() const;
charT& back();
9 Requires: !empty().
10 Effects: Equivalent to return operator [] (size() - 1);
```

# 24.3.2.6 basic_string modifiers

# 24.3.2.6.1 basic_string::operator+=

```
basic_string&
operator+=(const basic_string& str);
1 Effects: Calls append(str).
2 Returns: *this.
basic_string operator+=(basic_string_view<charT, traits> sv);
3 Effects: Calls append(sv).
4 Returns: *this.
basic_string operator+=(const charT* s);
5 Effects: Calls append(s).
6 Returns: *this.
basic_string operator+=(charT c);
7 Effects: Calls push_back(c);
8 Returns: *this.
basic_string operator+=(initializer_list<charT> il);
9 Effects: Calls append(il).
10 Returns: *this.
```

# 24.3.2.6.2 basic_string::append

```
basic_string&
append(const basic_string& str);
1 Effects: Calls append(str.data(), sv.size()).
2 Returns: *this.
basic_string&
append(const basic_string& str, size_type pos, size_type n = npos);
3 Throws: out_of_range if pos > str.size().
4 Effects: Determines the effective length rlen of the smaller of n and str.size()
- pos and calls append(str.data() + pos, len).
5 Returns: *this.
basic_string& append(basic_string_view<charT, traits> sv);
6 Effects: Equivalent to return append(sv.data(), sv.size());
```