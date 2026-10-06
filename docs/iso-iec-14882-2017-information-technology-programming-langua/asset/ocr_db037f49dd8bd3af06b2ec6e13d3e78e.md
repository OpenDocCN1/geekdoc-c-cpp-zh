# ISO/IEC 14882:2017(E)

size_type find_first_not_of(const basic_string& str, size_type pos = 0) const noexcept;

Effects: Equivalent to:
return find_first_not_of(basic_string_view<charT, traits>(str), pos);

size_type find_first_not_of(const char* s, size_type pos, size_type n) const;

Returns: find_first_not_of(basic_string_view<charT, traits>(s, n), pos;

size_type find_first_not_of(const char* s, size_type pos = 0) const;

Requires: s points to an array of least traits::length(s) + 1 elements of charT.

Returns: find_first_not_of(basic_string_view<charT, traits>(s), pos);

size_type find_first_not_of(const char* c, size_type pos = 0) const;

# 24.3.2.7 basic_string::find_last_of [string.find_last_not.of]

size_type find_last_not_of(basic_string_view<charT, traits> sv,
size_type pos = npos) const noexcept;

Effects: Determines the highest position, if both of the following conditions hold:

+   (1.1) xpos < at(pos) and pos < size();
(1.2) traits::eq(at(xpos), no element of the data referenced by

Returns: xpos if the function can determine a value for xpos. Returns npos;

size_type find_last_not_of(const charT* s, size_type pos = npos) const noexcept;

Effects: Equivalent to:
return find_last_not_of(basic_string_view<charT, traits>(str), pos);

size_type find_last_not_of(const charT* s, size_type pos, size_type n) const;

Returns: find_last_not_of(basic_string_view<charT, traits>(s, n), pos;

size_type find_last_not_of(const charT* s, size_type pos = npos) const;

Requires: s points to an array of least traits::length(s) + 1 elements of charT.

Returns: find_last_not_of(basic_string_view<charT, traits>(s), pos);

size_type find_last_not_of(const char* c, size_type pos = npos) const;

# 24.3.2.7.8 basic_string::substr [string.substr]

basic_string substr(size_type pos = 0, size_type n = npos) const;

Throws: out_of_range if pos > size();

Effects: Determines the effective length rlen of the copy as the smaller of n and size() -
pos.

Returns: basic_string(data() + pos, rlen).

©ISO/IEC 2017 - All rights reserved 754