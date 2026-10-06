# ISO/IEC 14882:2017(E)

> [Note: Unlike basic_string::data() and string literals, data() may return a pointer to a buffer that is not-terminated. Therefore it is typically a mistake to pass data() to a function that just takes a const charT* and expects a null-terminated string.— end note]

# 24.4.2.5 Modifiers [string.view.modifiers]

constexpr void remove_prefix(size_type n);

+   - Requires: n <= size();

+   - Equivalent to: data() == n; size() == n;

constexpr void remove_suffix(size_type n);

+   - Requires: n <= size();

+   - Equivalent to: size() -- n == n;

constexpr void swap(basic_string_view& s) noexcept;

+   - Effects: Exchanges the values of *this and other.

# 24.4.2.6 String operations [string.view.ops]

size_type copy(size_type n, size_type n, size_type pos = 0) const;

+   - Let rlen the smaller of n and size() - pos.

+   - Throws: out_of_range if pos > size().

+   - Requires: rlen is a valid range.

+   - Effects: Equivalent to traits::copy(s, data() + pos, rlen).

+   - Returns: rlen.

+   - Complexity: O(rlen).

constexpr basic_string_view substr(size_type pos = 0, size_type n = npos) const;

+   - Let rlen the smaller of n and size() - pos.

+   - Throws: out_of_range if pos > size().

+   - Effects: Returns rlen, the effective length of the string to the reference.

+   - Returns: basic_string_view(data() + pos, rlen).

constexpr compare(basic_string_view str) const noexcept;

+   - Let rlen the smaller of size() and str.size().

+   - Effects: Returnslen, the effective length of the strings to compare. The function then compares the two strings by calling traits::compare(data(), str.data(), rlen).

+   - Complexity: O(rlen).

+   - Returns: The nonzero result if the result of the comparison is nonzero. Otherwise, returns a value as indicated in Table 6.

constexpr compare(size_type pos1, size_type n1, basic_string_view str) const;

+   - Effects: Equivalent to return substr(pos1, n1).compare(str);

constexpr compare(size_type pos1, size_type n1, basic_string_view str, size_type pos2, size_type n2) const;

+   - Effects: Equivalent to return substr(pos1, n1).compare(str.substr(pos2, n2));