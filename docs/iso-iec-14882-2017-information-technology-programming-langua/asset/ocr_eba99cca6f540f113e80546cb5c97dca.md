# ISO/IEC 14882:2017(E)

basic_string& assign(size_type n, charT c);

Effects: Equivalent to assign(basic_string(n, c)).

Returns: *this.

template<class InputIterator>
basic_string& assign(InputIterator first, InputIterator last);

Effects: Equivalent to assign(basic_string(first, last, get_allocator()));

Returns: *this.

# 24.3.2.6.4 basic_string::insert [string.Insert]

basic_string&
insert(size_type pos,
const basic_string& str);

Effects: Equivalent to insert(pos, str.data(), str.size());

basic_string&
insert(size_type pos,
const basic_string& str,
size_type pos2, size_type n = npos);

Throws: out_of_range if pos > size() or pos2 > str.size();

Effects: Creates the length rlen of the string to insert as min of n and str.size()
- pos2 and calls insert(pos, str.data() + pos2, rlen).

Returns: *this.

basic_string& insert(size_type pos, const basic_string_view<charT, traits> sv);

Effects: Equivalent to return insert(pos, sv.data(), sv.size());

template<class T>
basic_string& insert(size_type pos, const T& t,
size_type pos2, size_type n = npos);

Throws: out_of_range if pos > size() or pos2 > sv.size();

Effects: Creates a variable, sv, as by basic_string_view<charT, traits> sv = t. Determines
the length rlen of the string to assign as min of n and sv.size()
insert(pos1, sv.data() + pos2, rlen).

Remarks: This function shall not participate in overload resolution unless is_convertible_v<const T, basic_string<const charT, traits>> is true and is_convertible_v<const T, char*>
is false.

Returns: *this.

basic_string&
insert(size_type pos, const charT* s, size_type n);

Requires: to insert an array of at least n elements of charT.

Throws: out_of_range if pos > size() or length_error if size() + n > max_size();

Effects: Replaces the string controlled by *this with a string of length size() + n whose first pos
elements are copies of the initial elements of the string controlled by *this and whose next n
elements are a copy of the elements in s and whose remaining elements are a copy of the remaining
elements of the original string controlled by *this.

 24.3.2.6.4

©ISO/IEC 2017 - All rights reserved 747